Creating a View Component
First things first, how do you create a View Component? (I typically place all my View Components in a "ViewComponents" folder inside my web site project.) View Components typically consist of two parts:

A View Component class
A Razor View
public class InvokeExample2ViewComponent : ViewComponent
{
    public IViewComponentResult Invoke()
    {
        return View();
    }
}
And they are called from within one another Razor View:

@await Component.InvokeAsync("NamingConvention1")
Or called from within an MVC Controller method:

public IActionResult GetByClientSide()
{
    return ViewComponent(typeof(FromBrowserComponent));
}

View Component Naming Conventions
Let’s review the various ways in which ViewComponents can be named:

Can add the suffix "ViewComponent" to the end of the class name
Can be a class that inherits from "ViewComponent"
Can be a class that utilizes the "ViewComponent" Attribute
Can be a class that utilizes the "ViewComponent" Attribute and the Name Property
Can implement another class that inherits from "ViewComponent"
Note: An actual View Component doesn’t need to inherit from ViewComponent class, but if you don’t do this then you need to return an object that is of type IViewComponentResult. Inheriting from ViewComponent will allow you to call the View() or Content() method as well as be able to access other contextual items such as the ViewBag.


Returning Views for ViewComponent
View Components that inherit from ViewComponent class are able to call the View() method. When no specific view is called out, the view is searched in the following two ways and in the following order:

Views/{ControllerName}/Components/{ComponentName}/Default.cshtml
Views/Shared/Components/{ComponentName}/Default.cshtml

You can have the view in either location or both:

1. View Component views in Shared > Components folder: Since there is no Component view for “Defining1” in the VCViews/Components folder, the Shared/Defining1/Default.cshtml view is used.

View Components Folder Structure

2. View Component views in Controller > Components folder: Even though there is a "Shared/Components/Defining2/Default.cshtml" view, there is a Controller specific view "VCViews/Components/Defining2/Default.cshtml" as well. In such cases, the Controller specific views takes priority.

View Components Folder Structure

3. Returning a specific view: You can also specify the View you want to use rather than having it be Default.

return View("AnotherView");
View Components Folder Structure


View Component Invoke Methods
View Components implement either Invoke or InvokeAsync.

InvokeAsync is attempted to be found first, and if that doesn’t exist, Invoke is attempted to be found and run. The Invoke/InvokeAsync methods can be overloaded to take parameters. Regardless of the method that is implemented in a View Component, all calls from a Razor View will be as @await Component.InvokeAsync.

1. Invoke Asynchronously: Example of a View Component that uses the InvokeAsync method.

public class InvokeExample1ViewComponent : ViewComponent
{
    public async Task<IViewComponentResult> InvokeAsync()
    {
        return await Task.FromResult(View());
    }
}
2. Invoke Synchronously: Example of a View Component that uses the Invoke method.

public class InvokeExample2ViewComponent : ViewComponent
{
    public IViewComponentResult Invoke()
    {
        return View();
    }
}
3. Passing in Parameters to Invoke/InvokeAsync: Example of a View Component that is overloading the InvokeAsync method and taking parameters being passed into it.

await Component.InvokeAsync("InvokeExample4", new { id = 4 })
public class InvokeExample4ViewComponent : ViewComponent
{
    public IViewComponentResult Invoke(int id, bool isNew)
    {
        return isNew ? View("WithParametersLatest") : View("WithParameters");
    }
}
4. Invoked as TagHelper: New as of .Net Core 1.1 is the ability to call View Components as TagHelpers. All View Component TagHelpers are prefixed with “vc:”. The View Component name is all lowercase with it being kebab’d. The parameters to be passed in are treated as attributes with their names kebab’d as well.

<vc:invoke-example4 id="4" is-new="true"></vc:invoke-example4>
5. Javascript and View Components: View Components cannot be directly called from an HTTP request, but there are workarounds. You can call a controller and then from there have the controller call the View Component

public IActionResult GetByClientSide()
{
    return ViewComponent(typeof(FromBrowserComponent));
}
View Component Constructor
An important item to know about View Components and the work that is performed inside its methods is that the constructor allows for other classes to be injected.

Complex Examples
In my previous post "TagHelpers in .Net Core", I showed you some complex examples of using Custom Tag Helpers. In this post, we will take those same examples, but instead of using Custom Tag Helpers, I will use View Components. Something important to note is that both examples call ProductItemViewComponent, but because each example is initiated from a different controller, a different view of the Product Item is displayed. Another item to note is that in the Checkout example, I make a call to CartItemsViewComponent, which in turn has its view call another View Component, so you can see that nesting View Components is allowed.

List of Products Example

View Components Output

