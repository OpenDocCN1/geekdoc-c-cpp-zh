# The Select method of the AccessDataSource class

| Method | Description |
| --- | --- |
| Select(selectOptions) | Returns an IEnumerable object that contains the rows retrieved from the underlying Access database. To get all the rows, the selectOptions parameter should be DataSourceSelectArguments.Empty. |

# Members of the DataView class for retrieving rows

| Property | Description |
| --- | --- |
| RowFilter | A string that is used to filter the rows retrieved from the Access database. |
| Indexer | Description |
| [index] | Returns a DataRowView object for the row at the specified index position. |

# Members of the DataRowView class for retrieving columns

| Indexer | Description |
| --- | --- |
| [index] | Returns the value of the column at the specified index position as an object. |
| [name] | Returns the value of the column with the specified name as an object. |

# Code that gets product information for the selected product

```
DataView productsTable = (DataView)
    AccessDataSource1.Select(DataSourceSelectArguments.Empty);
productsTable.RowFilter =
    "ProductID = '" + ddlProducts.SelectedValue + "'";
DataRowView row = (DataRowView) productsTable[0];

Product p = new Product();
p.ProductID = row["ProductID"].ToString();
p.Name = row["Name"].ToString();
p.ShortDescription = row["ShortDescription"].ToString();
p.LongDescription = row["LongDescription"].ToString();
p.UnitPrice = (decimal)row["UnitPrice"];
p.ImageFile = row["ImageFile"].ToString();
```

# Description

+   - The Select method of the AccessDataSource class returns an IEnumerable object that contains the rows retrieved from the Access database. To work with these rows, you must cast the IEnumerable object to a DataView object.
+   - The RowFilter property of the DataView class lets you filter rows in the data view based on a criteria string.
+   - You can use the indexer of the DataView class to return a specific row as a DataRowView object. Then, you can use the indexer of the DataRowView class to return the value of a specified column. The indexer for the column can be an integer that represents the column’s position in the row or a string that represents the name of the column.
+   - The DataView and DataRowView classes are stored in the System.Data namespace.