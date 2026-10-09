Defining a custom exception simply involves deriving from System .Exception or some other exception type. Listing 11.5 provides an example.

# **LISTING 11.5: Creating a Custom Exception**

```
class DatabaseException : System.Exception
{
    public DatabaseException(
        System.Data.SqlClient.SQLException exception)
    {
        InnerException = exception;
        // ...
    }

    public DatabaseException(
        System.Data.OracleClient.OracleException exception)
    {
        InnerException = exception;
        // ...
    }

    public DatabaseException()
    {
        // ...
    }

    public DatabaseException(string message)
    {
        // ...
    }

    public DatabaseException(
        string message, Exception innerException)
    {
        InnerException = innerException;
        // ...
    }
}
```

This custom exception might be created to wrap proprietary database exceptions. Since Oracle and SQL Server (for example) throw different excep- tions for similar errors, an application could define a custom exception that standardizes the database-specific exceptions into a common exception wrap- per that the application can handle in a standard manner. That way, whether the application was using an Oracle or a SQL Server back-end database, the same catch block could be used to handle the error higher up the stack.

The only requirement for a custom exception is that it derives from System .Exception or one of its descendants. However, there are several more good practices for custom exceptions: