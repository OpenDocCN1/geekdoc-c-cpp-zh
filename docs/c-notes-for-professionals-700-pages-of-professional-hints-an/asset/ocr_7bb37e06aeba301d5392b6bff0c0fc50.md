# The finally block

The finally block executes every time whether the exception is thrown or not. One subtlety with expressions in when is exception filters are executed further up the stack before entering the inner finally blocks. This can cause unexpected results and behaviors when code attempts to modify global state (like the current thread's user or culture) and set it back in a finally block.

# Example: finally block

```
```csharp
private static bool Flag = false;

static void Main(string[] args)
{
    Console.WriteLine("Start");
    try
    {
        SomeOperation();
    }
    catch (Exception) when (EvaluatesTo())
    {
        Console.WriteLine("Catch");
    }
    finally
    {
        Console.WriteLine("Outer Finally");
    }
}

private static bool EvaluatesTo()
{
    Console.WriteLine($"EvaluatesTo: {Flag}");
    return true;
}

private static void SomeOperation()
{
    try
    {
        Flag = true;
        throw new Exception("Boom");
    }
    finally
    {
        Flag = false;
        Console.WriteLine("Inner Finally");
    }
}
```
```

# Produced Output:

+   - Start
+   - EvaluatesTo: True
+   - Inner Finally
+   - Catch
+   - Outer Finally

View Demo