
# The user interface for the Customer Maintenance application

![](img/3148667e42d4db35b3d08576aaa1fa01_584_0.png)

# The code for the application

```
private void Form1_Load(object sender, EventArgs e)
{
    // TODO: This line of code loads data into the
    // mMABooksDataSet.Customers' table.
    // You can move, or remove it, as needed.
    this.customersTableAdapter.Fill(this.mMABooksDataSet.Customers);
}
```

```
private void customersBindingNavigatorSaveItem_Click(
object sender, EventArgs e)
{
    this.Validate();
    this.customersBindingSource.EndEdit();
    this.tableAdapterManager.UpdateAll(this.mMABooksDataSet);
}
```

Figure 18-12 A Customer Maintenance application that uses TextBox controls

## How to handle data errors

When you develop an application that uses a data source, you'll want to provide code that handles any data errors that might occur. In general, those errors fall into three categories: data provider errors, ADO.NET errors, and errors that the DataGridView control detects. You'll learn how to provide for these errors in the topics follow.

### How to handle data provider errors

When you access a database, there is always the possibility that an unrecoverable error might occur. For example, the database server might be shut down when you try to access it, or the network connection to the database server might be broken. Either way, your applications should usually anticipate such problems by catching any database exceptions that might occur.

Figure 18-13 shows the exceptions thrown by the .NET data providers when an unrecoverable error occurs. You can refer to these errors as data provider errors. As you can see, each data provider has its own exception class. So, if you're using the SQL Server provider, you should catch exceptions of the SqlException class. If you're using the Oracle data provider, you should catch exceptions of the OracleException class. And so on.

The code example in this figure shows how you can catch a SQLException that might occur when attempting to fill a dataset using a table adapter. Here, the shaded lines show the code that has been added to the generated code. This code will display an error message when a SqlException occurs, and it uses the Number and Message properties of the SQLException class to display details about the exception. It also uses the GetType method to indicate the type of exception that occurred.

Although it's uncommon, more than one server error can occur as the result of a single database operation. In that, an error object is created for each error. These errors are stored in a collection that you can access through the Errors property of the exception object. Each error object contains a Number and Message property just like the exception object. However, because the Number and Message properties of the exception object are set to the Number and Message properties of the first error in the Errors collection, you don't usually need to work with the individual error objects.

## .NET data provider exception classes

| Name | Description |
| --- | --- |
| SqlException | Thrown if a server error occurs when accessing a SQL Server database. |
| OracleException | Thrown if a server error occurs when accessing an Oracle database. |
| OdbException | Thrown if a server error occurs when accessing an ODBC database. |
| OleDbException | Thrown if a server error occurs when accessing an OLE DB database. |

## Common members of the .NET data provider exception classes

| Property | Description |
| --- | --- |
| Number | An error number that identifies the type of error. |
| Message | A message that describes the error. |
| Source | The name of the provider that generated the error. |
| Errors | A collection of error objects that contain information about the errors that occurred during a database operation. |

| Method | Description |
| --- | --- |
| GetType () | Gets the type of the current exception. |

## Code that catches a SQL exception

```
private void Form1_Load(object sender, EventArgs e) {
    try {
        this.customersTableAdapter.Fill(this.mmABooksDataSet.Customers);
    } catch (SqlException ex) {
        MessageBox.Show("Database error #" + ex.Number + ": " + ex.Message, ex.GetType().ToString());
    }
}
```

## Description

- Whenever the data provider (SQL Server, Oracle, ODBC, or OLE DB) encounters a situation it can't handle, a data provider exception is thrown. You can handle types of exceptions by catching them and displaying appropriate error messages.
- The Number and Message properties pinpoint the specific server error that caused the data provider exception to be thrown.
- The SQLException class is stored in the System.Data.SqlClient namespace.

![](img/3148667e42d4db35b3d08576aaa1fa01_586_0.png)

## How to handle ADO.NET errors

When you work with controls, ADO.NET errors can occur when the data in those controls is saved to the dataset (not the database), or when an Insert, Update, or Delete statement can't be executed against the database. Figure 18-14 presents some of the most common of those errors.

Here, ConstraintException and NullAllowedException are subclasses of the DataException class, so you can catch each of these errors by catching DBConcurrencyException. In contrast, DBConcurrencyException is not a subclass of the DataException class, so you must catch DBConcurrencyException errors separately. All of the ADO.NET exception classes are members of the System.Data namespace.

The error-handling code in this figure catches errors caused by the EndEdit method of a binding source and the UpdateAll method of a table adapter manager. The first exception, DBConcurrencyException, occurs if the number of rows that are affected by an insert, update, or delete operation is zero, which typically indicates that concurrency errors have occurred. A message box is used to display an error message, and the Fill method of the table adapter is used to retrieve the current data from the database and load it into the dataset. That will help prevent further errors from occurring.

Although you might think that a concurrency error would be generated by the database rather than ADO.NET, that's not the case. To understand why, you need to realize that the Update and Delete statements are generated for a table adapter contain code that checks that a row hasn't changed since it was retrieved. But if the row has changed, the row with the specified criteria won't be found and the row wasn't updated or deleted, however, it realizes there was a concurrency error and throws an exception.

## Common ADO.NET exception classes

| Class | Description |
|---|---|
| DBConcurrency | The exception that's thrown if the number of rows affected by an insert, update, or delete operation is zero. This typically caused by concurrency. |
| DataException | The general exception that's thrown when an ADO.NET error occurs. |
| ConstraintException | The exception that's thrown when an operation violates a constraint. This is a subclass of the DataException class. |
| NullNullException | The exception that's thrown when an add or update operation attempts to save a null value in a column that doesn't allow nulls. This is a subclass of the DataException class. |

## Common members of ADO.NET classes

| Property | Description |
|---|---|
| Message | A message that describes the exception. |
| Method | |
| GetType() | Gets the type of the current exception. |

## Code that handles ADO.NET errors

```
try {
    this.customersBindingSource.EndEdit();
    this.tableAdapter.UpdateAll(this.mMABooksDataSet);
} catch (DBConcurrencyException) {
    MessageBox.Show("A concurrency error occurred." + 
        " Some rows were not updated.", "Concurrency Exception");
    this.customerTableAdapter.Fill(this.mMABooksDataSet.Customers);
} catch (DataException ex) {
    MessageBox.Show(ex.Message, ex.GetType().ToString());
    customersBindingSource.CancelEdit();
} catch (SqlException ex) {
    MessageBox.Show("Database error # " + ex.Number + 
        ": " + ex.Message, ex.GetType().ToString());
}
```

## Description

- An ADO.NET exception is an exception that occurs on any ADO.NET object. All of these exceptions are members of the System.Data namespace.
- In most cases, you'll catch specific types of exceptions if you want to perform special processing when those exceptions occur. Then, you can use the DataException class to catch all ADO.NET exceptions that are represented by its subclasses.
