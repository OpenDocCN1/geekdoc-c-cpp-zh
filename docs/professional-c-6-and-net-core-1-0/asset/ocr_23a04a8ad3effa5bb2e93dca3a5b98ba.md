dynamic type that enables assigning any property name to pass data to the view (code file MVCSampleApp/Controllers/SubmitDataController.cs):

```
public IActionResult PassingData()
{
    ViewBag.MyData ="Hello from the controller";
    return View();
}
```

> NOTE Using dynamic types has the advantage that there is no direct dependency from the view to the controller. Dynamic types are explained in detail in Chapter 16, “Reflection, Metadata, and Dynamic Programming.”

From within the view, you can access the data passed from the controller in a similar way as in the controller. The base class of the view (WebViewPage) defines a ViewBag property (code file MVCSampleApp/Views/ViewsDemo/PassingData.cshtml):

```
<div>
    <div>@ViewBag.MyData</div>
</div>
```

# Understanding Razor Syntax

As discussed earlier when you were introduced to views, the view contains both HTML and server-side code. With ASP.NET MVC you can use Razor syntax to write C# code in the view. Razor uses the @ character as a transition character. Starting with @, C# code begins.

With Razor you need to differentiate statements that return a value and methods that don’t. A value that is returned can be used directly. For example, ViewBag.MyData returns a string. The string is put directly between the HTML div tags as shown here:

```
<div>@ViewBag.MyData</div>
```

When you’re invoking methods that return void, or specifying some other statements that don’t return a value, you need a Razor code block. The following code block defines a string variable:

```
@{
    string name ="Angela";
}
```

You can now use the variable with the simple syntax; you just use the transition character @ to access the variable:

```
<div>@name</div>
```

With the Razor syntax, the engine automatically detects the end of the C# code when it finds an HTML element. There are some cases in which the end of the C# code cannot be detected automatically. You can resolve this by using parentheses as shown in the following example to