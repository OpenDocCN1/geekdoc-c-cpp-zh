# The DAO TableDef object

The DAO TableDef object represents a table in an Access database. The table may be local to the current database or linked to an external source. The following procedure (which is included in the Chapter28.accdb example database) creates a new table named MyTempTable, adds three text fields to it, and adds the table to the current database’s TableDefs collection.

```
```vb
Public Sub CreateNewTableDef()

    Dim daDb As DAO.Database
    Dim taDtf As DAO.TableDef

    Const sTABLENAME As String = "MyTempTable"

    Set daDb = Application.CurrentDb

    'Delete an existing table, but ignore the error
    'if table doesn't exist
    On Error Resume Next
        daDb.TableDefs.Delete sTABLENAME
    On Error GoTo 0

    ' Create a new TableDef object:
    Set taDtf = daDb.CreateTableDef(sTABLENAME)

    With taDtf
        ' Create fields and append them to the TableDef
        .Fields.Append .CreateField("FirstName", dbText)
        .Fields.Append .CreateField("LastName", dbText)
        .Fields.Append .CreateField("Phone", dbText)
    End With

    ' Append the new TableDef object to the current database:
    daDb.TableDefs.Append taDtf

    daDb.Close
    Set daDb = Nothing

End Sub
```
```

Running this code in the Chapter28.accdb database creates a new table named MyTempTable, a permanent addition to the database. Notice that the CreateNewTableDef procedure deletes this table if it exists, before creating it as a new TableDef. Access won’t be able to append the new TableDef object to its TableDefs collection if a table with the same name already exists in the database.