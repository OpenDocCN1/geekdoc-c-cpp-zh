that will be used by others.

Here is how you could raise a custom exception without wrapping the inner exception:

```
try
{
    // ...
}
catch (SomeStandardException ex)
{
    // ...
    throw new MyCustomException(someMessage);
}
```

# Conclusion

When raising a custom exception (either with wrapping or with an unwrapped new exception), you should raise an exception that is meaningful to the caller. For instance, a user of a class library may not know much about how that library does its internal work. The exceptions that are thrown by the dependencies of the class library are not meaningful. Rather, the user wants an exception that is relevant to how the class library is using those dependencies in an erroneous way.

```
try
{
    // ...
}
catch (IOException ex)
{
    // ...
    throw new StorageServiceException("@The Storage Service encountered a problem saving your data. Please consult the inner exception for technical details.
If you are not able to resolve the problem, please call 555-555-1234 for technical assistance.", ex);
}
```

# Section 76.2: Finally block

```
try
{
    /* code that could throw an exception */
}
catch (Exception)
{
    /* handle the exception */
}
finally
{
    /* Code that will be executed, regardless if an exception was thrown / caught or not */
}
```

The try / catch / finally block can be very handy when reading from files.

For example:

```
FileStream f = null;
```

```
try
{
    f = File.OpenRead("file.txt");
    /* process the file here */
```