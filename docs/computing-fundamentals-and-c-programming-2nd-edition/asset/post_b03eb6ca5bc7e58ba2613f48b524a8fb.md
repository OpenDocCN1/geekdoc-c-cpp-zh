
## DEBUGGING EXERCISES

- 1. Find errors, if any, in the following program:

```c
           /* A simple program
           int main( )
           {
               /* Does nothing */
           }
```

LO 3.2

- 2. Find errors, if any, in the following program:

```c
           #include (stdio.h)
           void main(void)
           {
               print("Hello C");
           }
```

LO 3.2

- 3. Find errors, if any, in the following program:

```c
           Include <math.h>
           main { }
           (
               FLOAT X;
               X = 2.5;
               Y = exp(x);
               Print(x,y);
           )
```

LO 3.3

## PROGRAMMING EXERCISES

- 1. Write a program to display the equation of a line in the form

```text
ax + by = c
```

for  a = 5, b = 8  and  c = 18.

LO 3.2

- 2. Write a program that will print your mailing address in the following form:

```text
First line     :     Name
Second line    :     Door No, Street
Third line     :     City, Pin code
```

LO 3.2

- 3. Write a program to output the following multiplication table:

```text
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
.    .
.    .
5 x 10 = 50
```

LO 3.2

### 4.2.1 Trigraph Characters

Many non-English keyboards do not support all the characters mentioned in Table 4.1. ANSI C introduces the concept of “trigraph” sequences to provide a way to enter certain characters that are not available on some keyboards. Each trigraph sequence consists of three characters (two question marks followed by another character) as shown in Table 4.2.

For example, if a keyboard does not support square brackets, we can still use them in a program using the trigraphs ??( and ??).

**Table 4.2** *ANSI C Trigraph Sequences*

| Trigraph sequence | Translation |
|---|---|
| ??= | # number sign |
| ??( | [ left bracket |
| ??) | ] right bracket |
| ??< | { left brace |
| ??> | } right brace |
| ??! | \| vertical bar |
| ??/ | \ back slash |
| ??' | ^ caret |
| ??- | ~ tilde |

### 4.3 C TOKENS LO 4.1

In a passage of text, individual words and punctuation marks are called *tokens*. Similarly, in a C program the smallest individual units are known as C tokens. C has six types of tokens as shown in Fig. 4.1. C programs are written using these tokens and the syntax of the language.

![](img/11b034a94fc590add0a7808250a38792_134_0.png)

Fig. 4.1 C tokens and examples

## 4.4 KEYWORDS AND IDENTIFIERS

LO 4.1

Every C word is classified as either a *keyword* or an *identifier*. All keywords have fixed meanings and these meanings cannot be changed. The list of all keywords of ANSI C are listed in Table 4.3. All keywords must be written in lowercase. Some compilers may use additional keywords that must be identified from the C manual.

> **Note** C99 adds some more keywords. See the Appendix “C99 Features”.

Table 4.3 ANSI C Keyword

| auto | double | int | struct |
|---|---|---|---|
| break | else | long | switch |
| case | enum | register | typedef |
| char | extern | return | union |
| const | float | short | unsigned |
| continue | for | signed | void |
| default | goto | sizeof | volatile |
| do | if | static | while |

**Identifiers** refer to the names of variables, functions and arrays. These are user-defined names. Both uppercase and lowercase letters are permitted. The underscore character is also permitted in identifiers.

### Rules for Identifiers

- 1. First character must be an alphabet (or underscore).
- 2. Must consist of only letters, digits or underscore.
- 3. Only first 31 characters are significant.
- 4. Cannot use a keyword.
- 5. Must not contain white space.

## 4.5 CONSTANTS

LO 4.2

Constants in C refer to fixed values that do not change during the execution of a program. C supports several types of constants as illustrated in Fig. 4.2.

### 4.5.1 Integer Constants

