
- 0900—Incorrect representation as zero cannot be the leading digit in decimal number representation when the number of digits is more than one
- 235-897—We cannot specify a range of decimal numbers in a decimal constant

In an octal integer constant, the digits are taken from the range 0 to 7. The first digit of an octal constant must be zero. Some examples of valid and invalid octal constants are as follows:

- 0—Valid
- 012—Valid
- 345—Invalid octal number as it does not begin with a zero
- 0989—Invalid as the digits are greater than 7
- 056.66—Invalid character (.)

In a hexadecimal representation, a constant must start with a 0x or 0X. It can be followed by any combination of digits ranging from 0-9 and a to f (both the upper case and lower case) where the characters a to f represent numbers from 10 to 15, respectively. Some valid and invalid hexadecimal constant representations are:

- 0x—Valid
- 0X—Valid
- 0x7aff—Valid
- 0xdcba—Valid
- 0adf—Invalid as it doesn’t start with 0x or 0X
- 0xqdg—The hex range is from a to f so g is not supported
- 0xff.44—Illegal character (.)

The range of an integer constant varies from one compiler to another but typically the length of an integer constant was defined to not more than 32,767, which is 2¹⁵ - 1. For octal constants, the range becomes 77777 and for hex constants, the range becomes 7FFF. Unsigned integer constants are also present in C. The range of an unsigned constant is double that of a signed constant. A signed constant could be declared as an unsigned constant by appending a U at its end. Similarly, we have long integer constants, which extend the range of an integer constant even more. They can be identified by appending an L at the end of a signed constant. Some examples of unsigned and long integer constants are:

- 60787U—Unsigned decimal
- 874329872L—Long decimal
- 2345678123UL—Unsigned long decimal
- 0123456L—Long octal
- 0777777UL—Unsigned octal
- 0xFFFFFFFL—Long hexadecimal
- 0xAD3467665UL—Unsigned long hexadecimal

## Floating Point Constant

A floating point constant is defined as a numeric constant, containing both the integer part and the exponential part. Some examples of the floating point constant are as follows:

0.0, 0.2, 875.3455, 1.666E+5, 2E-6, 0.0006e-3

The following are some invalid floating point representations:

- 1—Invalid as floating point must contain an exponent
- 1,777—Invalid as (,) is not an allowed character
- 5E+10.3—Exponent should be an integer
- 4E 6—Blank space is not allowed before an exponent

The exponent part of a floating point constant shifts the decimal point to the right if its value is positive, or to the left if the value is negative. The range of a floating point constant is much larger than that of an integer constant. Floating point constants are also treated as double precision quantities and require 8 bytes of storage. Some compilers also allow a single-precision floating point constant by appending an F at the end of a floating point constant. We can also mention a long floating point by appending an L at the end of a floating point variable.

Both floating point and integer fall under a larger section of numeric constant. Compiler fits a numeric constant into a smallest compatible data type that will hold it. It means that if we declare a constant as 15, it becomes an integer by default but a constant like 156899 becomes a long integer.

## Character Constants

A character constant is defined as a single character enclosed within apostrophes, such as ‘A’ and ‘D’. All character constants contain integer values associated with them based on the character set of a machine. Standards of character sets can vary from computer to computer. For this reason, C follows a unanimously accepted character set, which is also known as American Standard Code for Information Interchange (ASCII) where each character is provided with a unique numeric value that differentiates it from others. Table 1.4 defines the ASCII character set and its corresponding decimal values:

**Table 1.4: ASCII Character Set and Its Corresponding Decimal Values**

