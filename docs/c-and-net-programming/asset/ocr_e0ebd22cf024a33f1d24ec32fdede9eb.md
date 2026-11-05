```
catch (Exception ex)
{
    //Some exception handling code
}

finally
{
    sqlConnection.Close();
}
```

# Using the "using" statement in ADO .NET Exception handling

The using statement can be used to specify a boundary for the object outside of which, the object is destroyed automatically. The runtime invokes the Dispose method of the objects that are specified within this statement when the control comes out of this block. This is why this is a preferred choice when using exceptions for managing resources in .NET. Refer to the following code that uses the "using" statement :

```
string connectionString = ...; // Some connection string
using (SqlConnection sqlConnection = new SqlConnection(connectionString))
{
    sqlConnection.Open();
    //Some code
}
```

Note that when the end of the using block would be encountered, the Dispose () method will be immediately called on the instance. Note that when the Dispose() method is called on this connection instance, it checks to see if the connection is opened; if open it would close it implicitly prior to disposing off the instance.

Dispose and Finalize for more information on when and how to use them appropriately.

The above code gets translated implicitly to :

```
string connectionString = ...;// Some connection string
SqlConnection sqlConnection = new SqlConnection(connectionString);
try
{
    sqlConnection.Open();
    //Some code
}
finally
{
    ((IDisposable)sqlConnection).Dispose();
}
```

Remember to keep the try block as short as possible. Note that in the code example above, the connection is just opened in the try block. Do not use any unnecessary code/logic in the try