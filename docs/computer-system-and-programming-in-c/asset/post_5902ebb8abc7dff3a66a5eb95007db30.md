
## Using Assignment Statement

The values are assigned just after the declarations are made.

### Example

```
int a, b, c;
a = 1000;
b = 0.4e-5;
c = 'a';
```

## CONSTANTS

A constant is an identifier whose value cannot be changed throughout the execution of a program whereas the variable value keeps on changing.

### C Constants Classification

C constants can be divided into two major categories:

- (a) Primary constants
- (b) Secondary constants

These constants are further classified in the following diagram.

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_136_0.png)

Now we will discuss only primary constants, namely, integer, real, character and string constants.

### Integer Constants

**Rules for Constructing Integer Constants**

The following are the rules that we have to follow to form an integer constant.

- An integer constant must have at least one digit.
- It must not accept a decimal point.
- It can be either positive or negative.
- If no sign precedes an integer constant it is assumed to be positive.
- No commas or blanks are allowed within an integer constant.
- The permissible range for integer constants is -32768 to 32767.

Truly speaking, the range of an integer constant depends upon the compiler. For a 16-bit compiler like Turbo C or Turbo C++ the range is -32768 to 32767. For a 32-bit compiler the range would be even bigger.

**Classification of Integer Constants**

Further, these constant can be classified according to the base of the numbers which are as follows:

**1. Decimal integer constants**

These consist of digits 0 through 9 and first digit should not be 0.

**Example**

1        44        3277 are valid decimal integer constants

The following are the invalid decimal constants:

| Invalid decimal constant | Reason |
|---|---|
| `12, 45` | comma not allowed |
| `36.0` | illegal char |
| `1 010` | blank space not allowed |
| `10 - 10` | illegal char - |
| `0900` | the first digit should not be a zero |

**2. Octal integer constants**

These consist of digits 0 through 7. The first digit must be zero in order to identify the constant as an octal number.

**Example**

Valid octal integer constants are as follows:

0          01          0743          0777

Invalid octal integer constants are as follows:

| Invalid octal integer constant | Reason |
|---|---|
| 743 | does not begin with 0 |
| 0438 | illegal character 8 |
| 0777.77 | illegal char. |

**3. Hexadecimal integer constants**

These constants begin with 0x or 0X and are followed by combination of digits taken from hexadecimal digits 0 to 9, a to f or A to F.

The following are the valid hexadecimal constants:

0X0        0X1        0XF77        0xabcd.

| Invalid hexadecimal constant | Reason |
|---|---|
| 0BEF | x is not included |
| 0x.4bff | illegal char (.) |
| 0XGBC | illegal char G |
| 1 | decimal or exponent required |
| 1,00.0 | comma not allowed |
| 2E+10.2 | exponent is written after integer quantity |
| 3E 10 | blank space |

Maximum values these constants can have are as follows:

| Integer constants | Maximum value |
|---|---:|
| Decimal integer | 32767 |
| Octal integer | 77777 |
| Hexadecimal integer | 7FFF |

**4. Unsigned integer constants**

Exceed the ordinary integer by a magnitude of 2; they are not negative. A character U is prefixed to number to make it unsigned.

**5. Long integer constants**

These are used to exceed the magnitude of ordinary integers and are appended by L.

**Example**

| Constant | Description |
|---|---|
| 50000U | decimal unsigned |
| 1234567889L | decimal long |
| 0123456L | octal long |
| 07777777U | octal unsigned |

### Floating Point Constants or Real Constants

Real constants are also named floating point constants. The real constants could be written in two forms—Fractional form and Exponential form.

**Rules for Constructing Floating Point Constants**

The following rules are observed while constructing real constants expressed in fractional form:

- A real constant must have at least one digit.
- It must accept a decimal point.
- It could be either positive or negative.
- Default sign is positive.
- No commas or blanks are allowed within a real constant.

Example of valid floating point constants:

+325.38      42.56      -32.78      -48.589

Examples of invalid floating point numbers are as follows:

