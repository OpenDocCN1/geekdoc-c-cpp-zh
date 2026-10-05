# .NET data provider exception classes

| Name | Description |
| --- | --- |
| SqlException | Thrown if a server error occurs when accessing a SQL Server database. |
| OracleException | Thrown if a server error occurs when accessing an Oracle database. |
| OdbException | Thrown if a server error occurs when accessing an ODBC database. |
| OleDbException | Thrown if a server error occurs when accessing an OLE DB database. |

# Common members of the .NET data provider exception classes

| Property | Description |
| --- | --- |
| Number | An error number that identifies the type of error. |
| Message | A message that describes the error. |
| Source | The name of the provider that generated the error. |
| Errors | A collection of error objects that contain information about the errors that occurred during a database operation. |

| Method | Description |
| --- | --- |
| GetType () | Gets the type of the current exception. |

# Code that catches a SQL exception

```
private void Form1_Load(object sender, EventArgs e) {
    try {
        this.customersTableAdapter.Fill(this.mmABooksDataSet.Customers);
    } catch (SqlException ex) {
        MessageBox.Show("Database error #" + ex.Number + ": " + ex.Message, ex.GetType().ToString());
    }
}
```

# Description

+   - Whenever the data provider (SQL Server, Oracle, ODBC, or OLE DB) encounters a situation it can't handle, a data provider exception is thrown. You can handle types of exceptions by catching them and displaying appropriate error messages.
- The Number and Message properties pinpoint the specific server error that caused the data provider exception to be thrown.
- The SQLException class is stored in the System.Data.SqlClient namespace.

![](bbox=[0.074, 0.935, 0.895, 0.966])