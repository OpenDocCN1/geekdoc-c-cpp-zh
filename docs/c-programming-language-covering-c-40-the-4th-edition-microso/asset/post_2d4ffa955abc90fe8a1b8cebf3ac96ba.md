
### 2.4.4.4 Character Literals

A character literal represents a single character, and usually consists of a character in quotes, as in 'a'.

```
character-literal:
  ' character '
```

```
character:
  single-character
  simple-escape-sequence
  hexadecimal-escape-sequence
  unicode-escape-sequence
```

```
single-character:
  Any character except ' (U+0027), \ (U+005C), and new-line-character
```

```
simple-escape-sequence: one of
  \' \" \\ \0 \a \b \f \n \r \t \v
```

```
hexadecimal-escape-sequence:
  \x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt
```

A character that follows a backslash character (\) in a character must be one of the following characters: ', \, 0, a, b, f, n, r, t, u, U, x, v. Otherwise, a compile-time error occurs.

A hexadecimal escape sequence represents a single Unicode character, with the value formed by the hexadecimal number following "\x".

If the value represented by a character literal is greater than U+FFFF, a compile-time error occurs.

A Unicode character escape sequence (§2.4.1) in a character literal must be in the range U+0000 to U+FFFF.

A simple escape sequence represents a Unicode character encoding, as described in the table below.

| Escape Sequence | Character Name | Unicode Encoding |
|---|---|---|
| \' | Single quote | 0x0027 |
| \" | Double quote | 0x0022 |
| \\ | Backslash | 0x005C |
| `\0` | Null | `0x0000` |
| `\a` | Alert | `0x0007` |
| `\b` | Backspace | `0x0008` |
| `\f` | Form feed | `0x000C` |
| `\n` | New line | `0x000A` |
| `\r` | Carriage return | `0x000D` |
| `\t` | Horizontal tab | `0x0009` |
| `\v` | Vertical tab | `0x000B` |

The type of a *character-literal* is `char`.

### 2.4.4.5 String Literals

C# supports two forms of string literals: *regular string literals* and *verbatim string literals*.

A regular string literal consists of zero or more characters enclosed in double quotes, as in "hello", and may include both simple escape sequences (such as `\t` for the tab character), and hexadecimal and Unicode escape sequences.

A verbatim string literal consists of an @ character followed by a double-quote character, zero or more characters, and a closing double-quote character. A simple example is @"hello". In a verbatim string literal, the characters between the delimiters are interpreted verbatim, the only exception being a *quote-escape-sequence*. In particular, simple escape sequences and hexadecimal and Unicode escape sequences are not processed in verbatim string literals. A verbatim string literal may span multiple lines.

> > **JON SKEET** One aspect of verbatim string literals that makes me nervous is the way a line break will take on the form in which it occurs in the file. It's the natural option of course, but it means switching a file between "\r\n" and "\n" line breaks isn’t a purely decorative change: It can affect behavior, too.

## 2. Lexical Structure

```
string-literal:
  regular-string-literal
  verbatim-string-literal

regular-string-literal:
  " regular-string-literal-characters_opt "

regular-string-literal-characters:
  regular-string-literal-character
  regular-string-literal-characters regular-string-literal-character

regular-string-literal-character:
  single-regular-string-literal-character
  simple-escape-sequence
  hexadecimal-escape-sequence
  unicode-escape-sequence

single-regular-string-literal-character:
  Any character except " (U+0022), \ (U+005C), and new-line-character

verbatim-string-literal:
  @" verbatim-string-literal-characters_opt "

verbatim-string-literal-characters:
  verbatim-string-literal-character
  verbatim-string-literal-characters verbatim-string-literal-character

verbatim-string-literal-character:
  single-verbatim-string-literal-character
  quote-escape-sequence

single-verbatim-string-literal-character:
  Any character except "

quote-escape-sequence:
  ""
```

A character that follows a backslash character (\ ) in a regular-string-literal-character must be one of the following characters: ', ", \, 0, a, b, f, n, r, t, u, U, x, v. Otherwise, a compile-time error occurs.