The exponential form of representation of real constants is usually used if the value of the constant is either too small or too large.

In the exponential form of representation, the real constant is represented in two parts. The part appearing before ‘e’ is called mantissa, whereas the part following ‘e’ is called exponent.

**Rules for constructing floating point constants when it is treated as an exponent form**

The following rules must be observed while constructing real constants expressed in exponential form:

- The mantissa part and the exponential part should be separated by a letter e.
- The mantissa part may have a positive or negative sign.
- Default sign of mantissa part is positive.
- The exponent must have at least one digit, which must be a positive or negative integer. Default sign is positive.
- Range of real constants expressed in exponential form is -3.4e38 to 3.4e38.

**Examples**

3.2e-5      4.1e8      -0.2e+3      3.2...e-5

### Character Constants

This constant is a single character enclosed in apostrophes ' ' . For example, some of the character constants are shown below:
'B', 'X', '4', '$'

'\0' is a null character having value zero. Character constants have integer values associated depending on the character set adopted for the computer. ASCII character set is in use which uses 7-bit code with 2^7 = 128 different characters. The digits 0–9 are having ASCII value of 48-57 and 'A' having ASCII value 65 and 'a' having value 97 are sequentially ordered.

**For example,**

'A' has 65, blank has 32

**Rules for Constructing Character Constants**

The following rules must be observed while constructing character constants:

- A character constant is a single alphabet, a single digit or a single special symbol enclosed within single inverted commas. Both the inverted commas should point to the left. For example, ‘A’ is a valid character constant whereas ’A’ is not.
- The maximum length of a character constant can be 1 character. Ex.: 'C'

**Escape Sequence**

There are some non-printable characters that can be printed by preceding them with '\\' backslash character. Within character constants and string literals, you can write a variety of **escape sequences**. Each escape sequence determines the code value for a single character.

You can use escape sequences to represent character codes which are as follows:

- You cannot otherwise write (such as `\n`)
- That can be difficult to read properly (such as `\t`)
- That might change value in different target character sets (such as `\a`)
- That must not change in value among different target environments (such as `\0`)

The following is the list of the escape sequences:

| Escape sequence | Character |
|---|---|
| `\n` | New line |
| `\r` | Carriage return |
| `\t` | Tab |
| `\v` | Vertical tab |
| `\b` | Backspace |
| `\f` | Form feed (page feed) |
| `\a` | Alert (beep) |
| `\'` | Single quote (‘) |
| `\"` | Double quote (”) |
| `\?` | Question mark (?) |
| `\\` | Backslash (\\) |

### String Constants

String constants consist of collection of characters enclosed within double quotes.

**Example**

"Red light"  "Blue Sea hundred"  "hello world".

### Symbolic Constants

Symbolic constant is a name that substitutes for a sequence of characters or a numeric constant, a character constant or a string constant. When program is compiled each occurrence of a symbolic constant is replaced by its corresponding character sequence.

The syntax is as follows:

```
#define name text
```

Where name implies symbolic name in caps, text implies value or the text.

**Example**

```
#define Q 100
#define MAX1 100
#define TRUE 1
#define FALSE 0
#define SIZE 10
```

The # character is used for preprocessor commands. A *preprocessor* is a system program, which comes into action prior to Compiler, and it replaces the replacement text by the actual text.

**Advantages of using symbolic constants**

The advantages of using symbolic constants are as follows:

- They can be used to assign names to values
- Replacement of value has to be done at one place and wherever the name appears in the text it gets the value by execution of the preprocessor. This saves time. If the symbolic constant appears 20 times in the program; it needs to be changed at one place only.

## USER DEFINED TYPE DECLARATION

In C language a user can define an identifier that represents an existing data type. The user defined data type identifier can later be used to declare variables.

The general syntax of defining a user defined type is as follows:

```
typedef type identifier;
```

where `type` represents existing data type and `identifier` refers to the name given to the data type.

**Example**

```
typedef int salary;
typedef float average;
```
