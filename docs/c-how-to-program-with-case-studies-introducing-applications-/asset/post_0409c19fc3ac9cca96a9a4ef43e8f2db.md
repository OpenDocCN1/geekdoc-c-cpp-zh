
## 9.5

Show what each of the following statements prints. If a statement is incorrect, indicate why.

- a) `printf("%-10d\n", 10000);`
- b) `printf("%%s\n", "This is a string");`
- c) `printf("%*.*f\n", 8, 3, 1024.987654);`
- d) `printf("#0\n%X\n%#e\n", 17, 17, 1008.83689);`
- e) `printf("% 1d%%\n%1d\n", 1000000, 1000000);`
- f) `printf("%10.2E\n", 444.93738);`
- g) `printf("%10.2g\n", 444.93738);`
- h) `printf("%d\n", 10.987);`

## 9.6

Find the error(s) in each of the following program segments. Explain how each error can be corrected.

- a) `printf("%s\n", 'Happy Birthday');`
- b) `printf("%c\n", 'Hello');`
- c) `printf("%c\n", "This is a string");`
- d) The following statement should print "Bon Voyage":
  `printf("%s", "Bon Voyage");`
- e) `char day[] = "Sunday";`
  `printf("%s\n", day[3]);`
- f) `puts('Enter your name: ');`
- g) `printf(%f, 123.456);`
- h) The following statement should print the characters '0' and 'k':
  `printf("%s%\n", '0', 'k');`
- i) `char s[10];`
  `scanf("%c", s[7]);`

## 9.7 (Differences Between %d and %i)

Write a program to test the difference between the %d and %i conversion specifiers when used in scanf statements. Ask the user to enter two integers separated by a space. Use the statements

`scanf("%d%", &x, &y);`
`printf("%d %d\n", x, y);`

to input and print the values. Test the program with the following sets of input data:

10 10
-10 -10
010 010
0x10 0x10

## 9.8 (Printing Numbers in Various Field Widths)

Write a program that prints the integer value 12345 and the floating-point value 1.2345 in fields of various sizes. What happens when the values are printed in fields containing fewer digits than the values?

## 9.9 (Rounding Floating-Point Numbers)

Write a program that prints 100.453627 rounded to the nearest digit, tenth, hundredth, thousandth and ten-thousandth.

## 9.10 (Temperature Conversions)

Write a program that converts integer Fahrenheit temperatures from 0 to 212 degrees to floating-point Celsius temperatures with 3 digits of precision. Perform the calculation using the formula

`celsius = 5.0 / 9.0 * (fahrenheit - 32);`

Display the output in two right-aligned columns of 10 characters each. Precede the Celsius temperatures by a sign for both positive and negative values.

## 9.11 (Escape Sequences)

Write a program to test the escape sequences \', \", \?, \\, \a, \b, \n, \r and \t. For the escape sequences that move the cursor, print a character before and after printing the escape sequence so it's clear where the cursor has moved.

## 9.12 (Printing a Question Mark)

Write a program that determines whether ? can be printed as part of a printf format control string as a literal character rather than using the \? escape sequence.

## 9.13 (Reading an Integer with Each scanf Conversion Specifier)

Write a program that inputs the value 437 using each of the scanf integer conversion specifiers. Print each input value using all the integer conversion specifiers.

## 9.14 (Outputting a Number with the Floating-Point Conversion Specifiers)

Write a program that uses each of the conversion specifiers e, f and g to input the value 1.2345. Print the values of each variable to prove that each conversion specifier can be used to input this same value.

## 9.15 (Reading Strings in Quotes)

In some programming languages, strings are entered surrounded by either single or double quotation marks. Write a program that reads the three strings suzy, "suzy" and 'suzy'. Are the single and double quotes ignored by C or read as part of the string?

## 9.16 (Printing a Question Mark as a Character Constant)

Write a program that determines whether ? can be printed as the character constant '?' rather than the character constant escape sequence '\?'. Use the conversion specifier %c in the format control string of a printf statement.

## 9.17 (Using %g with Various Precisions)

Write a program that uses the conversion specifier g to output the value 9876.12345. Print the value with precisions ranging from 1 to 9.

This page intentionally left blank

## Structures, Unions, Bit Manipulation and Enumerations

## Objectives

In this chapter, you'll:

- Create and use structs, unions and enums.
- Understand self-referential structs.
- Learn about the operations that can be performed on struct instances.
- Initialize struct members.
- Access struct members.
- Pass struct instances to functions by value and by reference.
- Use typedefs to create aliases for existing type names.
- Learn the operations that can be performed on unions.
- Initialize unions.
- Manipulate integer data with the bitwise operators.
- Create bit fields for storing data compactly.
- Use enum constants.
- Consider the security issues of working with structs, bit manipulation and enums.

