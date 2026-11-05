# 7.　The DataTable Class

The DataTable class represents **the tables in the database**. It has the following important properties; most of these properties are read only properties except the **PrimaryKey property**.

+   - **Some important properties of datatable class**

| Properties | Description |
|---|---|
| ChildRelations | Returns the collection of child relationship. |
| Columns | Returns the columns collection. |
| Constraints | Returns the constraints collection. |
| DataSet | Returns the parent DataSet. |
| DefaultView | Returns a view of the table. |
| ParentRelations | Returns the ParentRelations collection. |
| PrimaryKey | Gets or sets an array of columns as the primary key for the table. |
| Rows | Returns the Rows collection. |

+   - **Some important methods of the DataTable class**

| Methods | Description |
|---|---|
| AcceptChanges | Commits all changes since the last AcceptChanges. |
| Clear | Clears all data from the table. |
| GetChanges | Returns a copy of the DataTable with all changes made since the AcceptChanges method was called. |
| GetErrors | Returns an array of rows with errors. |
| ImportRows | Copies a new row into the table. |
| LoadDataRow | Finds and updates a specific row, or creates a new one, if not found any. |
| Merge | Merges the table with another DataTable. |
| NewRow | Creates a new DataRow. |