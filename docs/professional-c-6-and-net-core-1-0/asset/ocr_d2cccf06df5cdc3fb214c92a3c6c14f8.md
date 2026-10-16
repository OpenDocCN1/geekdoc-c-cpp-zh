> NOTE The extension method UseStaticFiles is discussed in Chapter 40. This method requires adding the Microsoft.AspNet.StaticFiles NuGet package.

With this default route, the name of the controller type (without the Controller suffix) and the method name make up the route, such as http://server[:port]/controller/action. You can also use an optional parameter named id, like so: http://server[:port]/controller/action/id. The default name of the controller is Home; the default name of the action method is Index.

The following code snippet shows another way to specify the same default route. The UseMvc method can receive a parameter of type Action<IRouteBuilder>. This IRouteBuilder interface contains a list of routes that are mapped. You define routes using the MapRoute extension method:

```
app.UseMvc(routes => with => routes.MapRoute(
    name:"default",
    template:"{controller}/{action}/{id?}",
    defaults: new {controller ="Home", action ="Index"}
));
```

This route definition is the same as the default one. The template parameter defines the URL; the ? with the id defines that this parameter is optional; the defaults parameter defines the default values for the controller and action part of the URL.

Let’s have a look at this URL:

```
http://localhost:[port]/UseAService/GetSampleStrings
```

With this URL, UseAService maps to the name of the controller, because the Controller suffix is automatically added; the type name is UseAServiceController; and GetSampleStrings is the action, which represents a method in the UseAServiceController type.

# Adding Routes

There are several reasons to add or change routes. For example, you can modify routes to use actions with the link, to define Home as the default controller, to add entries to the link, or to use multiple parameters.

You can define a route where the user can use links—such as http://<server>/About to address the About action method in the Home controller without passing a controller name—as shown in the following snippet. Notice that the controller name is left out from the URL. The controller keyword is mandatory with the route, but you can supply it with the defaults:

```
app.UseMvc(routes => routes.MapRoute(
    name:"default",
    template:"{action}/{id?}",
    defaults: new {controller ="Home", action ="Index"}
```