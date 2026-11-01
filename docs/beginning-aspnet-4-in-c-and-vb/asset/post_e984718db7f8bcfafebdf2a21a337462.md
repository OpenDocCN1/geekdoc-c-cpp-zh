
```
<p>
<input type="submit" value="Create" />
</p>
</fieldset>
<div>
<%= Html.ActionLink("Back to List", "Index") %>
</div>
</asp:Content>
```

code snippet PCSMVC MagicShop/Views/Products/Create.aspx

Several helper methods are included here to create and edit the form, and again you can see how the data model has been interrogated to extract information for the fields to use and the validation required. The form itself is contained in the following code block:

```
using (Html.BeginForm())
{
    ...
}
```

This helper method creates a form that is submitted using a standard HTML <input type="submit" /> control, which results in the form values being passed to the action method. You then have access to these values so that you can add a new item.

You can delete the following section of code to remove the text box for the product ID, since this is auto-generated:

```
<p>
<label for="ProductId">
ProductId:</label>
<%= Html.TextBox("ProductId") %>
<%= Html.ValidationMessage("ProductId", "**") %>
</p>
```

The code required to add an item is as follows:

```
[AcceptVerbs(HttpVerbs.Post)]
public ActionResult Create([Bind(Exclude = "ProductId")] Product productToCreate)
{
    try
    {
        if (!ModelState.IsValid)
        {
            return View();
        }
        entities.AddToProducts(productToCreate);
        entities.SaveChanges();
        return RedirectToAction("Index");
    }
    catch
    {
        return View();
    }
}
```

code snippet PCSMVC MagicShop/Controllers/ProductsController.cs

There are several points to note about this code. First, note that you can change the method signature to accept a strongly-typed Product value. This is easier than working through a collection of form values, but to facilitate it you need to exclude the ProductId field, since it won't be passed. The Bind attribute achieves this.

```
```csharp
using System.ComponentModel.DataAnnotations;

namespace PCSMVCMagicShop.Models
{
    public class ProductMetadata
    {
        [StringLength(20)]
        public object Name { get; set; }
    }
}
```
```

This will validate the data, as shown in Figure 42-16.

Obviously the code you need to use in the controller comes down to the model you are using, but which may not always be available, but it can be very useful in the right circumstances.

You will also probably want to edit the view created to provide more meaningful text, but the skeleton created is suitable for most needs. In this example, you’d probably want to change the form’s title and validation messages, as well as providing a bit more space for the item description.

![](img/d7d2ffa0a76feaab821930e95daace93_1334_0.png)

## Editing Items with Edit()

Editing items uses very similar code to creating new items. Rather than working through how to do this, let’s just take a look at the code in the controller:

```
```csharp
public ActionResult Edit(int id)
{
    var productToEdit = (from p in entities.Products
                         where p.ProductId == id
                         select p).First();

    return View(productToEdit);
}

[AcceptVerbs(HttpVerbs.Post)]
public ActionResult Edit(Product productToEdit)
{
    try
    {
        var originalProduct = (from p in entities.Products
                               where p.ProductID == productToEdit.ProductId
                               select p).First();

        if (!ModelState.IsValid)
        {
            return View(originalProduct);
        }

        entities.ApplyCurrentValues(originalProduct.EntityKey, EntitySetName,
                                    productToEdit);
        entities.SaveChanges();

        return RedirectToAction("Index");
    }
    catch
    {
        return View();
    }
}
```
```

*code snippet PCSMVC MagicShop/Controllers/ProductsController.cs*

This time, both `Edit()` method overloads need implementing. The first obtains a Product item from an ID value, and the second updates an item, using standard ADO.NET Entity Framework code.

Note that this time you require the product ID in the second Edit() overload, so you can’t just remove the auto-generated HTML for the ProductId field in the edit view as you did in the details and create views. Instead, to prevent it from being edited, you can include it as a hidden field as follows:

```
```html
<fieldset>
    <legend>Fields</legend>
    <%= Html.Hidden("ProductId", Model.ProductId) %>
```
```

*code snippet PCSMVC MagicShop/Views/Products/Edit.aspx*

