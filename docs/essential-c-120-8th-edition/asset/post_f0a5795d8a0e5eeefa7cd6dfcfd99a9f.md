
## Character Type (char)

A char type represents 16-bit characters whose set of possible values are drawn from the Unicode character set's UTF-16 encoding. A char is the same size as a 16-bit unsigned integer (ushort), which represents values between 0 and 65,535. However, char is a unique type in C# and code should treat it as such.

The BCL name for char is System.Char.

## BEGINNER TOPIC

## The Unicode Standard

Unicode is an international standard for representing characters found in most human languages. It provides computer systems with functionality for building localized applications—that is, applications that display the appropriate language and culture characteristics for different cultures.

## ADVANCED TOPIC

## 16 Bits Is Too Small for All Unicode Characters

Unfortunately, not all Unicode characters can be represented by just one 16-bit char. The original Unicode designers believed that 16 bits would be enough, but as more languages were supported, it was realized that this assumption was incorrect. As a result, some (rarely used) Unicode characters are composed of “surrogate pairs" of two char values.

To construct a literal char, place the character within single quotes, as in 'A'. Allowable characters comprise the full range of ANSI keyboard characters, including letters, numbers, and special symbols.

Some characters cannot be placed directly into the source code and instead require special handling. These characters are prefixed with a backslash (\ followed by a special character code. In combination, the backslash and special character code constitute an escape sequence. For example, \n represents a newline.

\t represents a tab. Since a backslash indicates the beginning of an escape sequence, it can no longer identify a simple backslash; instead, you need to use \\ to represent a single backslash character.

Listing 2.11 writes out one single quote because the character represented by '\' corresponds to a single quote.

## Listing 2.11: Displaying a Single Quote Using an Escape Sequence

```c
public class SingleQuote {
    public static void Main() {
        Console.WriteLine('''');
    }
}
```

In addition to showing the escape sequences, Table 2.5 includes the Unicode representation of characters.

## TABLE 2.5: Escape Characters

| Escape Sequence | Character Name | Unicode Encoding |
|---|---|---|
| \' | Single quote | \u0027 |
| \" | Double quote | \u0022 |
| \\ | Backslash | \u005C |
| \0 | Null character | \u0000 |
| \a | Alert (system beep) | \u0007 |
| \b | Backspace | \u0008 |
| \f | Form feed | \u000C |
| \n | Line feed (often referred to as a newline) | \u000A |
| \r | Carriage return | \u000D |
| \t | Horizontal tab | \u0009 |
| \v | Vertical tab | \u000B |

## Chapter 2: Data Types

## TABLE 2.5: Escape Characters (continued)

| Escape Sequence | Character Name | Unicode Encoding |
|---|---|---|
| \xxxx | Unicode character in hexadecimal | \u0029 |
| \x[n][n][n] | Unicode character in hex (first three placeholders are optional); variable-length version of \xxxx | \u03A |
| \U00xxxx, | Unicode sequence for creating surrogate pairs (max supported sequence is \u0010FFFF) | \U0020100 (廻) |
| \xxxx'\xxxx | Unicode sequence for creating surrogate pairs by \u0010FFFF | \uD83D\uDE00 (😊) |

You can represent any character using Unicode encoding. To do so, prefix the Unicode value with \u. You represent Unicode characters in hexadecimal notation. The letter A, for example, is the hexadecimal value 0x41. Listing 2.12 uses Unicode characters to display a smiley face (:), and Output 2.8 shows the results.

## LISTING 2.12: Using Encoding to Display a Smiley Face

```csharp
Console.Write("\:\');
Console.WriteLine("\)\');
```

## OUTPUT 2.8

```
:)
```

## Strings

A finite sequence of zero or more characters is called a string. The C# keyword is string, whose BCL name is System.String. The string type includes some special characteristics that may be unexpected to developers familiar with other programming languages. In addition to the string literal format discussed in Chapter 1, strings include a “verbatim string” prefix character of @, support for string interpolation with the \ prefix character, and the potentially surprising fact that strings are immutable. In C# 11, raw string literals were also added to the language.

## Literals

You can enter a literal string into code by placing the text in double quotes (""), as you saw in the HelloWorld program. Strings are composed of characters, and consequently, character escape sequences can be embedded within a string.

In Listing 2.13, two lines of text are displayed. However, instead of using Console.WriteLine(), the code list shows Console.Write() with the newline character, \n. Output 2.9 shows the results.

## LISTING 2.13: Using \ Character to Insert a Newline

```csharp
Console.Write("\n  "Truly, you have a");
```

## OUTPUT 2.9

```
Truly, you have a
newline
```

## LISTING 2.14: Displaying a Triangle Using a Verbatim String

```csharp
Console.Write(@"
Begin
End");
```

## OUTPUT 2.10

![OUTPUT 2.10](img/ffe0f34e7523830427369001d17102.png)

Without the @ character, this code would not compile. In fact, even if you changed the shape to square, the code still would not compile. The only escape sequence the verbatim string supports is "", which signifies a single set of double quotes.

## Language Contrast: C++—String Concatenation at Compile Time

Unlike C++, C# does not automatically concatenate literals. You cannot, for example, specify a string as follows:

"Major Strasser has been shot."
"Round up the usual suspects."

Rather, concatenation requires the use of the addition operator (+). If the compiler can calculate the result at compile time, however, the resultant CIL code will be a single string.

If the same literal string appears within an assembly multiple times, the compiler will define the string only once and all variables will refer to the same.
