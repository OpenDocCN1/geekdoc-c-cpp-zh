![](bbox=[0.34, 0.09, 0.77, 0.31])

Figure 22-19

| Toolbar Control | Action |
|---|---|
| Move First | Calls the MoveFirst() function for the BindingSource control object, which changes the current record for the underlying data source to be the first record. |
| Move Previous | Calls the MovePrevious() function for the BindingSource control object, which changes the current record for the underlying data source to be the previous record if there is one. |
| Current Position | Corresponds to the value of the Current property for the BindingSource object, which is the current record in the underlying data source. |
| Total Number of Items | Corresponds to the value of the Count property value for the BindingSource object, which corresponds to the number of records in the underlying data source. |
| Move Next | Calls the MoveNext() function for the BindingSource control object, which changes the current record for the underlying data source to be the next record if there is one. |
| Move Last | Calls the MoveLast() function for the BindingSource control object, which changes the current record for the underlying data source to be the last record. |
| Add New | Calls the AddNew() function for the BindingSource object. This has the effect of calling EndEdit() to execute any pending edit operations for the underlying data source and creates a new record in the list maintained by the BindingSource object. This does not update the underlying data source. |
| Delete | Calls the RemoveCurrent() function for the BindingSource object to remove the current record from the list. This does not modify the underlying data source. |