```
}
bool ExceptionFilter(Exception ex)
{
    Console.WriteLine("Filter");
    return true;
}

static void Method()
{
    try
    {
        throw new ArgumentException();
    }
    finally
    {
        Console.WriteLine("Finally");
    }
}
```

the method Method throws an exception. The first action is to examine the enclosing catch clauses, executing any exception filters. Then, the finally clause in Method executes before control transfers to the enclosing matching catch clause. The resulting output is:

```
Filter
Finally
Catch
end example
```

The try block of a try statement is reachable if the try statement is reachable.
A catch block of a try statement is reachable if the try statement is reachable.
The finally block of a try statement is reachable if the try statement is reachable.
The end point of a try statement is reachable if both of the following are true:

+   - The end point of the try block is reachable or the end point of at least one catch block is reachable.
+   - If a finally block is present, the end point of the finally block is reachable.

# 12.12 The checked and unchecked statements

The checked and unchecked statements are used to control the overflow-checking context for integral-type arithmetic operations and conversions.

```
checked_statement
    : 'checked' block
    ;

unchecked_statement
    : 'unchecked' block
    ;
```