# In C# 6

```
var dict = new Dictionary<int, string>()
{
    [3] = "three",
    [7] = "seven"
};
```

Dictionary initializers are covered in Chapter 11, “Collections.”

# Exception Filters

Exception filters allow you to filter exceptions before catching them.

# In C# 5

```
try
{
    //etc.
}
catch (MyException ex)
{
    if (ex.ErrorCode != 405) throw;
    // etc.
}
```

# In C# 6

```
try
{
    //etc.
}
catch (MyException ex) when (ex.ErrorCode == 405)
{
    // etc.
}
```

A big advantage of the new syntax is not only that it reduces the code length but also that the stack trace is not changed—which happens with the C# 5 variant. Exception filters are covered in Chapter 14, “Errors and Exceptions.”

# Await in Catch

await can now be used in the catch clause. C# 5 required a workaround.

# In C# 5

```
bool hasError = false;
string errorMessage = null;
try
{
    //etc.
}
catch (MyException ex)
{
    hasError = true;
    errorMessage = ex.Message;
}
if (hasError)
{
    await new MessageDialog().ShowAsync(errorMessage);
}
```