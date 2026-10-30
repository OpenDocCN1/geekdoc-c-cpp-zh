# Tip

If a newly created TableDef (or other object) doesn't appear in the Navigation pane, press F5 to refresh it.

The CreateNewTableDef procedure includes two statements that control how Access handles errors in this code. Chapter 27 discusses the VBA error handling statements and explains why you'd use On Error Resume Next and On Error GoTo 0 in a procedure such as this.

TableDef objects are stored in the TableDefs collection. The following procedure displays the names of all TableDef objects (including hidden and system tables) in the current database:

```
Public Sub DisplayAllTableDefs()

    Dim daDb As DAO.Database
    Dim daTdf As DAO.TableDef

    Set daDb = CurrentDb

    With daDb

        Debug.Print .TableDefs.Count & _
            " TableDefs in " & .Name

        For Each daTdf In .TableDefs
            Debug.Print , daTdf.Name
        Next daTdf
    End With

    daDb.Close
    Set daDb = Nothing

End Sub
```

# The DAO QueryDef object

A QueryDef object represents a saved query in an Access database. Using VBA code, you can point a QueryDef object variable at an existing query (or create a new query) and change the query's SQL statement, populate parameters used by the query, and execute the query. The query could be a select query that returns a recordset or an action query that modifies code in the tables underlying the query.

Creating a QueryDef in code is similar to creating a TableDef except that the new QueryDef doesn't have to be explicitly appended to the database's QueryDefs collection.