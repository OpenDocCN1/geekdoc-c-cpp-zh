
## Literals, Variables and Data Types

## 4.1 Introduction

A programming language is designed to manipulate certain kinds of data consisting of numbers, characters and strings and provide useful output known as information to the user. The task of manipulating data is accomplished by executing a sequence of instructions constituting what is known as a program.

A C# program is basically a collection of classes. A class is defined by a set of declaration statements and methods containing instructions known as executable statements. These instructions are formed using certain symbols and words according to some rigid rules known as syntax rules (or grammar). The smallest, non-reducible, textual elements in a program are referred to as tokens. The compiler recognizes them for building up expressions and statements.

In simple terms, a C# program is a collection of tokens, comments and white spaces. C# includes the following five types of tokens:

- Keywords
- Operators
- identifiers
- Punctuators
- Literals

White spaces and comments are not tokens, though they may act as separators for tokens. Keywords are an essential part of a language definition. They implement specific features of the language. They are reserved, and cannot be used as identifiers except when they are prefaced by the @ character. Table 4.1 lists all the C# keywords.

### Table 4.1 C# keywords

| abstract | event | namespace | static |
| as | explicit | new | string |
| base | extern | null | struct |
| bool | false | object | switch |
| break | finally | operator | this |
| byte | fixed | out | throw |
| case | float | override | true |
| catch | for | params | try |
| char | foreach | private | typeof |
| checked | get | protected | uint |
| class | goto | public | ulong |
| const | if | readonly | unchecked |
| continue | implicit | ref | unsafe |
| decimal | in | return | ushort |
| default | int | sbyte | using |
| delegate | interface | sealed | value |
| do | internal | set | virtual |
| double | is | short | volatile |
| else | lock | sizeof | void |
| enum | long | stackalloc | while |

*Identifiers* are programmer-designed tokens. They are used for naming classes, methods, variables, labels, namespaces, interfaces, etc. C# identifiers enforce the following rules:

- They can have alphabets, digits and underscore characters
- They must not begin with a digit
- Upper case and lower case letters are distinct
- Keywords in stand-alone mode cannot be used as identifiers

C# permits the use of keywords as identifiers when they are prefixed with the ‘@’ character

*Literals* are the way in which the values that are stored in variables are represented. We shall discuss these in detail in the next section.

*Operators* are symbols used in expressions to describe operations involving one or more operands. Operators are considered in detail in Chapter 5.

*Punctuators* are symbols used for grouping and separating code. They define the shape and function of a program. Punctuators (also known as separators) in C# include:

- Parentheses ( )
- Braces { }
- Brackets [ ]
- Semicolon ;
- Colon :
- Comma ,
- Period .

*Statements* in C# are like sentences in natural languages. A statement is an executable combination of tokens ending with a semicolon. C# implements several types of statements. They include:

- Empty statements
- Labeled statements
- Declaration statements
- Expression statements
- Selection statements
- Iteration statements
- Jump statements
- The try statements
- The checked statements
- The unchecked statements
- The lock statements
- The using statements

These statements are discussed as and when they are encountered.

Program 4.1 demonstrates the application of @ as a prefix for using a keyword as an identifier. The program uses a variable @if to print numbers from 0 to 9.

### Program 4.1 IDENTIFIER EXAMPLE

```
using System;
class IdentifierExample
{
	public static void Main()
	{
		// Using if keyword as an identifier by prefixing @
		int @if;
		Console.WriteLine(" Demonstrating use of if keyword as an identifier by prefixing @\n");
		for(@if = 0; @if < 10; @if++)
		Console.WriteLine("The value of @if is: {0}", @if);
	}
}
```

```
C:\Chapter 4>IdentifierExample
--Demonstrating use of if keyword as an identifier by prefixing @--
The value of @if is: 0
The value of @if is: 1
The value of @if is: 2
The value of @if is: 3
The value of @if is: 4
The value of @if is: 5
The value of @if is: 6
The value of @if is: 7
The value of @if is: 8
The value of @if is: 9
C:\Chapter 4>_
```

Literals are value constants assigned to variables (or results of expressions) in a program. C# supports several types of literals as illustrated in Fig. 4.1.

![](img/bae4ee2c7c29c052feb3b9a9c5659998_53_0.png)

