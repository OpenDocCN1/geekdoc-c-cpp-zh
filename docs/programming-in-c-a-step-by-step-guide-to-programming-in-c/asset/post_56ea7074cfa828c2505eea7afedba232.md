
```
scanf("%f", &radius); /* Input statement */
area=3.14159*radius*radius; /* Assignment statement */
printf("Area=%f",area); /* Output statement */
}
```

## Program 1.2: Print a few numbers

Here is a program to illustrate a simple loop.

```
#include <stdio.h>
/* print a few numbers, to illustrate a simple loop */
main()
{
int i;
for(i = 0; i < 10; i = i + 1) /* Looping statement */
printf("i is %d\n", i);
return 0;
```

## Program 1.3: Program to add two numbers

```
#include <stdio.h>
main()
{
int i,j,k; // Defining variables
i = 6; // Assign values
j = 8;
```

A sequence of digits preceded by 0x or 0X is considered as *hexadecimal* integer. They may also include alphabets A through F or a through f. The letters A through F represent numbers 10 through 15.

Examples: 0X6, 0x5B, 0Xbcd, 0X

The largest integer value that can be stored is machine-dependent. It is 32767 on 16-bit machines and 2,147,483,647 on 32-bit machines. It is also possible to store larger integer constants on these machines by appending *qualifiers* such as U, L and UL to the constants.

Examples: 54637U or 54637u (unsigned integer)

65757564345UL or 65757564345ul (unsigned long integer)

7685784L or 7685784l (long integer)

## Program 1.1: Program to represent integer constants on a 16-bit computer

```
/* Integer numbers on 16-bit machine */
main()
{
printf("Integer values\n\n");
printf("%d %d %d\n", 32767,32767+1,32767+10);
printf("\n");
printf("Long integer values\n\n");
printf("%ld %ld %ld\n", 32767L, 32767L+1L, 32767L+10L);
}
```

Type and execute the above program and observe the output

## 1.4.2 Real constants

The numbers containing fractional parts like 67.45 are called real (or floating point) constants.

Examples: 0.0045, -8.5, +345.678

A real number may also be expressed in *exponential (scientific)* notation. The general form is:

*mantissa* e *exponent*

The mantissa is either a real number expressed in decimal notation or an integer. The exponent is an integer number with an optional plus or minus sign. The letter e separating the mantissa and the exponent can be written in either lowercase or uppercase.

Examples: 04e4, 12e-2, -1.3E-2

750000000 may be written as 7.5E9 or 75E8.

Floating point constants are normally represented as double-precision quantities. However, the suffixes f or F may be used to force single precision and l or L to extend double-precision further.

## 1.4.3 Character constants

A single character constant (or simple character constant) contains a single character enclosed within a pair of single quote marks.

Examples: '6', 'X', ';'

Character constants have integer values known as ASCII values. For example, the statement

```
printf("%d", 'a');
```

would print the number 97, the ASCII value of the letter a. Similarly, the statement

```
printf("%c", 97);
```

would print the letter a.

## 1.4.4 String constants

A string constant is a sequence of characters enclosed within double quotes. The characters may be letters, numbers, special characters and blank space.

Examples: “Hello!”, “1947”, “5+3”

## 1.4.5 Backslash character constants

C supports some special backslash character constants that are used in output functions. A list of such backslash character constants is given in Table 1.1. Note that each one of them represents one character, although they consist of two characters. These character combinations are called escape sequences.

Table 1.1: Backslash character constants

| Constant | Meaning |
|---|---|
| ‘\b’ | back space |
| ‘\f’ | form feed |
| ‘\n’ | new line |
| ‘\r’ | carriage return |
| ‘\t’ | horizontal tab |
| ‘\v’ | vertical tab |
| ‘\’ | single quote |
| ‘\"’ | double quote |

