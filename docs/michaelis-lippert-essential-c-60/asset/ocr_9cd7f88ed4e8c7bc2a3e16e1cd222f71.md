The escape sequence for double quotes differentiates the printed double quotes from the double quotes that define the beginning and end of the string.

In C#, you can use the @ symbol in front of a string to signify that a backslash should not be interpreted as the beginning of an escape sequence. The resultant **verbatim string literal** does not reinterpret just the backslash character. Whitespace is also taken verbatim when using the @ string syntax. The triangle in Listing 2.12, for example, appears in the console exactly as typed, including the backslashes, newlines, and indentation. Output 2.10 shows the results.

```
```csharp
class Triangle
{
    static void Main()
    {
        System.Console.Write(@"begin
             /\\
            /  \\
           /    \\
          /______\\
end");
    }
}
```
```

```
```text
begin
       /\\
      /  \\
     /    \\
    /______\\
end
```
```

Without the @ character, this code would not even compile. In fact, even if you changed the shape to a square, eliminating the backslashes, the code still would not compile because a newline cannot be placed directly within a string that is not prefaced with the @ symbol.

The only escape sequence the verbatim string does support is `"`, which signifies double quotes and does not terminate the string.