Fig. 4.1 C# literals

## 4.2.1 Integer Literals

An integer literal refers to a sequence of digits. There are two types of integers, namely, decimal integers and hexadecimal integers.

Decimal integers consist of a set of digits, 0 through 9, preceded by an optional minus sign. Valid examples of decimal integer literals are:

123 -321 0 654321

Embedded spaces, commas and non-digit characters are not permitted between digits. For example,

15 750 20,000 $1000

are illegal numbers.

A sequence of digits preceded by 0x or 0X is considered as a hexadecimal integer (hex integer). It may also include alphabets A through F or 'a' through 'f'. A letter A through F represents the numbers 10 through 15. Following are the examples of valid hex integers.

0X2 0X9F 0Xbcd 0x

## 4.2.2 Real Literals

Integer literals are inadequate to represent quantities that vary continuously, such as distances, heights, temperatures, prices and so on. These quantities are represented by numbers containing fractional parts like 17.548. Such numbers are called real (or floating point) numbers. Further examples of real literals are:

0.0083 -0.75 435.36

These numbers are shown in decimal notation, having a whole number followed by a decimal point and the fractional part, which is an integer. It is possible that the number may not have digits before the decimal point, or digits after the decimal point. That is,

215. .95 -.71

are all valid real literals.

A real literal may also be expressed in exponential (or scientific) notation. For example, the value 215.65 may be written as 2.1565e2 in exponential notation. e2 means multiply by 10². The general form is:

mantissa e exponent

The mantissa is either a real number expressed in decimal notation or an integer. The exponent is an integer with an optional plus or minus sign. The letter 'e' separating the mantissa and the exponent can be written in either lowercase or uppercase. Since the exponent causes the decimal point to 'float', this notation is said to represent a real number in floating-point form. Examples of legal floating-point literals are:

0.65e4 12e-2 1.5e+5 3.18E3 -1.2E-1

Embedded white (blank) space is not allowed in any numeric constant.

Exponential notation is useful for representing numbers that are either very large or very small in magnitude. For example, 7500000000 may be written as 7.5E9 or 75E8. Similarly, 0.000000368 is equivalent to -3.68E-7.

A floating-point literal may thus comprise four parts:

- a whole number
- a decimal point
- a fractional part
- an exponent

## 4.2.3 Boolean Literals

There are two Boolean literal values:

- true
- false

They are used as values of relational expressions.

## 4.2.4 Single Character Literals

A single-character literal (or simply character constant) contains a single character enclosed within a pair of single quote marks. Example of character constants are: '5' 'X' ',' ' '

Note that the character constant '5' is not the same as the number 5. The last constant in the example above is a blank space.

## 4.2.5 String Literals

A string literal is a sequence of characters enclosed between double quotes. The characters may be alphabets, digits, special characters and blank spaces. Examples are: "Hello C#" "2001" "WELL DONE" "?..." "5+3" "y"

## 4.2.6 Backslash Character Literal

C# supports some special backslash character constants that are used in output methods. For example, the symbol '\n' stands for a new-line character. A list of such backslash character literals is given in Table 4.2. Note that each one represents one character, although they consist of two characters. These character combinations are known as escape sequences.

Program 4.2 prints the various numeric literals available in C#, such as Integer, Double and Exponential.

### Program 4.2 | LITERAL SAMPLE

### Table 4.2 Backslash character literals

| CONSTANT | MEANING |
| '\a' | alert |
| '\b' | back space |
| '\f' | form feed |
| '\n' | new-line |
| '\r' | carriage return |
| '\t' | horizontal tab |
| '\v' | vertical tab |
| '\'' | single quote |
| '\"' | double quote |
| '\\' | backslash |
| '\0' | null |

```
using System;

class LiteralSample
{
    public static void Main()
    {
        System.Console.WriteLine("Integer Literal\n{0}", 58);
        System.Console.WriteLine("Double Literal\n{0}",1.6180339887498);
        System.Console.WriteLine("Decimal Literal\n{0}",1.618033988734565m);
        System.Console.WriteLine("Exponential Notation for Decimal Literal:\n{0}",6.023E23f);
        System.Console.WriteLine("Hexadecimal Literal\n{0}",0x003A);
    }
}
```
