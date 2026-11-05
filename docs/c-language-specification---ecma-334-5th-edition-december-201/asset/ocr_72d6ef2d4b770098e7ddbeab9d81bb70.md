# 7.4.2 Unicode character escape sequences

A Unicode escape sequence represents a Unicode code point. Unicode escape sequences are processed in identifiers (§7.4.3), character literals (§7.4.5), and regular string literals (§7.4.5.6). A Unicode escape sequence is not processed in any other location (for example, to form an operator, punctuator, or keyword).

```
unicode-escape-sequence::
\u hex-digit hex-digit hex-digit hex-digit
\U hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit
```

A Unicode character escape sequence represents the single Unicode code point formed by the hexadecimal number following the "\u" or "\U" characters. Since C# uses a 16-bit encoding of Unicode code points in character and string values, a Unicode code point in the range U+10000 to U+10FFFF is represented using two Unicode surrogate code units. Unicode code points above U+FFFF are not permitted in character literals. Unicode code points above U+10FFFF are invalid and are not supported.

Multiple translations are not performed. For instance, the string literal "\u005C\u005C" is equivalent to "\u005C" rather than "\". [Note: The Unicode value \u005C is the character "\". end note]

[Example] The example

```
class Class1
{
    static void Test(bool \u0066) {
        char c = '\u0066';
        if (\u0066)
            System.Console.WriteLine(c.ToString());
    }
}
```

shows several uses of \u0066, which is the escape sequence for the letter "F". The program is equivalent to

```
class Class1
{
    static void Test(bool f) {
        char c = 'f';
        if (f)
            System.Console.WriteLine(c.ToString());
    }
}
```

end example]

# 7.4.3 Identifiers

The rules for identifiers given in this subclause correspond exactly to those recommended by the Unicode Standard Annex 15 except that underscore is allowed as an initial character (as is traditional in the C programming language). Unicode escape sequences are permitted in identifiers, and the "@" character is allowed as a prefix to enable keywords to be used as identifiers.

```
identifier::
    available-identifier
    @ identifier-or-keyword

available-identifier::
    An identifier-or-keyword that is not a keyword

identifier-or-keyword::
    identifier-start-character identifier-part-characters_opt

identifier-start-character::
    letter-character
    underscore-character
```