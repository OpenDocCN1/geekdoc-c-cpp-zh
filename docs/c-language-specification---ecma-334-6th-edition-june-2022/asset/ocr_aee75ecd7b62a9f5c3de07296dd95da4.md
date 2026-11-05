In order to locate a handler for an exception, catch clauses are examined in lexical order. If a catch clause specifies a type but no exception filter, it is a compile-time error for a later catch clause of the same try statement to specify a type that is the same as, or is derived from, that type.

> Note: Without this restriction, it would be possible to write unreachable catch clauses. end note

Within a catch block, a throw statement (§12.10.6) with no expression can be used to re-throw the exception that was caught by the catch block. Assignments to an exception variable do not alter the exception that is re-thrown.

Example: In the following code

```
using System;

class Test
{
    static void F()
    {
        try
        {
            G();
        }
        catch (Exception e)
        {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw; // re-throw
        }
    }

    static void G() => throw new Exception("G");

    static void Main()
    {
        try
        {
            F();
        }
        catch (Exception e)
        {
            Console.WriteLine("Exception in Main: " + e.Message);
        }
    }
}
```

the method F catches an exception, writes some diagnostic information to the console, alters the exception variable, and re-throws the exception. The exception that is re-thrown is the original exception, so the output produced is:

Exception in F: G
Exception in Main: G

If the first catch block had thrown e instead of rethrowing the current exception, the output produced would be as follows:

Exception in F: G
Exception in Main: F