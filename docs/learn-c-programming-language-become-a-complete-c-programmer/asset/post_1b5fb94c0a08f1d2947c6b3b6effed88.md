
signed or unsigned for a plain **char** is implementation-defined. C++ provides two types for which the answer is definite: **signed char**, which can hold at least the values **−127 to 127**, and **unsigned char**, which can hold at least the values **0 to 255**. Fortunately, the difference matters only for values outside the **0 to 127** range, and the most common characters are within that range.

Values outside that range stored in a plain **char** can lead to subtle portability problems. See §6.2.3.1 if you need to use more than one type of **char** or if you store integers in **char** variables.

Note that the character types are integral types (§6.2.1) so that arithmetic and bitwise logical operations (§10.3) apply. For example:

```
void digits()
{
for (int i=0; i!=10; ++i)
cout << static_cast<char>('0'+i);
}
```

This is a way of writing the ten digits to **cout**. The character literal **‘0’** is converted to its integer value and **i** is added. The resulting **int** is then converted to a **char** and written to **cout**. Plain **‘0’+i** is an **int**, so if I had left out the **static_cast<char>**, the output would have been something like **48, 49**, and so on, rather than **0, 1**, and so on.

## 6.2.3.1 Signed and Unsigned Characters

It is implementation-defined whether a plain **char** is considered signed or unsigned. This opens the possibility for some nasty surprises and implementation dependencies. For example:

```
char c = 255; // 255 is “all ones,” hexadecimal 0xFF
int i = c;
```

What will be the value of **i**? Unfortunately, the answer is undefined. On an implementation with 8-bit bytes, the answer depends on the meaning of the “all ones” **char** bit pattern when extended into an **int**. On a machine where a **char** is unsigned, the answer is **255**. On a machine where a **char** is signed, the answer is **−1**. In this case, the compiler might warn about the conversion of the literal **255** to the **char** value **−1**. However, C++ does not offer a general mechanism for detecting this kind of problem. One solution is to avoid plain **char** and use the specific **char** types only. Unfortunately, some standard-library functions, such as **strcmp()**, take plain **chars** only (§43.4).

A **char** must behave identically to either a **signed char** or an **unsigned char**. However, the three **char** types are distinct, so you can’t mix pointers to different **char** types. For example:

```
void f(char c, signed char sc, unsigned char uc)
{
char* pc = &uc; // error : no pointer conversion
signed char* psc = pc; // error : no pointer conversion
unsigned char* puc = pc; // error : no pointer conversion
psc = puc; // error : no pointer conversion
}
```

Variables of the three char types can be freely assigned to each other. However, assigning a too large value to a signed char (§10.5.2.1) is still undefined. For example:

```
void g(char c, signed char sc, unsigned char uc)
{
c = 255; // implementation-defined if plain chars are signed and have 8 bits
```

```
c = sc; // OK
c = uc; // implementation-defined if plain chars are signed and if uc’s value is too large
sc = uc; // implementation defined if uc’s value is too large
uc = sc; // OK: conversion to unsigned
sc = c; // implementation-defined if plain chars are unsigned and if c’s value is too large
uc = c; // OK: conversion to unsigned
}
```

To be concrete, assume that a char is 8 bits:

```
signed char sc = -160;
unsigned char uc = sc; // uc == 116 (because 256-160==116)
cout << uc; // print ‘t’
```

```
char count[256]; // assume 8-bit chars
++count[sc]; // likely disaster: out-of-range access
++count[uc]; // OK
```

None of these potential problems and confusions occur if you use plain char throughout and avoid negative character values.

## 6.2.3.2 Character Literals

A character literal is a single character enclosed in single quotes, for example, ‘a’ and ‘0’. The type of a character literal is char. A character literal can be implicitly converted to its integer value in the character set of the machine on which the C++ program is to run. For example, if you are running on a machine using the ASCII character set, the value of ‘0’ is 48. The use of character literals rather than decimal notation makes programs more portable.

A few characters have standard names that use the backslash, \, as an escape character:

| Name | ASCII Name | C++ Name |
|------|------------|----------|
| Newline | NL (LF) | \n |
| Horizontal tab | HT | \t |
| Vertical tab | VT | \v |
| Backspace | BS | \b |
| Carriage return | CR | \r |
| Form feed | FF | \f |
| Alert | BEL | \a |
| Backslash | \ | \\ |
| Question mark | ? | \? |
| Single quote | ‘ | \' |
| Double quote | " | " |
| Octal number ooo | | \ooo |
| Hexadecimal number hhh | | \xhhh ... |

Despite their appearance, these are single characters.

We can represent a character from the implementation character set as a one-, two-, or three-digit octal number (\ followed by octal digits) or as a hexadecimal number (\x followed by hexadecimal digits). There is no limit to the number of hexadecimal digits in the sequence. A sequence of octal or hexadecimal digits is terminated by the first character that is not an octal digit or a hexadecimal digit, respectively. For example:

