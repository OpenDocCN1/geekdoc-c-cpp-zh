> **NOTE
Placing the core functionality into a single method that all other overloading methods invoke that you can make changes in implementation in just the core method, which the other methods will automatically take advantage of.

# Optional Parameters

The C# language designers also added support for optional parameters. By allowing the association of a parameter with a constant value as part of the method declaration, it is possible to call a method without passing an argument for every parameter of the method (see Listing 5.24).

Listing 5.24: Methods with Optional Parameters

```
public static class LineCounter
{
    public static void Main(string[] args)
    {
        if(args.Length > 1)
        {
            totalLineCount = DirectoryCountLines(args[0], args[1]);
        }
        else if(args.Length > 0)
        {
            totalLineCount = DirectoryCountLines(args[0]);
        }
        else
        {
            totalLineCount = DirectoryCountLines();
        }
        Console.WriteLine(totalLineCount);
    }
}
```

7. Introduced in C# 4.0.