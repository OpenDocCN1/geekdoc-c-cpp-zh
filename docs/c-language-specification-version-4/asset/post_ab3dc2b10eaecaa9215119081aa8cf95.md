
real-literal:
  decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
  . decimal-digits exponent-part_opt real-type-suffix_opt
  decimal-digits exponent-part real-type-suffix_opt
  decimal-digits real-type-suffix

exponent-part:
  e sign_opt decimal-digits
  E sign_opt decimal-digits

sign: one of
  +  -

real-type-suffix: one of
  F f D d M m

If no real-type-suffix is specified, the type of the real literal is double. Otherwise, the real type suffix determines the type of the real literal, as follows:

- A real literal suffixed by F or f is of type float. For example, the literals 1f, 1.5f, 1e10f, and 123.456F are all of type float.
- A real literal suffixed by D or d is of type double. For example, the literals 1d, 1.5d, 1e10d, and 123.456D are all of type double.
- A real literal suffixed by M or m is of type decimal. For example, the literals 1m, 1.5m, 1e10m, and 123.456M are all of type decimal. This literal is converted to a decimal value by taking the exact value, and, if necessary, rounding to the nearest representable value using banker's rounding (§4.1.7). Any scale apparent in the literal is preserved unless the value is rounded or the value is zero (in which latter case the sign and scale will be 0). Hence, the literal 2.900m will be parsed to form the decimal with sign 0, coefficient 2900, and scale 3.

If the specified literal cannot be represented in the indicated type, a compile-time error occurs.

The value of a real literal of type float or double is determined by using the IEEE "round to nearest" mode.

Note that in a real literal, decimal digits are always required after the decimal point. For example, 1.3F is a real literal but 1.F is not.

## 2.4.4.4 Character literals

A character literal represents a single character, and usually consists of a character in quotes, as in 'a'.

```
character-literal:
  ' character '

character:
  single-character
  simple-escape-sequence
  hexadecimal-escape-sequence
  unicode-escape-sequence

single-character:
  Any character except ' (U+0027), \ (U+005C), and new-line-character

simple-escape-sequence: one of
  \' \" \\ \0 \a \b \f \n \r \t \v

hexadecimal-escape-sequence:
  \x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt
```

A character that follows a backslash character (\) in a character must be one of the following characters: ', ", \\, 0, a, b, f, n, r, t, u, U, x, v. Otherwise, a compile-time error occurs.

A hexadecimal escape sequence represents a single Unicode character, with the value formed by the hexadecimal number following "\x".

If the value represented by a character literal is greater than U+FFFF, a compile-time error occurs.

A Unicode character escape sequence (§2.4.1) in a character literal must be in the range U+0000 to U+FFFF.

A simple escape sequence represents a Unicode character encoding, as described in the table below.

| Escape sequence | Character name | Unicode encoding |
|---|---|---|
| \' | Single quote | 0x0027 |
| \" | Double quote | 0x0022 |
| \\ | Backslash | 0x005C |
| \0 | Null | 0x0000 |
| \a | Alert | 0x0007 |
| \b | Backspace | 0x0008 |
| \f | Form feed | 0x000C |
| \n | New line | 0x000A |
| \r | Carriage return | 0x000D |
| \t | Horizontal tab | 0x0009 |
| \v | Vertical tab | 0x000B |

The type of a character-literal is char.

## 2.4.4.5 String literals

C# supports two forms of string literals: regular string literals and verbatim string literals.

A regular string literal consists of zero or more characters enclosed in double quotes, as in "hello", and may include both simple escape sequences (such as \t for the tab character), and hexadecimal and Unicode escape sequences.

A verbatim string literal consists of an @ character followed by a double-quote character, zero or more characters, and a closing double-quote character. A simple example is @"hello". In a verbatim string literal, the characters between the delimiters are interpreted verbatim, the only exception being a quote-escape-sequence. In particular, simple escape sequences, and hexadecimal and Unicode escape sequences are not processed in verbatim string literals. A verbatim string literal may span multiple lines.

```
string-literal:
    regular-string-literal
    verbatim-string-literal

regular-string-literal:
    " regular-string-literal-characters_opt "
```

regular-string-literal-characters:
    regular-string-literal-character
    regular-string-literal-characters   regular-string-literal-character

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
    verbatim-string-literal-characters   verbatim-string-literal-character

verbatim-string-literal-character:
    single-verbatim-string-literal-character
    quote-escape-sequence

single-verbatim-string-literal-character:
    Any character except "

quote-escape-sequence:
    ""

A character that follows a backslash character (\) in a regular-string-literal-character must be one of the following characters: ', ", \, 0, a, b, f, n, r, t, u, U, x, v. Otherwise, a compile-time error occurs.

The example

```csharp
string a = "hello, world";                   // hello, world
string b = @"hello, world";                  // hello, world
string c = "hello \t world";                 // hello    world
string d = @"hello \t world";                // hello \t world
string e = "Joe said \"Hello\" to me";       // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me";      // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt";    // \\server\share\file.txt
string h = @"\\server\share\file.txt";       // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

shows a variety of string literals. The last string literal, j, is a verbatim string literal that spans multiple lines. The characters between the quotation marks, including white space such as new line characters, are preserved verbatim.

Since a hexadecimal escape sequence can have a variable number of hex digits, the string literal "\x123" contains a single character with hex value 123. To create a string containing the character with hex value 12 followed by the character 3, one could write "\x00123" or "\x12" + "3" instead.

The type of a string-literal is string.

## 2.4.4.6 The null literal

```
null-literal:
    null
```

The null-literal can be implicitly converted to a reference type or nullable type.

## 2.4.5 Operators and punctuators

There are several kinds of operators and punctuators. Operators are used in expressions to describe operations involving one or more operands. For example, the expression a + b uses the + operator to add the two operands a and b. Punctuators are for grouping and separating.

operator-or-punctuator: one of
{ } [ ] ( ) . , : ;
+ - * / % & | ^ ! ~
= < > ? ?? :: ++ --
-> == != <= >= += -= *=
&= |= ^= <<= >>= =>

```
right-shift:
    >|>
```

```
right-shift-assignment:
    >|=
```

The vertical bar in the right-shift and right-shift-assignment productions are used to indicate that, unlike other productions in the syntactic grammar, no characters of any kind (not even whitespace) are allowed between the tokens. These productions are treated specially in order to enable the correct handling of type-parameter-lists (§10.1.3).

## 2.5 Pre-processing directives

The pre-processing directives provide the ability to conditionally skip sections of source files, to report error and warning conditions, and to delineate distinct regions of source code. The term "pre-processing directives" is used only for consistency with the C and C++ programming languages. In C#, there is no separate pre-processing step; pre-processing directives are processed as part of the lexical analysis phase.

pp-directive:
- pp-declaration
- pp-conditional
- pp-line
- pp-diagnostic
- pp-region
- pp-pragma
