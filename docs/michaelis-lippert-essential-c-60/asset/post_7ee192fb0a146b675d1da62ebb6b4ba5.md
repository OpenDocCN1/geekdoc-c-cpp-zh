
Perhaps the most interesting thing that you can glean from such a listing is how relatively easy it is to follow what the program is doing compared to trying to read and understand machine code (assembler). In the listing, an explicit reference to System.Console.WriteLine() appears. There is a lot of peripheral information to the CIL code listing, but if a developer wanted to understand the inner workings of a C# module (or any CLI-based program) without having access to the original source code, it would be relatively easy unless an obfuscator is used. In fact, several free tools are available (such as Red Gate’s Reflector, ILSpy, JustDecompile, dotPeek, and CodeReflect) that can decompile from CIL to C# automatically.

## SUMMARY

This chapter served as a rudimentary introduction to C#. It provided a means of familiarizing you with basic C# syntax. Because of C#’s similarity to C++-style languages, much of this might not have been new material to you. However, C# and managed code do have some distinct characteristics, such as compilation down to CIL. Although it is not unique, another key characteristic of C# is its full support for object-oriented programming. Even tasks such as reading and writing data to the console are object oriented. Object orientation is foundational to C#, as you will see throughout this book.

The next chapter examines the fundamental data types that are part of the C# language, and discusses how you can use these data types with operands to form expressions.

## 2
### Data Types

From Chapter 1’s *HelloWorld* program, you got a feel for the C# language, its structure, basic syntax characteristics, and how to write the simplest of programs. This chapter continues to discuss the C# basics by investigating the fundamental C# types.

![](img/25683ccec0773ba5b8794b11f2b12877_73_0.png)

Until now, you have worked with only a few built-in data types, with little explanation. In C# thousands of types exist, and you can combine types to create new types. A few types in C#, however, are relatively simple and are considered the building blocks of all other types. These types are the **predefined types**. The C# language’s predefined types include eight integer types, two binary floating-point types for scientific calculations and one decimal float for financial calculations, one Boolean type, and a character type. This chapter investigates these types, looks more closely at the string type, and introduces arrays.

## Fundamental Numeric Types

The basic numeric types in C# have keywords associated with them. These types include integer types, floating-point types, and a special floating-point type called decimal to store large numbers with no representation error.

## Integer Types

There are eight C# integer types. This variety allows you to select a data type large enough to hold its intended range of values without wasting resources. Table 2.1 lists each integer type.

## TABLE 2.1: Integer Types

| Type | Size | Range (Inclusive) | BCL Name | Signed | Literal Suffix |
|---|---|---|---|---|---|
| sbyte | 8 bits | -128 to 127 | System.SByte | Yes | |
| byte | 8 bits | 0 to 255 | System.Byte | No | |
| short | 16 bits | -32,768 to 32,767 | System.Int16 | Yes | |
| ushort | 16 bits | 0 to 65,535 | System.UInt16 | No | |
| int | 32 bits | -2,147,483,648 to 2,147,483,647 | System.Int32 | Yes | |
| uint | 32 bits | 0 to 4,294,967,295 | System.UInt32 | No | U or u |
| long | 64 bits | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | System.Int64 | Yes | L or l |
| ulong | 64 bits | 0 to 18,446,744,073,709,551,615 | System.UInt64 | No | UL or ul |

Included in Table 2.1 (and in Tables 2.2 and 2.3) is a column for the full name of each type; we discuss the literal suffix later in the chapter. All the fundamental types in C# have both a short name and a full name. The full name corresponds to the type as it is named in the Base Class Library (BCL). This name, which is the same across all languages, uniquely identifies the type within an assembly. Because of the fundamental nature of these types, C# also supplies keywords as short names or abbreviations to the full names of fundamental types. From the compiler’s perspective, both names refer to

the same type, producing exactly the same code. In fact, an examination of the resultant CIL code would provide no indication of which name was used.

Although C# supports using both the full BCL name and the keyword, as developers we are left with the choice of which to use when. Rather than switching back and forth, it is better to use one or the other consistently. For this reason, C# developers generally go with using the C# keyword form—choosing, for example, int rather than System.Int32 and string rather than System.String (or a possible shortcut of String).

## Guidelines

- **DO** use the C# keyword rather than the BCL name when specifying a data type (for example, string rather than String).
- **DO** favor consistency rather than variety within your code.

The choice for consistency frequently may be at odds with other guidelines. For example, given the guideline to use the C# keyword in place of the BCL name, there may be occasions when you find yourself maintaining a file (or library of files) with the opposite style. In these cases it would better to stay consistent with the previous style than to inject a new style and inconsistencies in the conventions. Even so, if the “style” was actually a bad coding practice that was likely to introduce bugs and obstruct successful maintenance, by all means correct the issue throughout.

## Language Contrast: C++—short Data Type

In C/C++, the short data type is an abbreviation for short int. In C#, short on its own is the actual data type.

## Floating-Point Types (float, double)

Floating-point numbers have varying degrees of precision, and binary floating-point types can represent numbers exactly only if they are a fraction with a power of 2 as the denominator. If you were to set the value of a floating-point variable to be 0.1, it could very easily be represented as

0.09999999999999999 or 0.10000000000000001 or some other number very close to 0.1. Similarly, setting a variable to a large number such as Avogadro’s number, 6.02 × 10²³, could lead to a representation error of approximately 10⁸, which after all is a tiny fraction of that number. The accuracy of a floating-point number is in proportion to the magnitude of the number it represents. A floating-point number is precise to a certain number of significant digits, not by a fixed value such as ±0.01.

C# supports the two binary floating-point number types listed in Table 2.2.

**TABLE 2.2: Floating-Point Types**

| Type | Size | Range (Inclusive) | BCL Name | Significant Digits | Literal Suffix |
|---|---|---|---|---|---|
| `float` | 32 bits | ±1.5 × 10⁻⁴⁵ to ±3.4 × 10³⁸ | `System.Single` | 7 | F or f |
| `double` | 64 bits | ±5.0 × 10⁻³²⁴ to ±1.7 × 10³⁰⁸ | `System.Double` | 15–16 | — |

Binary numbers appear as base 10 (denary) numbers for human readability. The number of bits (binary digits) converts to 15 decimal digits, with a remainder that contributes to a sixteenth decimal digit as expressed in Table 2.2. Specifically, numbers between 1.7 × 10³⁰⁷ and less than 1 × 10³⁰⁸ have only 15 significant digits. However, numbers ranging from 1 × 10³⁰⁸ to 1.7 × 10³⁰⁸ will have 16 significant digits. A similar range of significant digits occurs with the decimal type as well.

## Decimal Type

C# also provides a decimal floating-point type with 128-bit precision (see Table 2.3). This type is suitable for financial calculations.

**TABLE 2.3: decimal Type**

| Type | Size | Range (Inclusive) | BCL Name | Significant Digits | Literal Suffix |
|---|---|---|---|---|---|
| `decimal` | 128 bits | 1.0 × 10⁻²⁸ to approximately 7.9 × 10²⁸ | `System.Decimal` | 28–29 | M or m |
