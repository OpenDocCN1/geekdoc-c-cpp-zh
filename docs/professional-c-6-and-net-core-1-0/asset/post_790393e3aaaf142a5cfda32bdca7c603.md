
Checking the result of the generated HTML code reveals that the `input` type Tag Helpers create a `type` attribute depending on the type of the property, and they also apply the `DataType` attribute. The property `Price` is of type double, which results in a number input type. Because the `Date` property has the `DataType` with a value of `DataType.Date` applied, the input type is a date. In addition to that you can see `data-val-length`, `data-val-length-max`, and `data-val-required` attributes that are created because of annotations:

```
<label for="Text">Menu</label>
<input type="text" data-val="true"
    data-val-length=
        "The field Menu must be a string with a maximum length of 50."
    data-val-length-max="50"
    data-val-required="The Menu field is required."
    id="FileName_Text" name="Text"
    value="Schweinsbraten mit Kn&ouml;del und Sauerkraut" />
<br/>
<label for="Price">Price</label>
<input type="number" data-val="true"
    data-val-required="The Price field is required."
    id="FileName_Price" name="Price" value="6.9" />
<br />
<label for="Date">Date</label>
<input type="date" data-val="true"
    data-val-required="The Date field is required."
    id="FileName_Date" name="Date" value="10/5/2016" />
```

Modern browsers have a special look for HTML 5 input controls such as date control. The input date control of Microsoft Edge is shown in Figure 41.10.

![](img/3d365b72b289213a91ade7eb366b8f35_1604_0.png)

Figure 41.10

## Using a Form with Validation

For sending data to the server, the input fields need to be surrounded by a form. A Tag Helper for the form defines the action attribute by using asp-method and asp-controller. With input controls, you’ve seen that validation information is defined by these controls. The validation errors need to be displayed. For display, the validation message Tag Helper extends the span element with asp-validation-for (code file MVCSampleApp/Views/TagHelpers/FormHelper.cs):

```
<form method="post" asp-method="FormHelper">
    <input asp-for="Id" hidden="hidden" />
    <hr />
    <label asp-for="Text"></label>
    <div>
        <input asp-for="Text" />
        <span asp-validation-for="Text"></span>
    </div>
    <br />
    <label asp-for="Price"></label>
    <div>
        <input asp-for="Price" />
        <span asp-validation-for="Price"></span>
    </div>
    <br />
    <label asp-for="Date"></label>
    <div>
        <input asp-for="Date" />
        <span asp-validation-for="Date"></span>
    </div>
    <label asp-for="Category"></label>
    <div>
        <input asp-for="Category" />
        <span asp-validation-for="Category"></span>
    </div>
    <input type="submit" value="Submit" />
</form>
```

The controller verifies whether the receive data is correct by checking the ModelState. In case it’s not correct, the same view is displayed again (code file MVCSampleApp/Controllers/TagHelpersController.cs):

```
public IActionResult FormHelper() => View(GetSampleMenu());

[HttpPost]
public IActionResult FormHelper(Menu m)
{
    if (!ModelState.IsValid)
    {
        return View(m);
    }
    return View("ValidationHelperResult", m);
}
```

When you run the application, you can see error information like that shown in Figure 41.11.

## ASP.NET MVC Sample App

## Form Helper

Menu
Schweinsbraten mit Knödel
Price
12
Date
7/18/2016
Category
This category is too long The field Category must be a string with a maximum length of 10.
Submit

Sample code for Professional C#
© 2015 - My ASP.NET Application

Figure 41.11

## Creating Custom Tag Helpers

Aside from using the predefined Tag Helpers, you can create a custom Tag Helper. The sample custom Tag Helper you build in this section extends the HTML table element to show a row for every item in a list and a column for every property.

The controller implements the method CustomHelper to return a list of Menu objects (code file MVCSampleApp/Controllers/TagHelpersController.cs):

