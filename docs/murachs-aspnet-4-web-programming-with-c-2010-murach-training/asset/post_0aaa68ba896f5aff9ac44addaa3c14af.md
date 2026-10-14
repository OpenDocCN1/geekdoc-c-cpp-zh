
## The Default.aspx file

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
    ConflictDetection="CompareAllValues"
    ConnectionString="<%= ConnectionStrings:HalloweenConnectionString %>"
    OldValuesParameterFormatString="original_{0}"
    SelectCommand="SELECT [CategoryID], [ShortName], [LongName] FROM [Categories]"
    DeleteCommand="DELETE FROM [Categories] WHERE [CategoryID] = @original_CategoryID AND [ShortName] = @original_ShortName AND [LongName] = @original_LongName"
    InsertCommand="INSERT INTO [Categories] ([CategoryID], [ShortName], [LongName]) VALUES (@CategoryID, @ShortName, @LongName)"
    UpdateCommand="UPDATE [Categories] SET [ShortName] = @ShortName, [LongName] = @LongName WHERE [CategoryID] = @original_CategoryID AND [ShortName] = @original_ShortName AND [LongName] = @original_LongName">
    <DeleteParameters>
        <asp:Parameter Name="original_CategoryID" Type="String" />
        <asp:Parameter Name="original_ShortName" Type="String" />
        <asp:Parameter Name="original_LongName" Type="String" />
    </DeleteParameters>
    <InsertParameters>
        <asp:Parameter Name="CategoryID" Type="String" />
        <asp:Parameter Name="ShortName" Type="String" />
        <asp:Parameter Name="LongName" Type="String" />
    </InsertParameters>
    <UpdateParameters>
        <asp:Parameter Name="ShortName" Type="String" />
        <asp:Parameter Name="LongName" Type="String" />
        <asp:Parameter Name="original_CategoryID" Type="String" />
        <asp:Parameter Name="original_ShortName" Type="String" />
        <asp:Parameter Name="original_LongName" Type="String" />
    </UpdateParameters>
</asp:SqlDataSource>
```

## Notes

- The Select statement retrieves all rows in the Categories table.
- The Where clauses in the Delete and Update statements provide for optimistic concurrency.

```
<p id="new">To create a new category, enter the category information and click Add New Category.</p>
<p>
<asp:Label ID="lblError" runat="server" EnableViewState="False" CssClass="error">
</asp:Label>
</p>
<p class="label">ID:</p>
<p class="entry">
<asp:TextBox ID="txtID" runat="server" Width="100" MaxLength="10">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" ControlToValidate="txtID" CssClass="error" ErrorMessage="ID is a required field.">
</asp:RequiredFieldValidator>
</p>
<p class="label">Short Name:</p>
<p class="entry">
<asp:TextBox ID="txtShortName" runat="server" Width="200" MaxLength="15">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" ControlToValidate="txtShortName" CssClass="error" ErrorMessage="Short Name is a required field.">
</asp:RequiredFieldValidator>
</p>
<p class="label">Long Name:</p>
<p class="entry">
<asp:TextBox ID="txtLongName" runat="server" Width="200" MaxLength="50">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator3" runat="server" ControlToValidate="txtLongName" CssClass="error" ErrorMessage="Long Name is a required field.">
</asp:RequiredFieldValidator>
</p>
<p>
<asp:Button ID="btnAdd" runat="server" Text="Add New Category" OnClick="btnAdd_Click" />
</p>
</div>
</div>
</form>
</body>
</html>
```

## Notes

- The text boxes are used to enter data for a new row.
- The required field validators ensure that the user enters data for each column of a new row.

## The code-behind file

Although it would be nice if you could create a robust database application without writing any C# code, you must still write code to insert data into a GridView control and to catch and handle any database or concurrency errors that might occur. Figure 14-14 shows this code for the Category Maintenance application.

As you can see, this code-behind file consists of just three methods. The first, btnAdd_Click, sets the values of the three insert parameters to the values entered by the user. Then, it calls the Insert method of the data source control. If an exception is thrown, an appropriate error message is displayed.

The second method, GridView1_RowUpdated, is called after a row has been updated. This method checks the Exception property of the e argument to determine if an exception has been thrown. If so, an error message is displayed, the ExceptionHandled property is set to True to suppress the exception, and the KeepInEditMode property is set to True to leave the GridView control in edit mode. If an exception hasn’t occurred, the e argument’s AffectedRows property is checked. If it’s zero, it means that a concurrency error has occurred and an appropriate message is displayed.

The third method, GridView1_RowDeleted, is called after a row has been deleted. Like the method that’s called after a row is updated, this method checks if an exception has been thrown or if a concurrency error has occurred. The only difference is that this method doesn’t set the KeepInEditMode property to True, since the control isn’t in edit mode when the Delete button is clicked.

## The Default.aspx.cs file

```
public partial class _Default : System.Web.UI.Page
{
    protected void btnAdd_Click(object sender, EventArgs e)
    {
        SqlDataSource1.InsertParameters["CategoryID"].DefaultValue
            = txtID.Text;
        SqlDataSource1.InsertParameters["ShortName"].DefaultValue
            = txtShortName.Text;
        SqlDataSource1.InsertParameters["LongName"].DefaultValue
            = txtLongName.Text;
        try
        {
            SqlDataSource1.Insert();
            txtID.Text = "";
            txtShortName.Text = "";
            txtLongName.Text = "";
        }
        catch (Exception ex)
        {
            lblError.Text = "A database error has occurred.<br /><br />" +
                "Message: " + ex.Message;
        }
    }

