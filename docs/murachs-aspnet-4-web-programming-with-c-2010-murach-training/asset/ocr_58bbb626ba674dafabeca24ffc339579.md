# Events raised by the DetailsView control

| Event | Description |
|---|---|
| ItemCommand | Raised when a button is clicked. |
| ItemCreated | Raised when an item is created. |
| DataBound | Raised when data binding completes for an item. |
| ItemDeleted | Raised when an item has been deleted. |
| ItemDeleting | Raised when an item is about to be deleted. |
| ItemInserted | Raised when an item has been inserted. |
| ItemInserting | Raised when an item is about to be inserted. |
| ItemUpdated | Raised when an item has been updated. |
| ItemUpdating | Raised when an item is about to be updated. |
| PageIndexChanged | Raised when the index of the displayed item has changed. |
| PageIndexChanging | Raised when the index of the displayed item is about to change. |

# An event handler for the ItemUpdated event

```
protected void DetailsView1_ItemUpdated(
    object sender, DetailsViewUpdatedEventArgs e)
{
    if (e.Exception != null)
    {
        lblError.Text = "A database error has occurred. " +
            "Message: " + e.Exception.Message;
        e.ExceptionHandled = true;
    }
    else if (e.AffectedRows == 0)
    {
        lblError.Text = "Another user may have updated that product. "
            + "Please try again.";
    }
    else
    {
        ddlProducts.DataBind();
    }
}
```

# Description

+   - Like the GridView control, the DetailsView control raises events that you can use to test for database exceptions and concurrency errors.
+   - To determine if a SQL exception has occurred, test the Exception property of the e argument. If an exception has occurred, you can set the ExceptionHandled property to True to suppress the exception. You can also set the KeepInEditMode property to True to keep the DetailsView control in Edit mode. And you can set the KeepInInsertMode property to True to keep the control in Insert mode.
+   - If the AffectedRows property of the e argument is zero and an exception has not been thrown, a concurrency error has probably occurred.
+   - If the DetailsView control is used on a Master/Detail page, you should call the DataBind method of the master list control after a successful insert, update, or delete.