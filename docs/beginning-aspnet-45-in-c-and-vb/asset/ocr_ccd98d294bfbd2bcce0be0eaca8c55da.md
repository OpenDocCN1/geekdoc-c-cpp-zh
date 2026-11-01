16. Go into the Code Behind and modify the code as follows. Note that the ItemInserted and ItemUpdated handlers call the EndEditing method (that you also need to add to the code), whereas ItemInserting and ItemUpdating both set the UpdateDateTime value:

# VB.NET

```
Private Sub EndEditing()
    Response.Redirect("Reviews.aspx")
End Sub

Protected Sub DetailsView1_ItemInserted(sender As Object,
    e As DetailsViewInsertedEventArgs) Handles DetailsView1.ItemInserted
    If e.Exception Is Nothing Then
        EndEditing()
    End If
End Sub

Protected Sub DetailsView1_ItemInserting(sender As Object,
    e As DetailsViewInsertEventArgs) Handles DetailsView1.ItemInserting
    e.Values("UpdateDateTime") = DateTime.Now
End Sub

Protected Sub DetailsView1_ItemUpdated(sender As Object,
    e As DetailsViewUpdatedEventArgs) Handles DetailsView1.ItemUpdated
    If e.Exception Is Nothing Then
        EndEditing()
    End If
End Sub

Protected Sub DetailsView1_ItemUpdating(sender As Object,
    e As DetailsViewUpdateEventArgs) Handles DetailsView1.ItemUpdating
    e.NewValues("UpdateDateTime") = DateTime.Now
End Sub
```

# C#

```
private void EndEditing()
{
    Response.Redirect("Reviews.aspx");
}

protected void DetailsView1_ItemInserted(object sender,
    DetailsViewInsertedEventArgs e)
{
    if (e.Exception == null)
    {
        EndEditing();
    }
}
```

![](bbox=[0.62, 0.12, 0.89, 0.38])

FIGURE 13-23