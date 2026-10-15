> Currently, there are no out-of-the-box Web site project templates for ASP.NET MVC.

If you run the application, you will see that a few pages (including the master page) are included as part of the project template (see Figure 23-3). While not exactly the same, the site will be similar in look and feel to one created when you use the non-empty Web Forms project templates.

![](bbox=[0.146, 0.221, 0.703, 0.506])

# Controllers and Actions

In traditional Web application frameworks, requests are mapped to files containing markup for pages. In ASP.NET MVC, requests are mapped to methods on classes. The classes are the previously mentioned controller classes, and the methods are known as actions. Action methods are responsible for receiving user input, retrieving or saving data to the model, and passing control to the appropriate view. The view will typically return the markup for a page but it could also return other content types such as a binary file or JSON formatted data. Typical actions will handle requests to list, add, edit, or delete entities from the model.

Let’s examine these concepts further by creating a new controller. In the Solution Explorer, right-click on the Controllers folder and select Add ➜ Controller. By convention, the names of controller classes should end with “Controller.” The Add Controller dialog even encourages the use of this convention, as shown in Figure 23-4. Set the name to SimpleController and click the Add button.

![](bbox=[0.536, 0.692, 0.932, 0.819])

The class that’s created will inherit from the base Controller class (System.Web.Mvc.Controller) and will have the shell for a default action method named Index:

```
```csharp
Public Class SimpleController
    Inherits System.Web.Mvc.Controller
```
```