```
```java
return count;
}
```
```

These calls generate log records of level FINER that start with the strings ENTRY and RETURN.

> > **NOTE:** At some point in the future, the logging methods with an Object[] parameter will be rewritten to support variable parameter lists (“varargs”). Then, you will be able to make calls such as `logger.entering("com.mycompany.mylib.Reader", "read", file, pattern)`.

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
if (...)
{
    var e = new IOException("...");
    logger.throwing("com.mycompany.mylib.Reader", "read", e);
    throw e;
}
```
```

and

```
```java
try
{
    . . . .
}
catch (IOException e)
{
    logger.getLogger("com.mycompany.myapp").log(Level.WARNING, "Reading image", e);
}
```
```

The throwing call logs a record with level FINER and a message that starts with THROW.

# 7.5.3 Changing the Log Manager Configuration

You can change various properties of the logging system by editing a configuration file. The default configuration file is located at `/jdk/conf/logging.properties` (or at `/jre/lib/logging.properties` prior to Java 9).