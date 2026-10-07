# Fundamental Numeric Types

+   - Numeric literals with no suffix resolve to the first data type that can store the value, in this order: int, uint, long, and ulong.

+   - Numeric literals with the suffix U resolve to the first data type that can store the value, in the order uint and then ulong.

+   - Numeric literals with the suffix L resolve to the first data type that can store the value, in the long order and then ulong.

+   - If the numeric literal has the suffix UL or LU, it is of type ulong.

Note that suffixes for literals are case insensitive. However, uppercase is generally preferred to avoid any ambiguity between the lowercase l and the digit 1.

> ### Guidelines
DO use uppercase literal suffixes (e.g., 1.618033988749895M).

On occasion, numbers can get large and difficult to read. To overcome the readability problem, C# 7.0 added support for a digit separator, an underscore (_), when expressing a numeric literal, as shown in Listing 2.4.

# Listing 2.4: Specifying Digit Separator

```
Console.WriteLine(9_814_072_356M);
```

In this case, we separate the digits into thousands (threes), but this is not required by C#. You can use the digit separator to create whatever grouping you like as long as the underscore occurs between the first and last digits. In fact, you can even have multiple underscores side by side—with no digit between them.

In addition, you may wish to use exponential notation instead of writing out several zeros before after the decimal point (using a digit separator or not). To use exponential notation, supply the e or E infix, follow the infix character with a positive or negative integer number, and complete the literal with the appropriate data type suffix. For example, you could print Avogadro's number as a float, as shown in Listing 2.5 and Output 2.4.