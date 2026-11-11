| `javax.swing.JTable` | `1.2` |
|---|---|
| `JTable(Object[][] entries, Object[] columnNames)` | constructs a table with a default table model. |
| `void print()` `5.0` | displays a print dialog box and prints the table. |
| `boolean getAutoCreateRowSorter()` `6` |  |
| `void setAutoCreateRowSorter(boolean newValue)` `6` | gets or sets the autoCreateRowSorter property. The default is false. When set, a default row sorter is automatically set whenever the model changes. |
| `boolean getFillsViewportHeight()` `6` |  |
| `void setFillsViewportHeight(boolean newValue)` `6` | gets or sets the fillsViewportHeight property. The default is false. When set, the table always fills the enclosing viewport. |

# 11.1.2 Table Models

In the preceding example, the table data were stored in a two-dimensional array. However, you should generally not use that strategy in your own code. Instead of dumping data into an array to display it as a table, consider implementing your own table model.

Table models are particularly simple to implement because you can take advantage of the AbstractTableModel class that implements most of the required methods. You only need to supply three methods:

```
public int getRowCount();
public int getColumnCount();
public Object getValueAt(int row, int column);
```

There are many ways of implementing the getValueAt method. For example, if you want to display the contents of a RowSet that contains the result of a database query, simply provide this method:

```
public Object getValueAt(int r, int c)
{
    try
    {
        rowSet.absolute(r + 1);
        return rowSet.getObject(c + 1);
    }
}
```