For example:

```
```java
int read(String file, String pattern)
{
    logger.entering("com.mycompany.mylib.Reader", "read",
        new Object[] { file, pattern });
    . . .
    logger.exiting("com.mycompany.mylib.Reader", "read", count);
    return count;
}
```
```

These calls generate log records of level FINER that start with the strings ENTRY and RETURN.

# **NOTE:**

At some point in the future, the logging methods with an `Object[]` parameter will be rewritten to support variable parameter lists (“varargs”). Then, you will be able to make calls such as `logger.entering("com.mycompany.mylib.Reader", "read", file, pattern)`.

A common use for logging is to log unexpected exceptions. Two convenience methods include a description of the exception in the log record.

```
```java
void throwing(String className, String methodName, Throwable t)
void log(Level l, String message, Throwable t)
```
```

Typical uses are

```
```java
if (. . .)
{
    var e = new IOException(". . .");
}
```
```