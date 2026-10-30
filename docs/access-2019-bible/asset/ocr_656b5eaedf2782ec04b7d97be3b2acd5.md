```
daRs.MoveLast
Debug.Print daRs!CustomerID, daRs!Company

daRs.MovePrevious
Debug.Print daRs!CustomerID, daRs!Company

daRs.MoveFirst
Debug.Print daRs.Fields("CustomerID").Value, _
    daRs.Fields("Company").Value

daRs.Close
Set daRs = Nothing
Set daDb = Nothing

End Sub
```

This procedure begins by setting a variable to the current database and opening a Recordset object populated with data from tblCustomers. It immediately displays the CustomerID and Company from the very first record; then it moves around the recordset a few rows at a time, displaying the CustomerID and Company for each record along the way. It ends by returning to the first record and displaying its data. The output produced by RecordsetNavigation is shown in Figure 28.3.

# FIGURE 28.3

Demonstrating recordset navigation.

![](bbox=[0.22, 0.68, 0.55, 0.85])

Obviously, this is a trivial example meant to demonstrate how easily recordsets can be navigated. As a developer, you're free to work with any record in the recordset, moving up and down the rows as needed.

Recordsets support the concept of a current record pointer. Only one record at a time within a recordset is current. When you make changes to a recordset or navigate through its rows, your code affects only the current record.

The RecordsetNavigation procedure also demonstrates two methods for referencing individual fields within a record: using the bang operator (!) and the Fields collection.