numbers will be from 0 to 65,535. We declare **long** and **unsigned integers** to increase the range of values. The use of qualifier **signed** on integers is optional because the default declaration assumes a signed number. The Table 1.2 shows all the allowed combinations of basic types and qualifiers and their size and range on a 16- bit machine.

## Table 1.2: Basic types, qualifiers and their size

| Type | Size (bits) | Range |
|---|---|---|
| int or signed int | 16 | -32,768 to 32,767 |
| unsigned int | 16 | 0 to 65535 |
| short int or signed short int | 8 | -128 to 127 |
| unsigned short int | 8 | 0 to 255 |
| long int or signed long int | 32 | -2,147,483,648 to 2,147,483,647 |
| unsigned long int | 32 | 0 to 4,294,967,295 |

Informally, a *variable* (also called an *object*) is a place where you can store a value so that you can refer to it unambiguously. A variable needs a name. You can think of the variables in your program as a set of boxes, each with a label giving its name; you might imagine that storing a value “in" a variable consists of writing the value on a slip of paper and placing it in the box.

Now let us see how integers and variables are declared. A *declaration* tells the compiler the name and type of a variable you'll be using in your program. In its simplest form, a declaration consists of the type, the name of the variable, and a terminating semicolon:

```
int i;
```

The above statement declares an integer variable i.

```
long int i1, i2;
```

We can also declare several variables of the same type in one declaration, separating them with commas as shown above.

The placement of declarations is significant. You can't place them just anywhere (i.e. they cannot be interspersed with the other statements in your program). They must either be placed at the beginning of a function, or at the beginning of a brace-enclosed block of statements, or outside of any function. Furthermore, the placement of a declaration, as well as its storage class, controls several things about its *visibility* and *lifetime*, as we'll see later.

You may wonder *why* variables must be declared before use. There are two reasons:

- 1. It makes things somewhat easier on the compiler; it knows right away what kind of storage to allocate and what code to emit to store and manipulate each variable; it doesn't have to try to intuit the programmer's intentions.
- 2. It forces a bit of useful discipline on the programmer: you cannot introduce variables wherever you wish; you must think about them enough to pick appropriate types for them. (The compiler's error messages to you, telling you that you apparently forgot to declare a variable, are as often helpful as they are a nuisance: they're helpful when they tell you that you misspelled a variable, or forgot to think about exactly how you were going to use it.)

Most of the time, it is recommended to write one declaration per line. For the most part, the compiler doesn't care what order declarations are in. You can order the declarations alphabetically, or in the order that they're used, or to put related declarations next to each other. Collecting all variables of the same type together on one line essentially orders declarations by type, which isn't a very useful order (it's only slightly more useful than random order).

A declaration for a variable can also contain an initial value. This *initializer* consists of an equal sign and an expression, which is usually a single constant:

```
int i = 1;
int i1 = 10, i2 = 20;
```

## Self Assessment Questions

10. The size of the Integers in C language is same in all the machines. (True/False)

11. A _______ is a place where we can store values.

12. Size of int is _______ bits.

13. Which of the following tells the compiler the name and type of a variable you'll be using in your program? (declaration)

- (a) declaration
- (b) variables
- (c) integers
- (d) assignments

14. The _______ consists of an equal sign and an expression, which is usually a single constant. (initializer)

15. A single declaration statement can contain variables of different types. (True/False)

## 1.6 Rules for naming Variables and assigning values to variables

Within limits, you can give your variables and functions any names you want. These names (the formal term is “identifiers”) consist of letters, numbers, and underscores. For our purposes, names must begin with a letter. Theoretically, names can be as long as you want, but extremely long ones get tedious to type after a while, and the compiler is not required to keep track of extremely long ones perfectly. (What this means is that if you were to name a variable, say, supercalafragalisticespialidocious, the compiler might get lazy and pretend that you'd named it super calafragalisticespialidocio, such that if you later misspelled it supercalafragalisticespialidociouz, the compiler wouldn't
