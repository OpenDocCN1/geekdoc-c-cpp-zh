cannot simply check the delete permission in the OnPreInit method of the page because that would prevent users without the delete permission from being able to access it at all. Instead, you can handle the ItemDeleting event of the FormView control or the RowDeleting event of the GridView control and check user permissions there. Alternatively, to make implementation simpler and more consistent between the Details and List page templates, you can also handle the Deleting event of the EntityDataSource control, which works the same way with both UI controls. Here is the markup:

```
<asp:EntityDataSource ID="dataSource" runat="server" EnableDelete="true" OnDeleting="DataSource_Deleting" />
```

In the event handler, you simply call the CanDelete method of the MetaTable object associated with the page, redirect users without the delete permission to the login page, similar to the one shown back in Figure 14.5, and terminate further request processing:

```
protected void DataSource_Deleting(object sender, EventArgs e)
{
    if (!this.table.CanDelete(this.User))
    {
        FormsAuthentication.RedirectToLoginPage();
        this.Response.End();
    }
}
```

# Modifying Page Templates to Hide Inaccessible Actions

The dynamic List page displays links that allow users to Insert, Edit, Delete, and see Details of entities. Likewise, the Details page displays the links that allow users to Edit and Delete the current entity. If you want the users of the application to see these links regardless of whether they are authorized to perform the actions, nothing else needs to be changed. The out-of-the box page templates already display them, and if the user tries to perform an unauthorized action, with the changes already put in place in the previous section, he is redirected to a login page similar to that shown in Figure 14.5. However, if you want to implement security trimming and hide the actions that users cannot perform, several additional changes in the page templates are required.

In the List page template, the Details link takes the user to the Details page where they can “read” a single record or entity instance of the same entity type. Like the List page itself, it requires the user to have the CanRead permission. Therefore, if the user is authorized to see the List page, she is also authorized to see the Details page, and you don't need to worry about hiding or showing the Details link dynamically. The Edit, Insert, and Delete actions, however, require the CanUpdate, CanInsert, and CanDelete permissions, respectively, and you need to hide the links if the user is not authorized to perform them.

Here is the (abbreviated) markup to recap how the List page template implements the action links: