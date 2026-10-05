illustrates some of the ways in which the WriteLine method is defined in the Console class:

Click here to view code image

```
class Console
{
    public static void WriteLine(Int32 value)
    public static void WriteLine(Double value)
    public static void WriteLine(Decimal value)
    public static void WriteLine(Boolean value)
    ...
    public static void WriteLine(String value)
}
```

# Note

The documentation for the WriteLine method uses the structure types defined in the System namespace for its parameters rather than the C# aliases. For example, the overload that prints out the value for an int actually takes Int32 as the parameter. Refer to Chapter 9, “Creating value types with enumerations and structures,” for a list of the structure types and their mappings to C# aliases for these types.

As useful as overloading, it doesn’t cover every case. In particular, overloading doesn’t easily handle a situation in which the type of parameters doesn’t vary, but the number of parameters does. For example, if you want to write many values to the console? Do you have to provide versions of Console.WriteLine that can take two parameters of various combinations, other versions that can take three parameters, and so on? That would quickly become tedious. And wouldn’t the massive duplication of these overloaded methods worry you? It should.

Fortunately, there’s a way to write a method that takes a variable number of arguments (a variadic method): you can use a parameter array, which is declared by using the params keyword. To understand how params arrays