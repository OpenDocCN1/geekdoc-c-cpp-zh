Aside from using MetaTable permission methods to hide the foreign key columns the user is not allowed to read, Dynamic Data doesn't do anything else out of the box. In other words, it ignores the values returned by the CanInsert, CanUpdate, and CanDelete methods; in fact, it never calls them. For example, if you try to prevent unauthorized users from making changes in any of the tables by implementing the three permission methods similar to this

```
public override bool CanUpdate(IPrincipal principal)
{
    return principal.IsInRole("Employee");
}
```

...the dynamic Products will still display the Edit, Delete, and Insert new item links shown in Figure 14.4. Even more importantly, if the unauthorized user actually clicks one of these links, he can access it. He can even access the dynamic Suppliers page by typing its address directly in the address bar of their web browser, even though the Products page might not display the Supplier hyperlinks for them. Luckily, with just a few changes, you can make the dynamic page templates support the permission methods completely and implement both access control and UI trimming.

# Modifying Page Templates to Prevent Unauthorized Access

The Insert page template generates web pages that allow users to create new entity instances, or in database terms, insert new records in a particular table. To determine whether the current user is authorized to perform this action, it needs to call the CanInsert method of the MetaTable object describing the entity type. Here is a code snippet that shows how access security can be implemented in this template:

```
public partial class Insert : Page
{
    protected MetaTable table;
    protected override void OnPreInit(EventArgs e)
    {
        base.OnPreInit(e);
        this.table = DynamicDataRouteHandler.GetRequestMetaTable(this.Context);
        if (!this.table.CanInsert(this.User))
        {
            FormsAuthentication.RedirectToLoginPage();
            this.Response.End();
        }
    }
}
```