What is Jamstack?
Jamstack is a term that describes a modern web development architecture based on JavaScript, APIs, and Markup (JAM). Jamstack isn’t a specific technology or framework but a different architecture for building apps and websites.

Instead of using a traditional CMS or site builder, a Jamstack site splits up the code (JavaScript), the site infrastructure (APIs), and the content (Markup). These will all be handled in a decoupled architecture and with a clear split between server-side and client-side. In fact, the main idea behind building Jamstack websites and applications is to push as much of the load as possible away from the server and onto the client. By doing so, it dramatically reduces the number of requests sent to a server and thus eliminates a lot of the waiting time that comes with a server handling a request and sending it back to the client.

The name itself was originally coined by Mathias Biilmann, co-founder at Netlify, who wanted to make it easier to refer to this new way of doing web architecture. 

Table of content
A brief history of developing websites
Why use the Jamstack architecture?
Using Jamstack vs. a traditional CMS for your website
What are the pros and cons of using Jamstack?
Learn how to do Jamstack development
What is a static site generator?
Is Jamstack the future?
Can I use Umbraco for Jamstack websites?
A brief history of developing websites
To understand why the Jamstack architecture is becoming popular today and not 10 years ago, it's worth taking a quick history lesson. In fact, let's take a look at how websites used to work and how it's evolved from there.

In the early days of the internet, everything was simpler than we might think today. The first websites that were built were all just a folder with HTML files that could be requested by a browser. And that was pretty much it. The HTML would determine how the website looked and the content in it, while the browser's only job was to let the user view the page.

As the internet and the technologies surrounding it evolved, it allowed for more advanced websites and as a website owner, you got a lot more possibilities of what you could do. The first real change here was how content was being served. Static HTML files were no longer enough. Instead, it was necessary to serve customized content to the users of a website.

In order to serve customized content, the HTML of the website had to be built by the server at every request. This was a giant leap from serving simple HTML files. Now the user would request a page and instead of having it ready, the server had to consult a database and then build up the right content for this specific user.

 

Omnichannel content delivery animation gif
The benefits were clear: you could now serve more customized content to the user.

The downside? It required more server resources to build, and thus the content would be delivered to the user slower than if it had been an old-school static HTML file.

Unfortunately, there was nothing to do about it at the time. To serve customized content, you had to let your server and database build it. That all changed with the invention and maturity of JavaScript. Today it might be hard to imagine the internet without JavaScript, but that was the case for the first few years before Brendan Eich wrote the first prototype Called "Mocha". It was later renamed "LiveScript", but that only lasted 3 months until JavaScript became the final name.

JavaScript was developed to allow browsers to dynamically alter a page after it was loaded in the browser. This fundamentally changed how developers could work with dynamic behavior in websites, and since all major browsers adopted JavaScript, it became a universal runtime layer. The browser was no longer a simple document viewer but could handle complex tasks that altered how content on a website would look and behave. 

This development added huge benefits to all websites. Not only could they now use JavaScript to add dynamic capabilities to their website after it loaded, but they could also move some of the workloads from the server-side to the client-side. This meant a better user experience for website visitors, and faster delivery as the browser would now help carry some of the load of building the page.
