found by the compiler and import it using the Java import statement. If you need a class outside of the package, you must import it in Java.

The C++ compiler is stricter and requires the programmer to declare all functions, classes, and variables in a file before they are used. Because classes and constants are often used in multiple programs and locations in a program, C++ provides a mechanism called the pre-processor that lets you specify classes and data in a header file and then include it in your program. Comments, or directives, to the pre-processor are lines that begin with a hash #, as

```
#include <iostream> // The declaration of the iostream classes
#include "MyClass.h" // The declaration of MyClass
```

Notice system files use < >, while user-defined files use " to delimit the file name. A.8.1 of Appendix A, C++ Interlude 1, and Section K.4 of this approach shows how to develop C++ declarations.

Both Java and C++ are object-oriented languages, C++ has many elements that reflect its roots in the imperative language C. An imperative programming language does not use classes to group data and operations on that data. It is a sequence of functions and methods--that are not part of a class. As such, variables, constants, and functions in a C++ program can be declared in any file; while you are not forced to declare them within a class, as you are in Java. The only restriction to this capability is that a program cannot declare them inside another function.

Comments are an important part of any program, and C++ supports the same comment-style as Java:

```
// This is a comment that appears on its own line.
int sum = 0; // This is a comment that appears within a C++ statement
/* The following multiline comments end with /
*\* is a special multiline comment used for documentation systems such asoxygen. It begins with /**. See Appendix I for details. /
* This is a multiline comment that begins with /*
```

This style is often used to temporarily disable a group of statements during debugging.

# K.2 Data Types, Variables, and Arrays

C++ uses primitive data types and variable declarations that are similar to those in Java. The Java types char, int, float and double are used in C++ and behave the same as Java. In C++, int can be modified with short, long, signed and unsigned. All variables are initialized to zero, if a primitive type, or null1, if an object reference. You must initialize all C++ variables. If you do not, or an uninitialized variable is used, the result of the operation or statement is undefined.

Boolean types. One important difference between Java and C++ data occurs with boolean variables. In Java, boolean is a type that has the value true or false. In C++, the analog type is bool. It also has a value of true or false, but in C++, true and false are special identifiers. Variables, of type bool are actually integers. This affects the type of the statement that is used as the predicate or test clause in an if statement, for loop, or while loop, which you will see in the next section. The C++ value of false is 0, and an integer value of zero is considered false in a boolean test. The value of true is 1, and any non-zero integer is considered true.

String types. Java has a special class String to represent character strings. C++ also provides a special class string (the lower case s) that implements many of the features. To use this class,

```
#include <string>
```