![](img/43d318ad505997c339a3ea78d716d162_536_0.png)

## Outline

- 10.1 Introduction
- 10.2 Structure Definitions
  - 10.2.1 Self-Referential Structures
  - 10.2.2 Defining Variables of Structure Types
  - 10.2.3 Structure Tag Names
  - 10.2.4 Operations That Can Be Performed on Structures
- 10.3 Initializing Structures
- 10.4 Accessing Structure Members with . and ->
- 10.5 Using Structures with Functions
- 10.6 typedef
- 10.7 Random-Number Simulation Case Study: High-Performance Card Shuffling and Dealing
- 10.8 Unions
  - 10.8.1 Union Declarations
  - 10.8.2 Allowed union Operations
  - 10.8.3 Initializing unions in Declarations
  - 10.8.4 Demonstrating unions
- 10.9 Bitwise Operators
  - 10.9.1 Displaying an Unsigned Integer's Bits
  - 10.9.2 Making Function `displayBits` More Generic and Portable
  - 10.9.3 Using the Bitwise AND, Inclusive OR, Exclusive OR and Complement Operators
  - 10.9.4 Using the Bitwise Left- and Right-Shift Operators
  - 10.9.5 Bitwise Assignment Operators
- 10.10 Bit Fields
  - 10.10.1 Defining Bit Fields
  - 10.10.2 Using Bit Fields to Represent a Card's Face, Suit and Color
  - 10.10.3 Unnamed Bit Fields
- 10.11 Enumeration Constants
- 10.12 Anonymous Structures and Unions
- 10.13 Secure C Programming

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Special Section: Raylib Game-Programming Case Studies

## 10.1 Introduction

Structures are collections of related variables under one name, known as aggregates in the C standard. Structures may contain many variables of different types. That’s in contrast to arrays, which contain only elements of the same type. Here, we’ll discuss:

- `typedefs`—for creating *aliases* for previously defined data types.
- `unions`—similar to structures, but with members that share the *same* storage.
- `bitwise operators`—for manipulating the bits of integral operands.
- `bit fields`—`unsigned int` or `int` members of structures or unions for which you specify the number of bits in which the members are stored, helping you pack information tightly.
- `enumerations`—sets of integer constants represented by identifiers.

In Chapters 11 and 12, you’ll see that

- structures commonly define records to be stored in files, and
- pointers and structures facilitate forming data structures such as linked lists, queues, stacks and trees.

### Self Check

1. *(Fill-In)* ________ are similar to structures, but with members that share the same storage space.

**Answer:** unions.

2 (Fill-In) __________ are sets of integer constants represented by identifiers.
Answer: Enumerations.

## 10.2 Structure Definitions

Structures are derived data types—they're constructed using objects of other types. The keyword `struct` introduces a structure definition, as in

```
~~~c
struct card {
    const char *face;
    const char *suit;
};
~~~
```

The identifier `card` is the structure tag, which you use with `struct` to declare variables of the structure type—e.g., `struct card`. Variables declared within a `struct`'s braces are the structure's members. A `struct`'s members must have unique names, though separate structure types may contain members of the same name without conflict. Each structure definition ends with a semicolon.

The `struct card` definition contains `const char *` members `face` and `suit`. Structure members can be const or non-const primitive-type variables (e.g., `int`s, `double`s, etc.) or aggregates, such as arrays or other `struct`-type objects. Chapter 6 showed that an array's elements all have the same type. Structure members, however, can be of different types. For example, the following `struct` contains `char` array members for an employee's first and last names, an `int` member for the employee's age and a `double` member for the employee's hourly salary:

```
~~~c
struct employee {
    char firstName[20];
    char lastName[20];
    int age;
    double hourlySalary;
};
~~~
```

### 10.2.1 Self-Referential Structures

A `struct` type may not contain a variable of its own `struct` type (which is a compilation error), but it may contain a pointer to that `struct` type. For example, the updated `struct employee` below contains a pointer to the employee's manager, which would be another `struct employee` object:

```
~~~c
struct employee {
    char firstName[20];
    char lastName[20];
    unsigned int age;
    double hourlySalary;
    struct employee *managerPtr; // pointer
};
~~~
```

A structure containing a member that's a pointer to the *same* `struct` type is a self-referential structure. Self-referential structures are used to build linked data structures.
