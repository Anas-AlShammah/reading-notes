Identity
Identity is the ability to add Authentication and Authorization to your web application. This includes registrations, logins, restricted access to specific members, and authentication through Facebook, Google, Twitter, etc...

ASP.NET Core Identity was created to help with the security and management of users. It provides this abstraction layer between the application and the users/role data. We can use the API in it's entirety, or just bits and pieces as we need (such as the salting/hashing by itself) or email services. There is a lot of flexibility within ASP.NET Core Identity. We have the ability to take or leave whatever we want. Identity combines well with EFCore and SQL Server.

Integration Steps
Install Dependency: Identity Framework
Create a new user model, inheriting from IdentityUser
Add that model to your DbContext
Migrate the data, to create all of the Identity tables
Create related DTO's for login, register, user for use in services and controllers
This is part of pre-planning your application architecture
Create an IUser Interface to handle Authentication() and Register()
Should use the identity framework to log users in
Add the IUser service to your services configuration
Add an empty controller and add the /register and /signin routes, using your new service
Installing and Configuring "Identity"
Add Dependency: Microsoft.AspNetCore.Identity.EntityFrameWorkCore
Installs libraries as well as models for identities
Add an "Application User" Model
Notice how this inherits from IdentityUser, which we "got for free" from the dependency, which is a default implementation for a user

Create the user model
namespace SchoolDemo.Models
{
  public class ApplicationUser : IdentityUser
  {
  }
}
Add this to our DbContext
In our Data/SchoolDbContext class:
Change the class to inherit from IdentityDbContext instead of DbContext
This also inherits from DbContext as well as to bring in it's own requirements
We will also need to uncomment the base line, because Identity uses it to add it's own stuff
...

  public class SchoolDbContext : IdentityDbContext<ApplicationUser>
  {
    public SchoolDbContext(DbContextOptions options) : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
      // This calls the base method, and Identity needs it
      base.OnModelCreating(modelBuilder);
...
Migrate the data
What data? Our model is empty ... actually, we changed it to Inherit from Identity, so let's see what it did

PM Console: PM> add-migration identity

Power Shell: dotnet ef migrations add Identity

Look all the tables it's about to create!

PM Console: PM> update-database

Power Shell: dotnet ef database update

Now, inspect your DB to see the users tables. They will all be prefixed with dbo.AspNet

Register the identity services
Before we can do anything in our controllers, we need to register the proper services:

In Startup.cs in ConfigureServices

 services.AddIdentity<ApplicationUser, IdentityRole>(options =>
 {
   options.User.RequireUniqueEmail = true;
   // There are other options like this
 })
 .AddEntityFrameworkStores<SchoolDbContext>();

services.AddTransient<IUserService, IdentityUserService>
Note the last line. This is an interface and service we need to create ...

User Service
Create an empty IUserService Interface

Think: What methods do we probably need to manage a user?
public Task<UserDto> Register(RegisterUser data, ModelStateDictionary modelState);
public Task<UserDto> Authenticate(string username, string password);
Create am empty IdentityUserService Service Class that implements the above interface

DTO's
We will need 2 DTOs ...

UserDto - Outbound
Returned by the service when we register and authenticate

public class UserDto
{
  public string Id { get; set; }
  public string Username { get; set; }
}
RegisterUserDto - Inbound
Used by the Register() method to add a user to the Identity database

public class RegisterUser
{
  [Required]
  public string Username { get; set; }

  [Required]
  public string Password { get; set; }

  [Required]
  public string Email { get; set; }

  public string PhoneNumber { get; set; }
}
Create a new controller UsersController (Empty)
Use DI to have IUserService injected
Building out the API ... for the first route, work backward

Start in the controller and build out the Register() method

Use HttpPost("register") as the method
It should take in a specialized data shape as the POST BODY
Next, build the base method in IdentityUserService called Register() that takes in this DTO and (for now) doesn't implement it

Fix the bugs by adding that method signature to the Interface
 public Task<ApplicationUser> Register(RegisterUser data)
 {
   throw new NotImplementedException();
 }
At this point, you should be able to post to the route from Swagger or postman, and see the "Not Implemented" error, which is good. We're "Hooked Up"

While here, debug the route and prove that the object is coming in as expected

Identity: Register: Save the user to the database
Connect to Identity's "User Manager" to do the database work

The Service needs to implement UserManager in the constructor
private UserManager<ApplicationUser> userManager;

public IdentityUserService(UserManager<ApplicationUser> manager)
{
  userManager = manager;
}
Next, build out the Register method in the service, using UserManager

Ref: Services/IdentityUserService.cs
public async Task<ApplicationUser> Register(RegisterUser data)
{
  // throw new NotImplementedException();
  var user = new ApplicationUser
  {
    UserName = data.Username,
    Email = data.Email,
    PhoneNumber = data.PhoneNumber
  };

  var result = await userManager.CreateAsync(user, data.Password);

  if (result.Succeeded)
  {
    return user;
  }
  return null;
}
Run this with simple usernames and passwords.

Debug. What does "result" say?
Get your data compliant, and try again

Result is good, so we get back a full user object with "EVERYTHING"
What's that hashed password? Great time to talk about how this actually works ...
What happens if you add the same user again?

Yep, more errors
How can we modify this entire process to be more user friendly?

For the Happy Path, Let's make a new DTO that returns a simplified new user
Ref: Models/Api/UserDto.cs

namespace SchoolDemo.Models.Api
{
  public class UserDto
  {
    public string Id { get; set; }
    public string Username { get; set; }
  }
}
Add another fake user to see that the below DTO is being returned right

For errors, we're going to use a feature of EF called a ModelStateDictionary
This allows us to create any number of key/value pairs to indicate the state of the data model.

We can use this to inform the user as to what's happening

Change the signature of the method in the Interface and Service:

public async Task<UserDto> Register(RegisterData data, ModelStateDictionary modelState)
In the service, create a dictionary of error keys if there's an error

Note: This is boilerplate ...

foreach (var error in result.Errors)
{
  var errorKey =
      error.Code.Contains("Password") ? nameof(data.Password) :
      error.Code.Contains("Email") ? nameof(data.Email) :
      error.Code.Contains("UserName") ? nameof(data.Username) :
      "";
  modelState.AddModelError(errorKey, error.Description);
}
