

| Delimited_Comment
;

fragment Single_Line_Comment
: '//' Input_Character*
;

fragment Input_Character
// anything but New_Line_Character
: ~('\u000D' | '\u000A' | '\u0085' | '\u2028' | '\u2029')
;

fragment New_Line_Character
: '\u000D' // carriage return
| '\u000A' // line feed
| '\u0085' // next line
| '\u2028' // line separator
| '\u2029' // paragraph separator
;

fragment Delimited_Comment
: '/*' Delimited_Comment_Section* ASTERISK+ '/'
;

fragment Delimited_Comment_Section
: SLASH
| ASTERISK* Not_Slash_Or_Asterisk
;

fragment Not_Slash_Or_Asterisk
: ~('/*' | '*')  // Any except SLASH or ASTERISK
;

Comments do not nest. The character sequences /* and */ have no special meaning within a single-line comment, and the character sequences // and /* have no special meaning within a delimited comment.

Comments are not processed within character and string literals.

Note: These rules must be interpreted carefully. For instance, in the example below, the delimited comment that begins before A ends between B and C(). The reason is that

```
// B * / C();
```

is not actually a single-line comment, since // has no special meaning within a delimited comment, and so */ does have its usual special meaning in that line.

Likewise, the delimited comment starting before D ends before E. The reason is that "D * / " is not actually a string literal, since it appears inside a delimited comment.

A useful consequence of /* and */ having no special meaning within a single-line comment is that a block of source code lines can be commented out by putting // at the beginning of each line. In general it does not work to put /* before those lines and */ after them, as this does not properly encapsulate delimited comments in the block, and in general may completely change the structure of such delimited comments.

Example code:

~~~
static void Main()
{
    /* A
    // B */ C();
    Console.WriteLine(/* "D */ "E");
}
~~~

*end note*

*单行注释* 和 *定界注释* 具有特定格式，可以用作 *文档注释*，如 §D 中所述。

### 6.3.4 White space

White space is defined as any character with Unicode class Zs (which includes the space character) as well as the horizontal tab character, the vertical tab character, and the form feed character.

~~~
Whitespace
    : [\p{Zs}]  // any character with Unicode class Zs
    | '\u0009'  // horizontal tab
    | '\u000B'  // vertical tab
    | '\u000C'  // form feed
    ;
~~~

## 6.4 Tokens

### 6.4.1 General

There are several kinds of *tokens*: identifiers, keywords, literals, operators, and punctuators. White space and comments are not tokens, though they act as separators for tokens.

~~~
token
    : identifier
    | keyword
    | Integer_Literal
    | Real_Literal
    | Character_Literal
    | String_Literal
    | operator_or_punctuator
    ;
~~~

*Note: This is an ANTLR parser rule, it does not define a lexical token but rather the collection of token kinds. end note*

### 6.4.2 Unicode character escape sequences

A Unicode escape sequence represents a Unicode code point. Unicode escape sequences are processed in identifiers (§6.4.3), character literals (§6.4.5.5), regular string literals (§6.4.5.6), and interpolated regular string expressions (§11.7.3). A Unicode escape sequence is not processed in any other location (for example, to form an operator, punctuator, or keyword).

~~~
fragment Unicode_Escape_Sequence
    : '\\u' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
    | '\\U' Hex_Digit Hex_Digit Hex_Digit Hex_Digit Hex_Digit Hex_Digit Hex_Digit
    Hex_Digit
    ;
~~~

A Unicode character escape sequence represents the single Unicode code point formed by the hexadecimal number following the "\u" or "\U" characters. Since C# uses a 16-bit encoding of Unicode code points in character and string values, a Unicode code point in the range U+10000 to U+10FFFF is represented using two Unicode surrogate code units. Unicode code points above U+FFFF are not permitted in character literals. Unicode code points above U+10FFFF are invalid and are not supported.

Multiple translations are not performed. For instance, the string literal "\u005Cu005C" is equivalent to "\u005C" rather than "\\".

> Note: The Unicode value \u005C is the character "\" . end note

Example: The example

```
class Class1
{
    static void Test(bool \u0066)
    {
        char c = '\u0066';
        if (\u0066)
        {
            System.Console.WriteLine(c.ToString());
        }
    }
}
```

