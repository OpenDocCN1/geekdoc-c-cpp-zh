# **TABLE 8.1 C# Character Escape Sequences**

| Escape Sequence | Description |
| :--- | :--- |
| \ ' | Single quote, used for character literals. |
| \ " | Double quote, used for string literals. |
| \\ | Backslash. |
| \0 | Unicode character 0. |
| \a | Alert (char 7). |
| \b | Backspace (char 8). |
| \f | Form Feed (char 12). |
| \n | New Line (char 10). |
| \r | Carriage Return (char 13). |
| \t | Horizontal Tab (char 9). |
| \v | Vertical Quote (char 11). |
| \uxxxx | Unicode escape sequence for a character with a hexadecimal value xxxx. Also a variable-length version can contain 1 to 4 numeric values. |
| \uxxxxxxxx | Unicode escape sequence for a character with a hexadecimal value xxxxxxxx, used for generating Unicode surrogates. |

When the compiler encounters a verbatim string literal, it translates that literal in to the properly escaped string literal. Listing 8.1 shows four different strings. The first two declarations are equivalent, although the verbatim string literal is generally easier to read. The second two declarations are also equivalent, where multiplines2 represents the translated string literal.

# **LISTING 8.1 String Literals**

```
```text
string stringLiteral = "C:\\Program Files\Microsoft Visual Studio 10\\VC#";
string verbatimLiteral = @"C:\Program Files\Microsoft Visual Studio 10\VC#";

string multiplines = @"This is a ""line"" of text.
And this is the second line.";
string multiplines2 =
"\"This is a \"\"line\"\" of text.\nAnd this is the second line.";
```
```