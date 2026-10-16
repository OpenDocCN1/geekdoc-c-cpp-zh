
RedirectToRouteResult that enables specifying route names, controllers, actions, and parameters. This builds a link that is returned to the client with an HTTP redirect request:

```
public IActionResult RedirectRouteDemo() =>
    RedirectToRoute(new { controller = "Home", action = "Hello" });
```

The File method of the Controller base class defines different overloads that return different types. This method can return FileContentResult, FileStreamResult, and VirtualFileResult. The different return types depend on the parameters used—for example, a string for a VirtualFileResult, a Stream for a FileStreamResult, and a byte array for a FileContentResult.

The next code snippet returns an image. Create an Images folder and add a JPG file. For the next code snippet to work, create an Images folder in the wwwroot directory and add the file Matthias.jpg. The sample code returns a VirtualFileResult that specifies a filename with the first parameter. The second parameter specifies the contentType argument with the MIME type image/jpeg:

```
public IActionResult FileDemo() =>
    File("~/images/Matthias.jpg", "image/jpeg");
```

The next section shows how to return different ViewResult variants.

## Working with the Controller Base Class and POCO Controllers

So far, all the controllers created have been derived from the base class Controller. ASP.NET MVC 6 also supports controllers—known as POCO (Plain Old CLR Objects) controllers—that do not derive from this base class. This way you can use your own base class to define your own type hierarchy with controllers.

What do you get out of the Controller base class? With this base class, the controller can directly access properties of the base class. The following table describes these properties and their functionality.

| Property | Description |
|---|---|
| ActionContext | This property wraps some other properties. Here you can get information about the action descriptor, which contains the name of the action, controller, filters, and method information; the HttpContext, which is directly accessible from the Context property; the state of the model that is directly accessible from the ModelState property, and route information that is directly accessible from the RouteData property. |
| Context | This property returns the HttpContext. With this context you can access the ServiceProvider to share information between views and controllers within a single request. By default, TempData writes information to the session state. |
| User | The User property returns information, including identity and claims, about an authenticated user. |

A POCO controller doesn’t have the Controller base class, but it’s still important to access such information. The following code snippet defines a POCO controller that derives from the object base class (you can use your own custom type as a base class). To create an ActionContext with the POCO class, you can create a property of this type. The POCOController class uses ActionContext as the name of this property, similar to the way the Controller class does. However, just having a property doesn’t set it automatically. You need to apply the ActionContext attribute. Using this attribute injects the actual ActionContext. The Context property directly accesses the HttpContext property from the ActionContext. The Context property is used from the UserAgentInfo action method to access and return the User-Agent header information from the request (code file MVCSampleApp/Controllers/POCOController.cs):

```
public class POCOController
{
    public string Index() =>
        "this is a POCO controller";

    [ActionContext]
    public ActionContext ActionContext { get; set; }
    public HttpContext Context => ActionContext.HttpContext;
    public ModelStateDictionary ModelState =>
        ActionContext.ModelState;

    public string UserAgentInfo()
    {
        if (Context.Request.Headers.ContainsKey("User-Agent"))
        {
            return Context.Request.Headers["User-Agent"];
        }
        return "No user-agent information";
    }
}
```

## Creating Views

The HTML code that is returned to the client is best specified with a view. For the samples in this section, the ViewsDemoController is created. The views are all defined within the Views folder. The views for the ViewsDemo controller need a ViewsDemo subdirectory. This is a convention for the views (code file MVCSampleApp/Controllers/ViewsDemoController.cs):

```
public ActionResult Index() => View();
```

> **NOTE** Another place where views are searched is the `Shared` directory. You can put views that should be used by multiple controllers (and special partial views used by multiple views) into the `Shared` directory.

After creating the `ViewsDemo` directory within the `Views` directory, the view can be created using Add, New Item and selecting the MVC View Page item template. Because the action method has the name `Index`, the view file is named `Index.cshtml`.

The action method `Index` uses the `View` method without parameters, and thus the view engine searches for a view file with the same name as the action name in the `ViewsDemo` directory. The `View` method used in the controller has overloads that enable passing a different view name. In that case, the view engine looks for a view with the name passed to the `View` method.

A view contains HTML code mixed with a little server-side code, as shown in the following snippet (code file `MVCSampleApp/Views/ViewsDemo/Index.cshtml`):

```cshtml
@{
    Layout = null;
}
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Index</title>
</head>

<body>
    <div>
    </div>
</body>
</html>
```

Server-side code is written using the @ sign, which starts the Razor syntax, which is discussed later in this chapter. Before getting into the details of the Razor syntax, the next section shows how to pass data from a controller to a view.

## Passing Data to Views

The controller and view run in the same process. The view is directly created from within the controller. This makes it easy to pass data from the controller to the view. To pass data, you can use a `ViewDataDictionary`. This dictionary stores keys as strings and enables object values. You can use the `ViewDataDictionary` with the `ViewData` property of the `Controller` class—for example, you can pass a string to the dictionary where the key value `MyData` is used: `ViewData["MyData"] = "Hello"`. An easier syntax uses the `ViewBag` property. `ViewBag` is a dynamic type that enables assigning any property name to pass data to the view (code file MVCSampleApp/Controllers/SubmitDataController.cs):

```
public IActionResult PassingData()
{
    ViewBag.MyData = "Hello from the controller";
    return View();
}
```

> **NOTE** Using dynamic types has the advantage that there is no direct dependency from the view to the controller. Dynamic types are explained in detail in Chapter 16, “Reflection, Metadata, and Dynamic Programming.”

From within the view, you can access the data passed from the controller in a similar way as in the controller. The base class of the view (WebViewPage) defines a ViewBag property (code file MVCSampleApp/Views/ViewsDemo/PassingData.cshtml):

```
<div>
    <div>@ViewBag.MyData</div>
</div>
```

## Understanding Razor Syntax

As discussed earlier when you were introduced to views, the view contains both HTML and server-side code. With ASP.NET MVC you can use Razor syntax to write C# code in the view. Razor uses the @ character as a transition character. Starting with @, C# code begins.

With Razor you need to differentiate statements that return a value and methods that don’t. A value that is returned can be used directly. For example, ViewBag.MyData returns a string. The string is put directly between the HTML div tags as shown here:

```
<div>@ViewBag.MyData</div>
```

When you’re invoking methods that return void, or specifying some other statements that don’t return a value, you need a Razor code block. The following code block defines a string variable:

```
@{
    string name = "Angela";
}
```

You can now use the variable with the simple syntax; you just use the transition character @ to access the variable:

```
<div>@name</div>
```

With the Razor syntax, the engine automatically detects the end of the C# code when it finds an HTML element. There are some cases in which the end of the C# code cannot be detected automatically. You can resolve this by using parentheses as shown in the following example to
