

- A legal C program is a legal C++ program except when the C program:
  - uses C++ keywords as identifiers
  - depends on certain C type conversion rules that are different in C++

- Control structures (for, while, do, if, if else, switch, etc.) all work as before and cannot be extended

- Operators (+, -, +=, ++, --, etc.) all work as before with the same precedence. However, operators can now be extended to work on new types (structs / classes).

- Still have global declarations and library declarations in .h files and implementation code in .cpp files, but levels of abstraction now tend to be separated into different source files,
  i.e., might have TimeDate.h declaration and TimeDate.cpp for implementation of functions, then Postmark.h and Postmark.cpp files that use TimeDate class

- main() as the program start point

- Still use { and } to delimit blocks

- Same primitive data types

- Same storage classes and scope rules

- Same memory layout and addressing scheme

- Functions still can't be nested

- Existing preprocessor features continue to work, but many uses of the preprocessor now done more elegantly in language itself

- Some dangerous / useful C features still present:
  - no array bounds checking (but it's possible to define a safe array type or class)

## C++ Is a Better C - What's New?

- Additional comment style available (//)

- Few more operators (scope resolution operator ::, new, delete)

- Function prototyping with checking of argument type and number of arguments is the most important "better C" feature.

- They find lots of bugs at compile time that otherwise must be found at runtime

- Default initialization of function parameters

- Overloading of function names (allows name reuse)

- Overloading of operators

- Declarations as statements

- Inline functions allow for optimizations

- Structures are type names

- const declarations

- References allow call by reference to be specified by the function called and does not require addresses to be explicitly passed to the called function

- Type-safe linkage ensure correct calling syntax

- Improved approach to IO - Streams library is an IO data type that is used in place of a set of library routines

- Classes

- Single Inheritance

- Multiple Inheritance

- Templates (Standard Template Library)

- Exception Handling

- Less reliance on preprocessor and libraries

- Storage management is handled by `new` and `delete`. These operators understand the language and therefore can be more accurate than `malloc` and `free`.

### C++ Supports Data Abstraction

Create abstract data types as "built-in" as fundamental data types

- Operator overloading

- User-defined objects

### C++ Supports Object-Oriented Programming

- Encapsulation
  - classes
  - objects
  - scope control
  - privacy

- Inheritance
  - sharing object class resources

- Polymorphism
  - semantic convenience
  - virtual functions

### C++/OOP Paradigm Shift

The key difference between C & C++ is that in C++ you try to work at a higher perceptual level. When people start writing a program in C, they get to the bits and bytes very fast. In a programming language like C++, and OOP in general, you start by saying:

- Now what are the fundamental concepts in my application?

- How do they relate to each other?

- Can we express the relationships between those fundamental concepts directly?

In other words, the design phase becomes a natural part of programming.

- can write programs faster

- can get higher quality code

- can write code that's easier to maintain

Note that C++ supports data abstraction and OOP but does not require their use.

## C++ Closing Comments

C++ provides a gradual migration path from C.

Biggest problem with the transition from C to C++ is that people don't know C!

You can still twiddle bits if you want to.

Run-time efficiency is very important... C++ provides the speed of C.

Experts can provide reusable packages to the rest of us that are:

- modular

- extensible by others

## Primary C++ Benefits

- ability to mix paradigms

- experience base of C programmers

- convenience of higher level of abstraction

- programmers like it

Should be called ++C

## First C++ Program

Note: If you copy and paste the code below into your C++ compiler, it will not compile properly until you change the slanted double quotes (from my Word document) into normal double quotes.

```
// hello.cpp
#include <iostream>
using namespace std;
int main() {
    int age;
    cout << "Please enter your age: ";
    cin >> age;
    cout << "Hello, world! I am " << age << " today!" << endl;
}
```

## Input / Output

The iostream header file automatically defines variables (objects) called cout and cin.

cout is a predefined object that accepts all data bound for the standard output stream (monitor).

cin is also a predefined object which corresponds to the standard input stream (keyboard).

To send data to the standard input stream, we use the << operator (which is the bitwise shift operator in C). This operator is overloaded in C++ to give it a new meaning when the operator is used with an object of a particular type. When used with iostream objects, << means send to.

Note that cout and the << operator know how to treat an integer and a string differently. If a string is sent, it is treated as text. If an integer is sent, it is treated as a number. This may seem obvious, but it's another example of operator overloading, a key feature of C++.

C programmers will remember that such functions as `printf()` need to be told about:

- both the variable to be displayed

- and the variable type

This older C syntax make things less intuitive.

Note that the send to operator (`<<`) can be cascaded. This allows a series of values to be sent to standard output.

The `>>` operator is the extraction operator or *get from* operator. It takes the value from the stream object on its left and places it in the variable on its right.

## iostream Manipulators

Manipulators are operators used with the send to (`<<`) operator to modify the way data is displayed. The two most common manipulators are:

- endl

- setw

`endl` generates a linefeed by inserting a linefeed into the output stream. It is equivalent to `'\n'`, but also clears the buffer.

`setw` causes the item following to be displayed in a field of the specified width. The default output field for a variable is just wide enough to hold the value. The `setw` manipulator acts on the number (or string) that follows it in the output stream. The item is displayed right-justified in the field.

For example:

```
cout << setw(8) << num << setw(12) << num << endl;
```

## Additional manipulators:

```
cout << "The octal value is " << oct << num;
cout << "The decimal value is " << dec << num;
cout << "The hex value is " << hex << num;
```

The I/O manipulators cause the num values to be formatted differently than without any manipulators. The declarations for the manipulators are not in the usual iostream header file, but in a separate header file called iomanip:

```
#include <iomanip>
```

## Why a New I/O Library?

Consider this C program:

```
#include <stdio.h>
int main(void) {
 char a = 'a';
 char *b = "a string";
 double c = 3.14;
 printf(" a = %d\n b = %d\n c = %d\n", a, b, c);
}
```

When compiled and executed, the C program produces the following output:

a = 97
b = 72688
c = -171818680

Why? Because the type and number of the arguments are determined by the format character string and is left to the programmer to get it right. Here's the same program written in C++:

```
#include <iostream>
using namespace std;
int main() {
 char a = 'a';
 char *b = "a string";
 double c = 3.14;
 cout << "a = " << a << endl;
 cout << "b = " << b << endl;
 cout << "c = " << c << endl;
}
```