shows several uses of \u0066, which is the escape sequence for the letter "f". The program is equivalent to

```
class Class1
{
    static void Test(bool f)
    {
        char c = 'f';
        if (f)
        {
            System.Console.WriteLine(c.ToString());
        }
    }
}
```

end example

### 6.4.3 Identifiers

The rules for identifiers given in this subclause correspond exactly to those recommended by the Unicode Standard Annex 15 except that underscore is allowed as an initial character (as is traditional in the C programming language), Unicode escape sequences are permitted in identifiers, and the "@" character is allowed as a prefix to enable keywords to be used as identifiers.

identifier
: Simple_Identifier
| contextual_keyword
;

Simple_Identifier
: Available_Identifier
| Escaped_Identifier

```
fragment Available_Identifier
  : Basic_Identifier    // excluding keywords or contextual keywords, see note below
;
fragment Escaped_Identifier
  // Includes keywords and contextual keywords prefixed by '@'. See note below.
  : '@' Basic_Identifier
;
fragment Basic_Identifier
  : Identifier_Start_Character Identifier_Part_Character*
;
fragment Identifier_Start_Character
  : Letter_Character
  | Underscore_Character
;
fragment Underscore_Character
  : '_'    // underscore
  | '\\u005F' // Unicode_Escape_Sequence for underscore
;
fragment Identifier_Part_Character
  : Letter_Character
  | Decimal_Digit_Character
  | Connecting_Character
  | Combining_Character
  | Formatting_Character
;
fragment Letter_Character
  // Category Letter, all subcategories; category Number, subcategory letter.
  : [\\p{L}|\\p{Nl}]
  // Only escapes for categories L & Nl allowed. See note below.
  | Unicode_Escape_Sequence
;
fragment Combining_Character
  // Category Mark, subcategories non-spacing and spacing combining.
  : [\\p{Mn}\\p{Mc}]
  // Only escapes for categories Mn & Mc allowed. See note below.
  | Unicode_Escape_Sequence
;
fragment Decimal_Digit_Character
  // Category Number, subcategory decimal digit.
  : [\\p{Nd}]
  // Only escapes for category Nd allowed. See note below.
  | Unicode_Escape_Sequence
;
```

fragment Connecting_Character
// Category Punctuation, subcategory connector.
// [\p{Pc}]
// Only escapes for category Pc allowed. See note below.
| Unicode_Escape_Sequence
;

fragment Formatting_Character
// Category Other, subcategory format.
// [\p{Cf}]
// Only escapes for category Cf allowed, see note below.
| Unicode_Escape_Sequence
;

Note:

- For information on the Unicode character classes mentioned above, see *The Unicode Standard*.
- The fragment *Available_Identifier* requires the exclusion of keywords and contextual keywords. If the grammar in this Standard is processed with ANTLR then this exclusion is handled automatically by the semantics of ANTLR:
  - Keywords and contextual keywords occur in the grammar as literal strings.
  - ANTLR creates implicit lexical token rules are created from these literal strings.
  - ANTLR considers these implicit rules before the explicit lexical rules in the grammar.
  - Therefore fragment *Available_Identifier* will not match keywords or contextual keywords as the lexical rules for those precede it.
- Fragment *Escaped_Identifier* includes escaped keywords and contextual keywords as they are part of the longer token starting with an @ and lexical processing always forms the longest possible lexical element (§6.3.1).
- How an implementation enforces the restrictions on the allowable *Unicode_Escape_Sequence* values is an implementation issue.

end note

*Example:* Examples of valid identifiers are `identifier1`, `_identifier2`, and `@if`. end example

An identifier in a conforming program shall be in the canonical format defined by Unicode Normalization Form C, as defined by Unicode Standard Annex 15. The behavior when encountering an identifier not in Normalization Form C is implementation-defined; however, a diagnostic is not required.

The prefix "@" enables the use of keywords as identifiers, which is useful when interfacing with other programming languages. The character @ is not actually part of the identifier, so the identifier might be seen in other languages as a normal identifier, without the prefix. An identifier with an @ prefix is called a *verbatim identifier*.

*Note:* Use of the @ prefix for identifiers that are not keywords is permitted, but strongly discouraged as a matter of style. end note

*Example:* The example:

```
class @class
{
    public static void @static(bool @bool)
    {
```
