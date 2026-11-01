```
[AcceptVerbs(HttpVerbs.Post)]
public ActionResult Create(FormCollection collection)
{
    try
    {
        // TODO: Add insert logic here

        return RedirectToAction("Index");
    }
    catch
    {
        return View();
    }
}
```

code snippet PCSMVC MagicShop/Controllers/ProductsController.cs

The first of these, which has no parameters, simply redirects to the create view, which you can add in the same way as other views (remembering the View content value to Create in the Add View Wizard). The second is used to actually create a new item in the data source, and you have to implement it yourself.

Note that the second Create() overload includes an AcceptVerbs attribute. This restricts the HTTP verb used to POST, which makes sense as you will typically want to submit more information when creating an item than you could reasonably include in a URL for a GET request.

The view that you created for the first Create() method includes the following auto-generated code:

```
<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" runat="server">
<h2>
Create</h2>
<%= Html.ValidationSummary(
"Create was unsuccessful. Please correct the errors and try again.") %>
<%= Html.BeginForm() %>
({
<fieldset>
<legend>Fields</legend>
<p>
<label for="ProductId">
ProductId:</label>
<%= Html.TextBox("ProductId") %>
<%= Html.ValidationMessage("ProductId", "*") %>
</p>
<p>
<label for="Name">
Name:</label>
<%= Html.TextBox("Name") %>
<%= Html.ValidationMessage("Name", "*") %>
</p>
<p>
<label for="Description">
Description:</label>
<%= Html.TextBox("Description") %>
<%= Html.ValidationMessage("Description", "**") %>
</p>
<p>
<label for="Cost">
Cost:</label>
<%= Html.TextBox("Cost") %>
<%= Html.ValidationMessage("Cost", "*") %>
</p>
```