| Octal | Hexadecimal | Decimal | ASCII |
|-------|-------------|---------|-------|
| '\6' | '\x6' | 6 | ACK |
| '\60' | '\x30' | 48 | '0' |
| '\137' | '\x05f' | 95 | '_' |

This makes it possible to represent every character in the machine’s character set and, in particular, to embed such characters in character strings (see §7.3.2). Using any numeric notation for characters makes a program nonportable across machines with different character sets.

It is possible to enclose more than one character in a character literal, for example, ‘ab’. Such uses are archaic, implementation-dependent, and best avoided. The type of such a multicharacter literal is int.

When embedding a numeric constant in a string using the octal notation, it is wise always to use three digits for the number. The notation is hard enough to read without having to worry about whether or not the character after a constant is a digit. For hexadecimal constants, use two digits. Consider these examples:

```
char v1[] = "a\xah\129"; char v2[] = "a\xah\127"; char v3[] = "a\xad\127"; char v4[] = "a\xad\0127";
```

```
// 6 chars: ‘a’ ‘\xa’ ‘h’ ‘\12’ ‘9’ ‘\0’
// 5 chars: ‘a’ ‘\xa’ ‘h’ ‘\127’ ‘\0’
// 4 chars: ‘a’ ‘\xad’ ‘\127’ ‘\0’
// 5 chars: ‘a’ ‘\xad’ ‘\012’ ‘7’ ‘\0’
```

Wide character literals are of the form L’ab’ and are of type wchar_t. The number of characters between the quotes and their meanings are implementation-defined.

A C++ program can manipulate character sets that are much richer than the 127-character ASCII set, such as Unicode. Literals of such larger character sets are presented as sequences of four or eight hexadecimal digits preceded by a U or a u. For example:

```
U'\UFADEBEEF'
u'\uDEAD'
u'\xDEAD'
```

The shorter notation u'\uXXXX' is equivalent to U'\U0000XXXX' for any hexadecimal digit X. A number of hexadecimal digits different from four or eight is a lexical error. The meaning of the hexadecimal number is defined by the ISO/IEC 10646 standard and such values are called universal character names. In the C++ standard, universal character names are described in §iso.2.2, §iso.2.3, §iso.2.14.3, §iso.2.14.5, and §iso.E.

## 6.2.4 Integer Types

Like char, each integer type comes in three forms: “plain” int, signed int, and unsigned int. In addition, integers come in four sizes: short int, “plain” int, long int, and long long int. A long int can be referred to as plain long, and a long long int can be referred to as plain long long. Similarly, short is a synonym for short int, unsigned for unsigned int, and signed for signed int. No, there is no long short int equivalent to int.

The unsigned integer types are ideal for uses that treat storage as a bit array. Using an unsigned instead of an int to gain one more bit to represent positive integers is almost never a good idea. Attempts to ensure that some values are positive by declaring variables unsigned will typically be defeated by the implicit conversion rules (§10.5.1, §10.5.2.1).

Unlike plain chars, plain ints are always signed. The signed int types are simply more explicit synonyms for their plain int counterparts, rather than different types.

If you need more detailed control over integer sizes, you can use aliases from <cstdint> (§43.7), such as int64_t (a signed integer with exactly 64 bits), uint_fast16_t (an unsigned integer with exactly 8 bits, supposedly the fastest such integer), and int_least32_t (a signed integer with at least 32 bits, just like plain int). The plain integer types have well-defined minimal sizes (§6.2.8), so the <cstdint> are sometimes redundant and can be overused.

In addition to the standard integer types, an implementation may provide extended integer types (signed and unsigned). These types must behave like integers and are considered integer types when considering conversions and integer literal values, but they usually have greater range (occupy more space).

## 6.2.4.1 Integer Literals

Integer literals come in three guises: decimal, octal, and hexadecimal. Decimal literals are the most commonly used and look as you would expect them to:

7 1234 976 12345678901234567890

The compiler ought to warn about literals that are too long to represent, but an error is only guaranteed for {} initializers (§6.3.5).

A literal starting with zero followed by x or X (0x or 0X) is a hexadecimal (base 16) number. A literal starting with zero but not followed by x or X is an octal (base 8) number. For example:

| Decimal | Octal | Hexadecimal |
|---------|-------|-------------|
| 0 | 0 | 0x0 |
| 2 | 02 | 0x2 |
| 63 | 077 | 0x3f |
| 83 | 0123 | 0x63 |

The letters a, b, c, d, e, and f, or their uppercase equivalents, are used to represent 10, 11, 12, 13, 14, and 15, respectively. Octal and hexadecimal notations are most useful for expressing bit patterns. Using these notations to express genuine numbers can lead to
