
```
@{
    ViewBag.Title = "View Components Sample";
}
```

## View Components Sample

```
@await Component.InvokeAsync("EventList", new DateTime(2016, 4, 10), new DateTime(2016, 4, 24))
```

Running the application, you can see the view component rendered as shown in Figure 41.6.

![](img/3d365b72b289213a91ade7eb366b8f35_1589_0.png)

## Using Dependency Injection in Views

In case a service is needed directly from within a view, you can inject it using the inject keyword:

```
@using MVCSampleApp.Services
@inject ISampleService sampleService
<p>@string.Join("*", sampleService.GetSampleStrings())</p>
```

When you do this, it's a good idea to register services using the AddScoped method. As previously mentioned, registering a service that way means it's only instantiated once for one HTTP request. Using AddScoped, injecting the same service within a controller and the view, it is only instantiated once for a request.

## Importing Namespaces with Multiple Views

All the previous samples for views have used the using keyword to open all the namespaces needed. Instead of opening the namespaces with every view, you can use the Visual Studio item template MVC View Imports Page to create a file (_ViewImports.cshtml) that defines all using declarations (code file MVCSampleApp/Views/_ViewImports.cshtml):

```
@using MVCSampleApp.Models
@using MVCSampleApp.Services
```

With this file in place, there’s no need to add all the using keywords to all the views.

## Submitting Data from the Client

Until now you used only HTTP GET requests from the client to retrieve HTML code from the server. What about sending form data from the client?

To submit form data, you create the view CreateMenu for the controller SubmitData. This view contains an HTML form element that defines what data should be sent to the server. The form method is declared as an HTTP POST request. The input elements that define the input fields all have names that correspond to the properties of the Menu type (code file MVCSampleApp/Views/SubmitData/CreateMenu.cshtml):

```
@{
    ViewBag.Title ="Create Menu";
}
<h2>Create Menu</h2>
<form action="/SubmitData/CreateMenu" method="post">
<fieldset>
    <legend>Menu</legend>
    <div>Id:</div>
    <input name="id"  />
    <div>Text:</div>
    <input name="text"  />
    <div>Price:</div>
    <input name="price"  />
    <div>Category:</div>
    <input name="category"  />
    <div></div>
    <button type="submit">Submit</button>
</fieldset>
</form>
```

Figure 41.7 shows the opened page within the browser.

ASP.NET MVC Sample App

Create Menu

Menu

Id:

Text:

Price:

Category:

Submit

*Figure 41.7*

Within the SubmitData controller, two CreateMenu action methods are created: one for an HTTP GET request and another for an HTTP POST request. Because C# has different methods with the same name, it’s required that the parameter numbers or types are different. Of course, this requirement is the same with action methods. Action methods also need to differ with the HTTP request method. By default, the request method is GET; when you apply the attribute HttpPost, the request method is POST. For reading HTTP POST data, you could use information from the Request object. However, it’s much simpler to define the CreateMenu method with parameters. The parameters are matched with the name of the form fields (code file MVCSampleApp/Controllers/SubmitDataController.cs):

```
public IActionResult Index() => View();

public IActionResult CreateMenu() => View();

[HttpPost]
public IActionResult CreateMenu(int id, string text, double price,
    string category)
{
    var m = new Menu { Id = id, Text = text, Price = price };
    ViewBag.Info =
        $"menu created: {m.Text}, Price: {m.Price}, category: {m.Category}";
    return View("Index");
}
```

To display the result, just the value of the ViewBag.Info is shown (code file MVCSampleApp/Views/SubmitData/Index.cshtml):

```
@ViewBag.Info
```

### Model Binder

Instead of using multiple parameters with the action method, you can also use a type that contains properties that match the incoming field names (code file MVCSampleApp/Controllers/SubmitDataController.cs):

```
[HttpPost]
public IActionResult CreateMenu2(Menu m)
{
    ViewBag.Info =
        $"menu created: {m.Text}, Price: {m.Price}, category: {m.Category}";
    return View("Index");
}
```

When the user submits the data with the form, a CreateMenu method is invoked that shows the Index view with the submitted menu data, as shown in Figure 41.8.