Views/Product/Items.cshtml

@model IList<int>
@{
    ViewData["Title"] = "Product Items";
}

<h2>Product Items</h2>
<div class="row">
    @foreach (var itemId in Model)
    {
        <div class="col-md-4">
            @await Component.InvokeAsync("ProductItem", new { productId = itemId })
        </div>
    }
</div>
ViewComponents/ProductItemViewComponent.cs

public class ProductItemViewComponent : ViewComponent
{
    private readonly IProductManager _productManager;

    public ProductItemViewComponent(IProductManager productManager)
    {
            _productManager = productManager;
    }

    public IViewComponentResult Invoke(int productId)
    {
        var productItem = _productManager.GetById(productId);
            return View(productItem);
    }
}
Views/Product/Components/ProductItem/Default.cshtml

@model BlogViewComponent.Core.Models.ProductItemModel

<div class="product-item">
    <div class='row'>
        <div class='col-md-12'>
            <img src='../images/@Model.ImageName-300.png' class="pull-left" />
        </div>
    </div>

    <div class='row title'>
        <div class='col-md-8'>
            <label>@Model.Name</label>
        </div>
        <div class='col-md-4'>
            <label>@Model.Price</label>
        </div>
    </div>

    <div class='row'>
        <div class='col-md-12'>
            <span>@Model.Description</span>
        </div>
    </div>
</div>

Checkout Page Example
View Components Output


Checkout.cshtml

@model int
@{
    ViewData["Title"] = "Product Items";
}

<h2>Checkout</h2>
<div class="row">
    <div class="col-md-9">
        @await Component.InvokeAsync("CartItems", new { cartId = Model })
    </div>
    <div class="col-md-3">
        @await Component.InvokeAsync("CartTotal", new { cartId = Model })
    </div>
</div>
ViewComponents/CartItemsViewComponent.cs

public class CartItemsViewComponent : ViewComponent
{
    private readonly ICartManager _cartManager;

    public CartItemsViewComponent(ICartManager cartManager)
    {
        _cartManager = cartManager;
    }

    public IViewComponentResult Invoke(int cartId)
    {
        var cartItemIds = _cartManager.GetCartItems(cartId);
            return View(cartItemIds);
    }
}
Views/Shared/Components/CartItems/Default.cshtml: Notice that this view of a View Component calls another View Component.

@model IList<int>

<table class="table">
    <thead>
        <tr>
            <th>Product Info</th>
            <th>Price</th>
        </tr>
    </thead>

    <tbody>
        @foreach (var id in Model)
        {
            @await Component.InvokeAsync("ProductItem", new { productId = id })
        }
    </tbody>
</table>
Views/Cart/Components/ProductItem/Default.cshtml : This is a different view that the ProductItemViewComponent calls based upon the Controller that the HTTP Request is called through.

@model BlogViewComponent.Core.Models.ProductItemModel

<tr>
    <td>
        <img src="../images/@Model.ImageName-100.png" />
        <label>@Model.Name</label>
        <span>@Model.Description.Substring(0, 80)</span>
    </td>
    <td>$@Model.Price</td>
</tr>
View Components/CartTotalViewcomponent.cs

public class CartTotalViewComponent : ViewComponent
{
    private readonly ICartManager _cartManager;

    public CartTotalViewComponent(ICartManager cartManager)
    {
        _cartManager = cartManager;
    }

    public IViewComponentResult Invoke(int cartId)
    {
        var cartTotals = _cartManager.GetCartTotals(cartId);
            return View(cartTotals);
    }
}
Views/Shared/Components/CartTotal/Default.cshtml

@model BlogViewComponent.Core.Models.CartTotalsModel

<form class="cart-totals form-horizontal">
    <div class='form-group'>
        <label class='col-md-6'>Subtotal:</label>
        <div class='col-md-6'>
            <span class='form-control-static'>$@Math.Round(Model.Subtotal, 2)</span>
        </div>
    </div>

    <div class='form-group'>
        <label class='col-md-6'>Tax:</label>
        <div class='col-md-6'>
            <span class='form-control-static'>$@Math.Round(Model.Tax, 2)</span>
        </div>
    </div>

    <div class='form-group'>
        <label class='col-md-6'>Shipping:</label>
        <div class='col-md-6'>
            <span class='form-control-static'>$@Math.Round(Model.ShippingAmount, 2)</span>
        </div>
    </div>

    <div class='form-group'>
        <label class='col-md-6'>Total:</label>
        <div class='col-md-6'>
            <span class='form-control-static'>$@Math.Round(Model.Subtotal + Model.Tax + Model.ShippingAmount, 2)</span>
        </div>
    </div>
</form>
