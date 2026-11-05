
The prefix "@" enables the use of keywords as identifiers, which is useful when interfacing with other programming languages. The character @ is not actually part of the identifier, so the identifier might be seen in other languages as a normal identifier, without the prefix. An identifier with an @ prefix is called a verbatim identifier. Use of the @ prefix for identifiers that are not keywords is permitted, but strongly discouraged as a matter of style.

The example

```
class @class
{
    public static void @static(bool @bool) {
        if (@bool)
            System.Console.WriteLine("true");
        else
            System.Console.WriteLine("false");
    }
}

class Class1
{
    static void M() {
        cl\u0061ss.st\u0061tic(true);
    }
}
```

defines a class named "class" with a static method named "static" that takes a parameter named "bool". Note that since Unicode escapes are not permitted in keywords, the token "cl\u0061ss" is an identifier, and is the same identifier as "@class".

Two identifiers are considered the same if they are identical after the following transformations are applied, in order:

- The prefix "@", if used, is removed.
- Each unicode-escape-sequence is transformed into its corresponding Unicode character.
- Any formatting-characters are removed.

Identifiers containing two consecutive underscore characters (U+005F) are reserved for use by the implementation. For example, an implementation might provide extended keywords that begin with two underscores.

## 2.4.3 Keywords

A keyword is an identifier-like sequence of characters that is reserved, and cannot be used as an identifier except when prefaced by the @ character.

*keyword: one of*

| abstract | as | base | bool | break |
|---|---|---|---|---|
| byte | case | catch | char | checked |
| class | const | continue | decimal | default |
| delegate | do | double | else | enum |
| event | explicit | extern | false | finally |
| fixed | float | for | foreach | goto |
| if | implicit | in | int | interface |
| internal | is | lock | long | namespace |
| new | null | object | operator | out |
| override | params | private | protected | public |
| readonly | ref | return | sbyte | sealed |
| short | sizeof | stackalloc | static | string |
| struct | switch | this | throw | true |
| try | typeof | uint | ulong | unchecked |
| unsafe | ushort | using | virtual | void |
| volatile | while |  |  |  |

In some places in the grammar, specific identifiers have special meaning, but are not key-words. Such identifiers are sometimes referred to as “contextual keywords.” For example, within a property declaration, the “get” and “set” identifiers have special meaning (§10.7.2). An identifier other than get or set is never permitted in these locations, so this use does not conflict with a use of these words as identifiers. In other cases, such as with the identifier “var” in implicitly typed local variable declarations (§8.5.1), a contextual keyword can conflict with declared names. In such cases, the declared name takes precedence over the use of the identifier as a contextual keyword.

> **ERIC LIPPERT** C# has not added any new reserved keywords since its original release. All the new language features that require new keywords (yield, select, and so on) use “contextual keywords,” which are not reserved and have special meaning only in context. This decision helps preserve backward compatibility with existing programs.

> **VLADIMIR RESHETNIKOV** In case you need the full list of these contextual keywords (including supported attribute targets), here it is:
> 
> ```
> add alias ascending assembly by descending dynamic equals field from get global group into join let method module on orderby param partial property
> remove select set type typevar value var where yield
> ```

## 2.4.4 Literals

A literal is a source code representation of a value.

```
literal:
    boolean-literal
    integer-literal
    real-literal
    character-literal
    string-literal
    null-literal
```

### 2.4.4.1 Boolean Literals

There are two boolean literal values: true and false.

```
boolean-literal:
    true
    false
```

The type of a boolean-literal is bool.

### 2.4.4.2 Integer Literals

Integer literals are used to write values of types int, uint, long, and ulong. Integer literals have two possible forms: decimal and hexadecimal.

```
integer-literal:
    decimal-integer-literal
    hexadecimal-integer-literal
```

```
decimal-integer-literal:
    decimal-digits   integer-type-suffix_opt
```

```
decimal-digits:
    decimal-digit
    decimal-digits   decimal-digit
```

```
decimal-digit: one of
    0 1 2 3 4 5 6 7 8 9
```

```
integer-type-suffix: one of
    U u L l UL Ul uL ul LU Lu lU lu
```

hexadecimal-integer-literal:
0x hex-digits integer-type-suffix_opt
0X hex-digits integer-type-suffix_opt

hex-digits:
hex-digit
hex-digits hex-digit

hex-digit: one of
0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f

> **ERIC LIPPERT** C# does not support octal literals, for two reasons. First, hardly anyone uses octal literals these days. Second, if C# supported octal in the standard “leading zero means octal” format, then it would be a potential source of errors. Consider this code:
> 
> `FlightNumber = 0541;`
> 
> Clearly this expression is intended as a decimal literal, not an octal literal.

The type of an integer literal is determined as follows:

- If the literal has no suffix, it has the first of these types in which its value can be represented: int, uint, long, ulong.
- If the literal is suffixed by U or u, it has the first of these types in which its value can be represented: uint, ulong.
- If the literal is suffixed by L or l, it has the first of these types in which its value can be represented: long, ulong.
- If the literal is suffixed by UL, Ul, uL, ul, LU, Lu, lU, or lu, it is of type ulong.

If the value represented by an integer literal is outside the range of the ulong type, a compile-time error occurs.

As a matter of style, it is suggested that “L” be used instead of “l” when writing literals of type long, since it is easy to confuse the letter “l” with the digit “1”.

To permit the smallest possible int and long values to be written as decimal integer literals, the following two rules exist:

- When a decimal-integer-literal with the value 2147483648 (2^31) and no integer-type-suffix appears as the token immediately following a unary minus operator token (§7.7.2), the result is a constant of type int with the value -2147483648 (-2^31). In all other situations, such a decimal-integer-literal is of type uint.
- When a decimal-integer-literal with the value 9223372036854775808 (2^63) and no integer-type-suffix or the integer-type-suffix L or l appears as the token immediately following a unary minus operator token (§7.7.2), the result is a constant of type long with the value -9223372036854775808 (-2^63). In all other situations, such a decimal-integer-literal is of type ulong.

> **JOSEPH ALBAHARI** Thanks to implicit constant expression conversions (§6.1.8), integer literals can be assigned directly to the uint, long, and ulong types (as well as short, ushort, byte, and sbyte):
> 
> ```
> uint x = 3; long y = 3; ulong z = 3;
> ```
> 
> As a consequence, the U and L suffixes are rarely necessary. An example of when they are still useful is to force 64-bit calculations on literals that would otherwise attract 32-bit arithmetic:
> 
> ```
> long error = 1000000 * 1000000; // Compile-time error (32-bit overflow)
> long trillion = 1000000L * 1000000L; // Okay -- no overflow
> ```

### 2.4.4.3 Real Literals

Real literals are used to write values of types float, double, and decimal.

real-literal:
  decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
  . decimal-digits exponent-part_opt real-type-suffix_opt
  decimal-digits exponent-part_opt real-type-suffix_opt
  decimal-digits real-type-suffix

exponent-part:
  e sign_opt decimal-digits
  E sign_opt decimal-digits

sign: one of
  + -

real-type-suffix: one of
  F f D d M m