    protected void GridView1_RowUpdated(object sender,
        GridViewUpdatedEventArgs e)
    {
        if (e.Exception != null)
        {
            lblError.Text = "A database error has occurred.<br /><br />" +
                "Message: " + e.Exception.Message;
            e.ExceptionHandled = true;
            e.KeepInEditMode = true;
        }
        else if (e.AffectedRows == 0)
        {
            lblError.Text = "Another user may have updated that category." +
                "<br />Please try again.";
        }
    }

    protected void GridView1_RowDeleted(object sender,
        GridViewDeletedEventArgs e)
    {
        if (e.Exception != null)
        {
            lblError.Text = "A database error has occurred.<br /><br />" +
                "Message: " + e.Exception.Message;
            e.ExceptionHandled = true;
        }
        else if (e.AffectedRows == 0)
        {
            lblError.Text = "Another user may have updated that category." +
                "<br />Please try again.";
        }
    }
}
```

## How to work with template fields

Although using bound fields is a convenient way to include bound data in a GridView control, the most flexible way is to use template fields. A template field is simply a field that provides one or more templates that are used to render the column. You can include anything you want in these templates, including labels or text boxes, data binding expressions, and validation controls. In fact, including validation controls for editable GridView controls is one of the main reasons for using template fields.

## How to create template fields

Figure 14-15 shows how to create template fields. The easiest way to do that is to first create a regular bound field and then convert it to a template field. This changes the BoundField element to a TemplateField element and, more importantly, generates ItemTemplate and EditItemTemplate elements that include labels and text boxes with appropriate binding expressions. In particular, each EditItemTemplate element includes a text box that uses the Bind method to implement two-way binding (please see figure 13-15 for more information about this method).

Once you’ve converted the bound field to a template, you can edit the template to add any additional elements you want to include, such as validation controls. In the code example in this figure, you can see that I added a RequiredFieldValidator control to the EditItem template for the ShortName column. That way, the user must enter data into the txtGridShortName text box. I also changed the names of the label and the text box that were generated for the Item and EditItem templates from their defaults (Label1 and TextBox1) to lblGridShortName and txtGridShortName.

You can also edit the templates from Design view. To do that, you use the same basic techniques that you use to work with the templates for a DataList control. The main difference is that each bound column in a GridView control has its own templates. In this figure, for example, you can see the EditItem template for the ShortName column.

Although a text box is included in the EditItem template for a column by default, you should know that you can use other types of controls too. For example, you can use a check box to work with a Boolean column, and you can use a Calendar control to work with a date column. You can also use a drop-down list that lets the user select a value from the list. To do that, you must create a separate data source that retrieves the data for the list. Then, you can bind the drop-down list to this data source by setting the DataTextField and DataValueField attributes as shown in the last chapter, and you can bind the drop-down list to a column in the GridView’s data source by setting its SelectedValue attribute using the DataBindings dialog box you saw in the last chapter.