```
public IActionResult CustomHelper() => View(GetSampleMenus());

private IList<Menu> GetSampleMenus() =>
    new List<Menu>()
    {
        new Menu
        {
            Id = 1,
            Text ="Schweinsbraten mit Kn&ouml;del und Sauerkraut",
            Price = 8.5,
            Date = new DateTime(2016, 10, 5),
            Category ="Main"
        },
        new Menu
        {
            Id = 2,
            Text ="Erd&auml;pfelgulasch mit Tofu und Geb&auml;ck",
            Price = 8.5,
            Date = new DateTime(2016, 10, 6),
            Category ="Vegetarian"
        },
        new Menu
        {
            Id = 3,
            Text ="Tiroler Bauerngr&ouml;st'l mit Spiegelei und Krautsalat",
            Price = 8.5,
            Date = new DateTime(2016, 10, 7),
            Category ="Vegetarian"
        }
    };
```

Now step into the Tag Helper. The custom implementation needs these namespaces:

```
using Microsoft.AspNet.Mvc.Rendering;
using Microsoft.AspNet.Razor.Runtime.TagHelpers;
using System.Collections.Generic;
using System.Linq;
using System.Reflection;
```

A custom Tag Helper derives from the base class TagHelper. The attribute TargetElement defines what HTML elements are extended by the Tag Helper. This Tag Helper extends the table element; thus the string "table" is passed to the constructor of the element. With the property Attributes, you can define a list of attributes that are assigned to the HTML element that are used by the Tag Helper. This Tag Helper makes use of the items attribute. You can use the Tag Helper with this syntax: <table items="Model"></table>, where Model needs to be a list that can be iterated. In case you’re creating a Tag Helper that should be used with multiple HTML elements, you just need to apply the attribute TargetElement multiple times. To automatically assign the value of the items attribute to the Items property, the attribute HtmlAttributeName is assigned to this property (code file MVCSampleApp/Extensions/TableTagHelper.cs):

```
[TargetElement("table", Attributes = ItemsAttributeName)]
public class TableTagHelper : TagHelper
{
    private const string ItemsAttributeName ="items";

    [HtmlAttributeName(ItemsAttributeName)]
    public IEnumerable<object> Items { get; set; }

    // etc.
}
```

The heart of the Tag Helper is in the method Process. This method needs to create HTML code that is returned from the helper. With the parameters of the Process method you receive a TagHelperContext This context contains both the attributes of the HTML element where the Tag Helper is applied and all child elements. With the table element, rows and columns could already have been defined, and you could merge the result with the existing content. In the sample, this is ignored, and just the attributes are taken to put them in the result. The result needs to be written to the second parameter: the TagHelperOutput object. For creating HTML code, the TagBuilder type is used. The TagBuilder helps create HTML elements with attributes, and it deals with closing of elements. To add attributes to the TagBuilder, you use the method MergeAttributes. This method requires a dictionary of all attribute names and their values. This dictionary is created by using the LINQ extension method ToDictionary. With the Where method, all of the existing attributes—with the exception of the items attribute—of the table element are taken. The items attribute is used for defining items with the Tag Helper but is not needed later on by the client:

```
public override void Process(TagHelperContext context,
TagHelperOutput output)
{
    TagBuilder table = new TagBuilder("table");
    table.GenerateId(context.UniqueId,"id");
    var attributes = context.AllAttributes
        .Where(a => a.Name != ItemsAttributeName).ToDictionary(a =>
    a.Name);
    table.MergeAttributes(attributes);
    // etc.
}
```

> **NOTE** *In case you need to invoke asynchronous methods within the Tag Helper implementation, you can override the `ProcessAsync` method instead of the `Process` method.*

> **NOTE** *LINQ is explained in Chapter 13, “Language Integrated Query.”*

Next create the first row in the table. This row contains a tr element as a child of the table element, and it contains td elements for every property. To get all the property names, you invoke the First method to retrieve the first object of the collection. You access the properties of this instance using reflection, invoking the GetProperties method on the Type object, and writing the name of the property to the inner text of the th HTML element:

```
// etc.
var tr = new TagBuilder("tr");
var heading = Items.First();
PropertyInfo[] properties = heading.GetType().GetProperties();
foreach (var prop in properties)
{
    var th = new TagBuilder("th");
    th.InnerHtml.Append(prop.Name);
    th.InnerHtml.AppendHtml(th);
}
table.InnerHtml.AppendHtml(tr);
// etc.
```
