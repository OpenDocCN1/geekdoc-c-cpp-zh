In this case, the first argument ` ` is a literal of `char` type, a space character in particular. `char` is a built-in type in C# representing the Unicode characters. More on this later.

The end result is the same regardless of whether we use `"` or ` ` as a separator. The resulting greeting text, using the string interpolation, is printed to the console, as in the previous example.

```
Console.WriteLine($"Hello {name}!");
```

If you are new to programming, there are two kinds of methods (or functions) in the programming languages like C#. There are methods that return a value. And, there are methods that do not return anything.

`System.String.Join()` happens to be a method that returns a value (a single value). It combines the elements of the second array argument with the string/char of the first argument, and it returns the concatenated string. In this example, the returned string value is assigned to the variable `name`.

![](bbox=[0.1, 0.5, 0.15, 0.56])

`System.Console.WriteLine()`, however, does not return any value. Outputting the argument string to the console is merely a "side effect" of calling this method. Since this method does not return any value, the only reason for calling this method is for the side effect. Just to be clear, the methods that return a value can also have side effects. Because of this, in general, the methods/functions in the imperative programming languages like C# are not "real functions" (in the mathematical sense).

C# is a compiled language. In particular, the `dotnet build` command on .NET (version 5 or 6, or later) generates an executable for the given machine architecture (e.g., of the machine where the build is done), as well as an IL assembly for the .NET