| ASCII value | Character | ASCII value | Character | ASCII value | Character | ASCII value | Character |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | NUL | 32 | (blank) | 64 | @ | 96 | \` |
| 1 | SOH | 33 | ! | 65 | A | 97 | a |
| 2 | STX | 34 | " | 66 | B | 98 | b |
| 3 | ETX | 35 | # | 67 | C | 99 | c |
| 4 | EOT | 36 | $ | 68 | D | 100 | d |
| 5 | ENQ | 37 | % | 69 | E | 101 | e |
| 6 | ACK | 38 | & | 70 | F | 102 | f |
| 7 | BEL | 39 | ' | 71 | G | 103 | g |
| 8 | BS | 40 | ( | 72 | H | 104 | h |
| 9 | HT | 41 | ) | 73 | I | 105 | i |
| 10 | LF | 42 | * | 74 | J | 106 | j |
| 11 | VT | 43 | + | 75 | K | 107 | k |
| 12 | FF | 44 | , | 76 | L | 108 | l |
| 13 | CR | 45 | - | 77 | M | 109 | m |
| 14 | SO | 46 | . | 78 | N | 110 | n |
| 15 | SI | 47 | / | 79 | O | 111 | o |
| 16 | DLE | 48 | 0 | 80 | P | 112 | p |
| 17 | DC1 | 49 | 1 | 81 | Q | 113 | q |
| 18 | DC2 | 50 | 2 | 82 | R | 114 | r |
| 19 | DC3 | 51 | 3 | 83 | S | 115 | s |
| 20 | DC4 | 52 | 4 | 84 | T | 116 | t |
| 21 | NAK | 53 | 5 | 85 | U | 117 | u |
| 22 | SYN | 54 | 6 | 86 | V | 118 | v |
| 23 | ETB | 55 | 7 | 87 | W | 119 | w |
| 24 | CAN | 56 | 8 | 88 | X | 120 | x |
| 25 | EM | 57 | 9 | 89 | Y | 121 | y |
| 26 | SUB | 58 | : | 90 | Z | 122 | z |
| 27 | ESC | 59 | ; | 91 | [ | 123 | { |
| 28 | FS | 60 | < | 92 | \\ | 124 | \| |
| 29 | GS | 61 | = | 93 | ] | 125 | } |
| 30 | RS | 62 | > | 94 | ^ | 126 | ~ |
| 31 | US | 63 | ? | 95 | _ | 127 | DEL |

It is also possible to define a multibyte character constant. Multibyte constants are required for those languages which define wide character sets. To specify a multibyte character constant, we need to enclose multiple characters within a single quote like 'xy'. For wide characters, we need to precede the character with an L, such as:

```c
wchar_t wc = L'Q';
```

Here, wc is assigned a wide character constant which is equivalent to Q. The character type is wchar, which signifies a wide character type and is defined in the <stddef.h> header file. This is not a built-in data type.

## String Constants

Another set of constants supported by C is of string constants. String is a set of characters enclosed in double quotes. For example "hello world" forms a string. Although C allows to define string constants but doesn't allow to use it as a data type. The compiler automatically places a NULL (\0) at the end of a string constant. NULL signifies termination of a string constant. While using a string constant, one should not mix it with character constants, for example 'A' describes a character constant while "A" describes a string constant that contains a single character. Both are different from each other.

## Backslash Character Constants

We can write character constants in C by enclosing them inside single quotes. This rule does not seem to apply to all the character constants. Few character constants like carriage return needs special handling. It requires enclosing the character constants within single quotes and preceding the character constants with a backslash. These are also referred to as escape sequences. Escape sequences are always denoted by multiple characters. Table 1.5 lists the escape sequences in C:

- `-` : Used for subtraction
- `*` : Used for multiplication
- `/` : Used for division
- `%` : Used to find out the remainder, also known as the modulus operator

Other operations, such as exponentiation and logarithmic computation are done by library functions that are defined in the internal header files of C. The operands on which the operators work must contain numeric values, so the operands can be of type integers, floating point variables, or characters. While mentioning characters, it is actually their ASCII values that are taken into account. For using the modulus operator, both the numerator and denominator should be of the integer type. Division operation on integer variables always results in truncated values, as the decimal portion of the quotient is dropped. In order to avoid this truncation, it is advisable to store the result of a division operation in a floating point variable.

Assume that several integer operations are taking place on variables a and b whose values are 20 and 7, respectively. The result would be shown as:

| Expression | Value |
|---|---|
| a + b | 27 |
| a - b | 13 |
| a * b | 140 |
| a / b | 2 |
| a % b | 6 |

The a%b operation shows that truncation of result has taken place for the integer division. Now, let's consider operating on floating point variables a and b, whose values are 36.89 and 12.25, respectively. In this case, the result would appear as follows:

| Expression | Value |
|---|---|
| a + b | 49.14 |
| a - b | 24.64 |
| a * b | 451.9025 |
| a / b | 3.011 |

Let's execute the same set of operations on two character variables, ch1 and ch2, whose content will be A and B, respectively. The result would appear as follows:

| Expression | Value |
|---|---|
| ch1 + ch2 | 131 |
| ch1 - ch2 | -1 |

When arithmetic operations are done on character variables, it is actually the ASCII values which are taken into account. The following is the list of some truncation rules that must be followed while performing a floating point operation:

- The operand with a lower precision will be converted to the precision of another operand and the result will be expressed in a higher precision. It means for an operation between a float and a double, the result will be expressed in double.
- If one of the operand is a floating point and the other is an integer or a character, the char or int operand will be converted into a floating point variable.
- If operations are made between an int and a long int, the result will be shown in the long int.
