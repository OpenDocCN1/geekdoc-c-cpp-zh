```
LogManager.Log(ex.ToString());
}
```

# Do not catch exceptions that you cannot handle

Many resources, such as this one, strongly urge you to consider why you are catching an exception in the place that you are catching it. You should only catch an exception if you can handle it at that location. If you can do something there to help mitigate the problem, such as trying an alternative algorithm, connecting to a backup database, trying another filename, waiting 30 seconds and trying again, or notifying an administrator, you can catch the error and do that. If there is nothing that you can plausibly and reasonably do, just "let it go" and let the exception be handled at a higher level. If the exception is sufficiently catastrophic and there is no reasonable option other than for the entire program to crash because of the severity of the problem, then let it crash.

```
try
{
    //Try to save the data to the main database.
}
catch(SqlException ex)
{
    //Try to save the data to the alternative database.
}
//If anything other than a SqlException is thrown, there is nothing we can do here. Let the exception bubble up to a level where it can be handled.
```

# Section 76.4: Exception Anti-patterns

# Swallowing Exceptions

One should always re-throw exception in the following way:

```
try
{
    ...
}
catch (Exception ex)
{
    ...
    throw;
}
```

Re-throwing an exception like below will obfuscate the original exception and will lose the original stack trace. One should never do this! The stack trace prior to the catch and rethrow will be lost.

```
try
{
    ...
}
catch (Exception ex)
{
    ...
    throw ex;
}
```

# Baseball Exception Handling

One should not use exceptions as a substitute for normal flow control constructs like if-then statements and while loops. This anti-pattern is sometimes called Baseball Exception Handling.