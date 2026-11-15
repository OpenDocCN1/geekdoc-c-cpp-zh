# TABLE 2.4: Escape Characters (Continued)

| Escape Sequence | Character Name | Unicode Encoding |
|---|---|---|
| \r | Carriage return | \u000D |
| \t | Horizontal tab | \u0009 |
| \v | Vertical tab | \u0008 |
| \uxxxx | Unicode character in hex | \u0029 |
| \x[n][n][n]n | Unicode character in hex (first three placeholders are options; variable length version of \uxxxx) | \u3A |
| \Uxxxxxxxx | Unicode escape sequence for creating surrogate pairs | \UD840DC01 (𠮷) |

You can represent any character using Unicode encoding. To do so, prefix the Unicode value with \u. You represent Unicode characters in hexadecimal notation. The letter A, for example, is the hexadecimal value 0x41. Listing 2.10 uses Unicode characters to display a smiley face (:)), and Output 2.8 shows the results.

# LISTING 2.10: Using Unicode Encoding to Display a Smiley Face

```
System.Console.Write('\u003A');
System.Console.WriteLine('\u0029');
```

# OUTPUT 2.8:

:)

# Strings

The fundamental string type in C# is the data type string, whose BCL name is System.String. The string includes some special characteristics that may be unexpected to developers familiar with other programming languages. The characteristics include a string verbatim prefix character, @, and the fact that a string is immutable.