### The example

```
string a = "hello, world"; // hello, world
string b = @"hello, world"; // hello, world
string c = "hello \t world"; // hello world
string d = @"hello \t world"; // hello \t world
string e = "Joe said \"Hello\" to me"; // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me"; // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt"; // \\server\share\file.txt
string h = @"\\server\share\file.txt"; // \\server\share\file.txt

string i = "one\n\r\n two\r\nthree";
string j = @"one
two
three";
```

shows a variety of string literals. The last string literal, j, is a verbatim string literal that spans multiple lines. The characters between the quotation marks, including white space such as new line characters, are preserved verbatim.

> **BRAD ABRAMS** In the early days of the C# language design, we experimented with using the backtick (`) character. Personally, I really liked this choice: The backtick is in the quote family and is a grossly underused character. In fact, it was so underused that some international keyboards don’t even include a key for it. We were lucky to have such a good, early international following for C#, which allowed us to fix this potential error very early in the design of the language.

Since a hexadecimal escape sequence can have a variable number of hex digits, the string literal "\x123" contains a single character with hex value 123. To create a string containing the character with hex value 12 followed by the character 3, one could write "\x00123" or "\x12" + "3" instead.

> **JON SKEET** Hexadecimal escape sequences aren’t just rare—they’re dangerous. While a string such as "\x9Tabbed" is reasonably clear, it’s not nearly as obvious that "\x9Badly tabbed" actually begins with the Unicode character U+9BAD.

The type of a string-literal is string.

Each string literal does not necessarily result in a new string instance. When two or more string literals that are equivalent according to the string equality operator (§7.10.7) appear in the same program, these string literals refer to the same string instance. For instance, the output produced by

```
```csharp
class Test
{
    static void Main() {
        object a = "hello";
        object b = "hello";
        System.Console.WriteLine(a == b);
    }
}
```
```

is True because the two literals refer to the same string instance.

> **JOSEPH ALBAHARI** This optimization is called *interning*. One of the benefits of interning is that it reduces the size of the compiled assembly because duplicate string literals are factored out.
> 
> In the preceding example, a and b are declared of type object, which forces the subsequent comparison to use object's reference-type equality semantics. If a and b were declared of type string, the comparison would bind to string's == operator, which evaluates to true if the strings have identical content—even if they refer to different underlying objects.

### 2.4.4.6 The null Literal

null-literal:
null

The *null-literal* can be implicitly converted to a reference type or nullable type.

> **ERIC LIPPERT** The null literal expression itself does not have a type.

### 2.4.5 Operators and Punctuators

There are several kinds of operators and punctuators. Operators are used in expressions to describe operations involving one or more operands. For example, the expression a + b uses the + operator to add the two operands a and b. Punctuators are for grouping and separating.

operator-or-punctuator: one of
{ } [ ] ( ) . , : ;
+ - * / % & ^ ! ~
= < > ? ?? :: ++ -- && ||
-> == != <= >= += -= *= /= %=
&= |= ^= << <<= =>

right-shift:
>|

right-shift-assignment:
>|=

The vertical bars in the right-shift and right-shift-assignment productions are used to indicate that, unlike other productions in the syntactic grammar, no characters of any kind (not even white space) are allowed between the tokens. These productions are treated specially to enable the correct handling of type-parameter-lists (§10.1.3).

## 2.5 Preprocessing Directives

> BILL WAGNER This section shows how the C heritage colors so much of modern development. I rarely, if ever, use any of the preprocessing directives—but I can only imagine the storm of criticism if C# had not included a strong set of preprocessing directives.

The preprocessing directives provide the ability to conditionally skip sections of source files, to report error and warning conditions, and to delineate distinct regions of source code. The term “preprocessing directives” is used only for consistency with the C and C++ programming languages. In C#, there is no separate preprocessing step; preprocessing directives are processed as part of the lexical analysis phase.

- pp-directive:
- pp-declaration
- pp-conditional
- pp-line
- pp-diagnostic
- pp-region
- pp-pragma
