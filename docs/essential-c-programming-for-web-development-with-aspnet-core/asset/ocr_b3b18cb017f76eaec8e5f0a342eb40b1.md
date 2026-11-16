The ViewData["Title"] line sets the title of the page, which can be used in the layout or displayed in the browser's title bar.

# Running the Application

Now, let's run your application and navigate to the root URL (/). You should see the "Welcome to My First Web Application!" message rendered in your browser, indicating that the HomeController's Index action method successfully rendered the Index.cshtml view.

# Passing Data to the View

Controllers can pass data to views using the ViewData dictionary or by strongly typing the view model. Let's modify the Index action method to pass a message to the view:

```
C#

public IActionResult Index()
{
    ViewData["Message"] = "Hello from the controller!";
    return View();
}
```

And update the Index.cshtml view to display the message:

```
Razor CSHTML

<h1>Welcome to My First Web Application!</h1>
<p>This is the home page of your application.</p>
<p>@ViewData["Message"]</p>
```