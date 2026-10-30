# Part VII: Advanced Access Programming Techniques

You specify the type of recordset using the dbOpenTable, dbOpenDynaset, dbOpenSnapshot, and dbOpenForwardOnly constants as arguments of the OpenRecordset method of a Database object. The following example shows how to open a Snapshot-type recordset based on a SQL string:

```
Dim daDb As DAO.Database
Dim daRs As DAO.Recordset
Dim sSql As String
sSql = "SELECT * FROM tblCustomers;"
Set daDb = CurrentDb
Set daRs = daDb.OpenRecordset(sSql, dbOpenSnapshot)
```

If you don't explicitly choose a type of Recordset, Access uses what it believes to be the most efficient method. The Dynaset-type recordset is the most commonly used because it's the most versatile. The other types restrict what you can do with the recordset in exchange for better performance.

# Navigating recordsets

Recordsets wouldn't be much use if all you could do is open and close them. Depending on context, the word recordset means several different things:

+   - The rows of data returned by a query
+   - The data bound to an Access form
+   - The object filled with data as the result of a DAO operation

In all cases, however, a recordset is a data structure containing rows and columns of data. The rows, of course, are records, while the columns are fields.

It makes sense that DAO provides ways to navigate through a recordset. When viewing a table or query results as a datasheet, you can use the vertical and horizontal scroll bars or arrow keys to move up and down, left and right, through the Datasheet view of the recordset. It's not surprising, then, that Recordset objects support methods for moving through the records contained in a recordset.

The following procedure, RecordsetNavigation, demonstrates the fundamental recordset navigation methods:

```
Public Sub RecordsetNavigation()

    Dim daDb As DAO.Database
    Dim daRs As DAO.Recordset

    Set daDb = CurrentDb
    Set daRs = daDb.OpenRecordset("tblCustomers", dbOpenTable)

    Debug.Print daRs!CustomerID, daRs!Company

    daRs.MoveNext
    Debug.Print daRs!CustomerID, daRs!Company
```