This ensures that it will be passed to the action method correctly.

## Further Development

As with dynamic data web sites, this chapter has only included a brief introduction to ASP.NET MVC. There is plenty more that is worth looking into, including:

- Adding your own actions
- Custom action return types
- Unit testing controller
- Custom HTML helper methods

And much more. If you are interested in learning more, your first point of call should be the ASP.NET MVC web site at http://asp.net/mvc, which contains tutorials, samples, and everything you need to dig deeper into this exciting new technology. There are also plenty of other great resources on the internet, including Scott Guthrie’s blog at http://weblogs.asp.net/scottgu/. Scott has also written a great book for Wrox, *Professional ASP.NET MVC 1.0* (ISBN: 0470348611), with fellow expert ASP.NET MVC authors Rob Conery, Scott Hanselman, and Phil Haack. While this only covers version 1.0 of ASP.NET MVC, it is well worth a look, and I expect an updated version for ASP.NET MVC 2 before too long.

## SUMMARY

In this chapter, you have completed your grand tour of ASP.NET by looking at some of the latest additions to the language and tools built on the framework that make it such an exciting way to develop for the web.

You started by looking at how routing can make friendly URLs much easier to implement, and how to control that routing to tweak URL mapping in exactly the way you want.

Next, you saw how to create dynamic data web sites that provide seamless integration of your data with a powerful front-end ASP.NET UI. This technology provides so much code for you by default that at times it feels like your web sites write themselves. You saw how two different data access methodologies, LINQ to SQL and the ADO.NET Entity Framework, are both supported by dynamic data sites, and how to customize scaffolding to make sites work just the way you want.

- Hosting for components and services — Just as you can use custom hosts with .NET Remoting and Web Service Enhancements (WSE), you can host a WCF service in the ASP.NET runtime, a Windows service, a COM+ process, or just a Windows Forms application for peer-to-peer computing.
- Declarative behavior — Instead of the requirement to derive from a base class (this requirement exists with .NET Remoting and Enterprise Services), attributes can be used to define the services. This is similar to Web services developed with ASP.NET.
- Communication channels — Although .NET Remoting is very flexible for changing the communication channel, WCF is a good alternative because it offers the same flexibility. WCF offers multiple channels to communicate using HTTP, TCP, or an IPC channel. Custom channels using different transport protocols can be created as well.
- Security infrastructure — For implementing platform-independent Web services, a standardized security environment must be used. The proposed standards are implemented with WSE 3.0, and this continues with WCF.
- Extensibility — .NET Remoting has a rich extensibility story. It is not only possible to create custom channels, formatters, and proxies, but also to inject functionality inside the message flow on the client and on the server. WCF offers similar extensibilities; however, here the extensions are created by using SOAP headers.
- Support of previous technologies — Instead of rewriting a distributed solution completely to use WCF, WCF can be integrated with existing technologies. WCF offers a channel that can communicate with serviced components using DCOM. Web services that have been developed with ASP.NET can be integrated with WCF as well.

The final goal is to send and receive messages between a client and a service across processes or different systems, across a local network, or across the Internet. This should be done, if required, in a platform-independent way and as fast as possible. From a distant view, the service offers an endpoint that is described by a contract, binding, and an address. The contract defines the operations offered by the service, binding gives information about the protocol and encoding, and the address is the location of the service. The client needs a compatible endpoint to access the service.

Figure 43-1 shows the components that participate with a WCF communication.

![](img/d7d2ffa0a76feaab821930e95daace93_1341_0.png)

The client invokes a method on the proxy. The proxy offers methods as defined by the service but converts the method call to a message and transfers the message to the channel. The channel has a client-side part and a server-side part that communicate across a networking protocol. From the channel, the message is passed to the dispatcher, which converts the message to a method call that is invoked with the service.

WCF supports several communication protocols. For platform-independent communication, Web services standards are supported. For communication between .NET applications, faster communication protocols with less overhead can be used.

The following sections look at the functionality of core services used for platform-independent communication:

- SOAP — a platform-independent protocol that is the foundation of several Web service specifications to support security, transactions, reliability
- WSDL (Web Services Description Language) — offers metadata to describe a service
