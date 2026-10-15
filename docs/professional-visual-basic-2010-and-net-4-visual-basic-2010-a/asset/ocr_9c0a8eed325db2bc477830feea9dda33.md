We’ll look at the Edit action in two parts. The first part involves generating a form that allows editing of product data; the second involves receiving the updated data when the user submits the form.

The Edit action method will have the same implementation as the Details action method. Modify it so that it retrieves the requested product and returns the Details view:

```
' GET: /Admin/Edit/5

Function Edit(ByVal id As Integer) As ActionResult
    Dim product = _repository.GetProduct(id)
    Return View(product)
End Function
```

Code snippet from \Controllers\AdminController.vb

Generate a strongly typed view, selecting Edit from the View content drop-down, as shown in Figure 23-16.

```
<h2>Edit Product</h2>

<script src="../../Scripts/jquery-1.3.2.min.js" type="text/javascript"></script>
<script src="../../Scripts/jquery.validate.min.js" type="text/javascript"></script>
<script src="../../Scripts/MicrosoftMvcJQueryValidation.js" type="text/javascript"></script>

<%= Html.ValidationSummary("Edit was unsuccessful. Please correct the errors ... ") %>
<% Html.EnableClientValidation() %>

<% Using Html.BeginForm() %>

    <fieldset>
        <legend>Fields</legend>
        <p>
            <label for="ProductName">ProductName:</label>
            <%= Html.TextBox("ProductName", Model.ProductName) %>
            <%= Html.ValidationMessage("ProductName", "*") %>
        </p>
        <p>
            <label for="SupplierID">SupplierID:</label>
            <%= Html.TextBox("SupplierID", Model.SupplierID) %>
            <%= Html.ValidationMessage("SupplierID", "*") %>
        </p>
        <!-- Some fields removed for brevity -->
        <p>
            <%= Html.LabelFor(Function(p) p.Discontinued) %>
            <%= Html.EditorFor(Function(p) p.Discontinued) %>
            <%= Html.ValidationMessage("Discontinued", "*") %>
        </p>
        <p>
            <input type="submit" value="Save" />
        </p>
    </fieldset>

<% End Using %>

<div>
    <%=Html.ActionLink("Back to List", "Index") %>
</div>
```

Code snippet from \Views\Admin\Edit.aspx