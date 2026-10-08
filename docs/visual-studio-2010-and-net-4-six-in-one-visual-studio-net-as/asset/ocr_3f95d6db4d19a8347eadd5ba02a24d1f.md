IgnoreRoute and MapRoute extension methods for the RouteCollection class and provided by the MVC framework. Figure 18-10 show how an HTTP request is forwarded to the responsible entity for processing it after the request is sent from a client's browser through the routing component.

The first point within IIS for the request is the UrlRoutingModule provided by ASP.NET. Its task is to format the request to the UrlRoutingHandler. The UrlRoutingHandler checks the incoming URL within its RouteCollection, and if a match is found, it forwards the request to the appropriate handler.

![](bbox=[0.505, 0.108, 0.865, 0.38])

The IgnoreRoute method creates a route associated with the StopRoutingHandler, which means ASP.NET stops processing URL and forwards it to the other handlers registered with IIS.

The MapRoute method creates a route associated with the MvcHandler, which is the first real entry point to an MVC application. From this point, you can use a RequestContext to instance all the data required to fulfill the request. RequestContext contains the current HttpContext and the matched RouteData.

Now, with this short explanation, you can how the menu links in the HTML representation of AcmeLibrary's Home and About menu items work:

```
<ul id="menu">
  <li><a href="/">Home</a></li>
  <li><a href="/Home/About">About</a></li>
</ul>
```

When the request is for "/ (for example, the URL is "http://AcmeLibrary.com/"), no controller and no action name is provided, the default "Home" controller is used with the default "Index" action. The ControllerFactory component shown in Figure 18-9 resolves the "Home" name to the HomeController class, and the ActionInvoker component resolves the "Index" name to the Index public method.

When the request is for "/Home/About" (for example, the URL is "http://AcmeLibrary.com/Home/About\ the "Home" controller is used with the "About" action that is mapped to the About public method of the HomeController class.