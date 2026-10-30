```
"tblSalesPerson", "SalesPersonID = " & index + 1), _
vbNullString)

label = sName

End Sub
```

The first callback (ddLogin_getItemCount) gets the count of items to be placed on the DropDown’s list. Notice the ByRef count parameter. This parameter tells the DropDown how many items to accommodate on its list.

The second procedure (ddLogin_getItemLabel) actually retrieves the items for the list. In this case, the procedure pulls the SalesPerson name field from tblSalesPersons using DLookup. ddLogin_getItemLabel is called by the DropDown multiple times; the exact number of calls is determined by the count value established by ddLogin_getItemCount.

An accurate count of values to add to the DropDown is important. The DropDown has no way, other than the count parameter, to know how many items to expect. Setting a count too low means that not all items will be added, whereas setting the count too high means that list contains blank spaces. For instance, if you set the count to ten items but only five are available, then the DropDown’s list contains the five items but also five blank spaces.

The ddLogin_getItemLabel routine cheats a little bit to supply this information. Notice the index parameter passed to this routine, which tells the procedure which slot on the drop-down list is being filled when the procedure is called. The DLookup adds 1 to this value and extracts the name of the salesperson whose ID matches this value. This means that the SalesPersonID values have to be sequential, starting with 1, or this procedure will fail.

Extracting data with nonsequential ID values, or where the ID value is non-numeric, requires a bit more work. In the following code, ddLogin_getItemLabel has been rewritten to use a recordset rather than the DLookup function. The ddLogin_onAction procedure uses a recordset in the same way:

```
Private Const msSQLSALESPERSON As String = _
    "SELECT SalesPersonName FROM tblSalesPerson ORDER BY
    SalesPersonName;"

Public Sub ddLogin_getItemLabel( _
    control As IRibbonControl, index As Integer, ByRef label)

    Dim adRs As ADODB.Recordset

    Set adRs = CurrentProject.Connection.Execute(msSQLSALESPERSON)
    adRs.Move index

    label = adRs.Fields(0).Value

End Sub
```