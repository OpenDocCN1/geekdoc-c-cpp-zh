```
}
}
}
```

The Index action method returns a ViewResult , indicating that it will render a view.

# Creating the Corresponding View

Now, let's create the view that will be rendered by the Index action method:

+   1. Right-click on the Views folder and create a new folder named Home .
+   2. Right-click on the Home folder and select "Add" -> "View...".
+   3. Name the view Index and select the "Empty (without model)" template.
+   4. Click "Add."

This will create a new Razor view file named Index.cshtml within the Views/Home folder.

# Adding Content to the View

Let's add some basic content to the Index.cshtml view:

```
Razor CSHTML
@{
    ViewData["Title"] = "Home Page";
}

<h1>Welcome to My First Web Application!</h1>
<p>This is the home page of your application.</p>
```