![](img/3d365b72b289213a91ade7eb366b8f35_1592_0.png)

*Figure 41.8*

A model binder is responsible for transferring the data from the HTTP POST request. A model binder implements the interface IModelBinder. By default the FormCollectionModelBinder class is used to bind the input fields to the model. This binder supports primitive types, model classes (such as the Menu type), and collections implementing ICollection<T>, IList<T>, and IDictionary<TKey, TValue>.

In case not all the properties of the parameter type should be filled from the model binder, you can use the Bind attribute. With this attribute you can specify a list of property names that should be included with the binding.

You can also pass the input data to the model using an action method without parameters, as demonstrated by the next code snippet. Here, a new instance of the Menu class is created, and this instance is passed to the TryUpdateModelAsync method of the Controller base class.

TryUpdateModelAsync returns false if the updated model is not in a valid state after the update:

```
[HttpPost]
public async Task<IActionResult> CreateMenu3Result() 
{
  var m = new Menu();
  bool updated = await TryUpdateModelAsync<Menu>(m);
  if (updated)
  {
    ViewBag.Info = 
      $"menu created: {m.Text}, Price: {m.Price}, category: {m.Category}";
    return View("Index");
  }
  else
  {
    return View("Error");
  }
}
```

### Annotations and Validation

You can add some annotations to the model type; the annotations are used when updating the data for validation. The namespace System.ComponentModel.DataAnnotations contains attribute types that can be used to specify some information for data on the client and can be used for validation.

The Menu type is changed with these added attributes (code file MVCSampleApp/Models/Menu.cs):

```
public class Menu
{
  public int Id { get; set; }
  [Required, StringLength(50)]
  public string Text { get; set; }
  [Display(Name="Price"), DisplayFormat(DataFormatString="{0:C}")]
  public double Price { get; set; }
  [DataType(DataType.Date)]
  public DateTime Date { get; set; }
  [StringLength(10)]
  public string Category { get; set; }
}
```

Possible attribute types you can use for validation are CompareAttribute to compare different properties, CreditCardAttribute to verify a valid credit card number, EmailAddressAttribute to verify an e-mail address, EnumDataTypeAttribute to compare the input to enumeration values, and PhoneAttribute to verify a phone number.

You can also use other attributes to get values for display and error messages—for example, DataTypeAttribute and DisplayFormatAttribute.

To use the validation attributes, you can verify the state of the model using ModelState.IsValid within an action method as shown here (code file MVCSampleApp/Controllers/SubmitDataController.cs):

```
[HttpPost]
public IActionResult CreateMenu4(Menu m)
{
    if (ModelState.IsValid)
    {
        ViewBag.Info =
            $"menu created: {m.Text}, Price: {m.Price}, category: {m.Category}";
    }
    else
    {
        ViewBag.Info ="not valid";
    }
    return View("Index");
}
```

If you use tool-generated model classes, you might think it’s hard to add attributes to properties. As the tool-generated classes are defined as partial classes, you can extend the class by adding properties and methods, by implementing additional interfaces, and by implementing partial methods that are used by the tool-generated classes. You cannot add attributes to existing properties and methods if you can’t change the source code of the type, but there’s help for such scenarios! Assume the Menu class is a tool-generated partial class. Then a new class with a different name (for example, MenuMetadata) can define the same properties as the entity class and add the annotations, as shown here:

```
public class MenuMetadata
{
    public int Id { get; set; }
    [Required, StringLength(25)]
    public string Text { get; set; }
    [Display(Name="Price"), DisplayFormat(DataFormatString="{0:C}")]
    public double Price { get; set; }
    [DataType(DataType.Date)]
    public DateTime Date { get; set; }
    [StringLength(10)]
    public string Category { get; set; }
}
```

The MenuMetadata class must be linked to the Menu class. With tool-generated partial classes, you can create another partial type in the same namespace to add the MetadataType attribute to the type definition that creates the connection:

```
[MetadataType(typeof(MenuMetadata))]
public partial class Menu
{
}
```

HTML Helper methods can also make use of annotations to add information to the client.

## Working with HTML Helpers

HTML Helpers are helpers that create HTML code. You can use them directly within the view using Razor syntax.