An *integer constant* refers to a sequence of digits. There are three types of integers, namely, *decimal integer*, *octal integer* and *hexadecimal integer*.

**Decimal integers** consist of a set of digits, 0 through 9, preceded by an optional – or + sign. Valid examples of decimal integer constants are:

```text
123  –321  0  654321  +78
```

![](img/11b034a94fc590add0a7808250a38792_136_0.png)

**Fig. 4.2** Basic types of C constants

Embedded spaces, commas, and non-digit characters are not permitted between digits. For example,

```text
15 750   20,000   $1000
```

are illegal numbers.

> **Note** ANSI C supports unary plus which was not defined earlier.

An *octal integer* constant consists of any combination of digits from the set 0 through 7, with a leading 0. Some examples of octal integer are:

```text
037   0   0435   0551
```

A sequence of digits preceded by 0x or 0X is considered as *hexadecimal integer*. They may also include alphabets A through F or a through f. The letter A through F represent the numbers 10 through 15. Following are the examples of valid hex integers:

```text
0X2  0x9F  0Xbed  0x
```

We rarely use octal and hexadecimal numbers in programming.

The largest integer value that can be stored is machine-dependent. It is 32767 on 16-bit machines and 2,147,483,647 on 32-bit machines. It is also possible to store larger integer constants on these machines by appending *qualifiers* such as U,L and UL to the constants. Examples:

```text
56789U                 or 56789u                  (unsigned integer)
987612347UL            or 98761234ul             (unsigned long integer)
9876543L               or 9876543l               (long integer)
```

The concept of unsigned and long integers are discussed in detail in Section 4.7.

### WORKED-OUT PROBLEM 4.1

Representation of integer constants on a 16-bit computer.

The program in Fig. 4.3 illustrates the use of integer constants on a 16-bit machine. The output in Fig. 4.3 shows that the integer values larger than 32767 are not properly stored on a 16-bit machine. However, when they are qualified as long integer (by appending L), the values are correctly stored.

Table 4.4 Examples of Numeric Constants

| Constant | Valid? | Remarks |
| :--- | :--- | :--- |
| 698354L | Yes | Represents long integer |
| 25,000 | No | Comma is not allowed |
| +5.0E3 | Yes | (ANSI C supports unary plus) |
| 3.5e-5 | Yes | |
| 7.1e 4 | No | No white space is permitted |
| -4.5e-2 | Yes | |
| 1.5E+2.5 | No | Exponent must be an integer |
| $255 | No | $ symbol is not permitted |
| 0X7B | Yes | Hexadecimal integer |

### 4.5.3 Single-Character Constants

A single character constant (or simply character constant) contains a single character enclosed within a pair of *single* quote marks. Example of character constants are:

```text
'5'   'X'   ';'   ' '
```

Note that the character constant '5' is not the same as the *number* 5. The last constant is a blank space. Character constants have integer values known as ASCII values. For example, the statement

```c
printf("%d", 'a');
```

would print the number 97, the ASCII value of the letter a. Similarly, the statement

```c
printf("%c", 97);
```

would output the letter 'a'. ASCII values for all characters are given in Appendix II.

Since each character constant represents an integer value, it is also possible to perform arithmetic operations on character constants.

### 4.5.4 String Constants

A string constant is a sequence of characters enclosed in *double* quotes. The characters may be letters, numbers, special characters and blank space. Examples are:

```text
"Hello!" "1987" "WELL DONE" "?...!" "5+3" "X"
```

Remember that a character constant (e.g., 'X') is not equivalent to the single character string constant (e.g., "X"). Further, a single character string constant does not have an equivalent integer value while a character constant has an integer value. Character strings are often used in programs to build meaningful programs.

### 4.5.5 Backslash Character Constants

C supports some special backslash character constants that are used in output functions. For example, the symbol '\n' stands for newline character. A list of such backslash character constants is given in Table 4.5. Note that each one of them represents one character, although they consist of two characters. These characters combinations are known as *escape sequences*.
