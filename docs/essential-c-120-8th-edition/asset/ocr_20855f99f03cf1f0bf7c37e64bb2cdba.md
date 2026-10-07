# Defining Custom Exceptions 615

```
System.Data.OracleClient.OracleException? exception
  : base(message, innerException: exception)
{
  // ...
}
public DatabaseException()
{
  // ...
}
public DatabaseException(string? message)
  : base(message)
{
  // ...
}
public DatabaseException(
  string? message, Exception? exception)
  : base(message, innerException: exception)
{
  // ...
}
  // ...

```

This custom exception might be created to wrap proprietary database exceptions. Since Oracle and SQL Server (for example) throw different exceptions for similar errors, an application could define a custom exception that standardizes the database-specific exceptions into a common exception wrapper that the application can handle in a standard manner. That, whether the application was using an Oracle or a SQL Server back-end database, the same catch block could be used to handle the error higher up the stack.

The only requirement for a custom exception is that it derives from System .Exception or one of its descendants. Other good practices for custom exceptions are as follows:

+   - All exceptions should use the “Exception” suffix. This way, their purpose is easily established from their name.
- Generally, all exceptions should include constructors that take no parameters, a string parameter, and a parameter set consisting of a string and an inner