
[content]
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
\** is a special multiline comment used for documentation systems such asoxygen. It begins with /**. See Appendix I for details. /
* This is a multiline comment that begins with /*
```

This style is often used to temporarily disable a group of statements during debugging.

## K.2 Data Types, Variables, and Arrays

C++ uses primitive data types and variable declarations that are similar to those in Java. The Java types char, int, float and double are used in C++ and behave the same as Java. In C++, int can be modified with short, long, signed and unsigned. All variables are initialized to zero, if a primitive type, or null, if an object reference. You must initialize all C++ variables. If you do not, or an uninitialized variable is used, the result of the operation or statement is undefined.

**Boolean types.** One important difference between Java and C++ data occurs with boolean variables. In Java, boolean is a type that has the value true or false. In C++, the analog type is bool. It also has a value of true or false, but in C++, true and false are special identifiers. Variables, of type bool are actually integers. This affects the type of the statement that is used as the predicate or test clause in an if statement, for loop, or while loop, which you will see in the next section. The C++ value of false is 0, and an integer value of zero is considered false in a boolean test. The value of true is 1, and any non-zero integer is considered true.

**String types.** Java has a special class String to represent character strings. C++ also provides a special class string (the lower case s) that implements many of the features. To use this class,

```
#include <string>
```

as one of the first lines in your program. More information on the C++ class string is in Section A.7 of Appendix A.

**Constants.** Constants in Java are declared within a class or method using the syntax

```
public static final int MAX_SIZE = 20;
```

which creates a publicly accessible constant MAX_SIZE with the value 20. A similar statement in C++ uses the keyword const to indicate a constant value:

```
const int MAX_SIZE = 20;
```

Constants in C++ are available anywhere within the scope of their declaration. If a constant declared outside of a class or file, that is available to any function or class defined after it is file and is said to be **global**, even though it is restricted to that file.

Java has a null that is used to indicate that an object has not been assigned to a variable. C++ uses nullptr for this purpose.

**Arrays.** You declare and reference arrays in Java and C++ using similar statements, their implementations are very different. Arrays in Java and C++ have a public field length that contains the number of locations in the array. If a program attempts to access a position beyond the end of the array, an exception is thrown.

C++ arrays are not objects, but are sequences of memory locations of the data type declared for try. In C++ arrays are accessed using [ ], just as they are in Java. C++ arrays have no data field that tracks the positions in the array that do, and most importantly, C++ permits the programmer to access positions in the array that do not exist. This is a very common source of errors in a C++ program and is one of the areas where you must take care. The STL class vector, which is discussed in Section A.6 of Appendix A, is an alternative to C++ arrays that provides some of the features of the Java array.

The following declares an array of 20 integers in Java:

```
int[] myArray = new int[MAX_SIZE];
```

This statement does the same thing in C++:

```
int myArray[MAX_SIZE];
```

You can also declare a C++ array by using syntax similar to that of Java:

```
int myArray[] = new int[MAX_SIZE];
```

One difference is the location of the square brackets, but you must also take responsibility for deleting the array when you are finished with. You do so with the delete statement:

```
delete[] myArray;
```

Notice the [ ] following the delete operator to indicate that myArray is an array. In C++ Interlude 2, we discuss the use of the operators new and delete in C++.

## K.3 Flow Control and Functions

**Flow control.** The syntax of flow is derived from C++, the structure of flow-control statements in C++ is the same as you you are familiar with Java. This is true for the selection statements if, if-else, and switch. It is also true for loop statements while, do-while, and for. significant differences in C++ are related to the test expression that controls the selection or repetition.

Consider the following Java if-else statement that compares the integer x to 6 and increments y by 10 if x is 6, and by 20 otherwise:

```
if (x == 6)
y += 10;
else
y += 20;
```

Because the syntax for an if-else statement is the same in C++, we could place this statement in a C++ program and the variable x is equal to 6 and false otherwise. The test x==6 is a predicate expression that returns true if it returns a value of type boolean. A Java flow-control statement requires its test expression to have a boolean value, so you must use a predicate expression as the test expression.

A C++ control statement does not restrict the data type of its test expression. Flow-control decisions are made based on whether the expression returns zero or nonzero. If the test returns zero, any nonzero value is considered true. The equality operator in the example returns true, which is 1, if x has the value of 6, it returns false, which is 0. The if-else statement determines its choice of action based on these.

This behavior of the C++ if-else statement gives you great flexibility in constructing tests for flow-control statements. It can also create confusion and subtle logic errors. For example, consider the following if-else statement:

```
if (x = 6)
y += 10;
else
y += 20;
```

At first, this might be the same as the earlier example, but by closer inspection you can see that the test expression is the assignment statement x = 6. The Java compiler will reject this as an error, since it is not a predicate expression. The C++ compiler will accept this statement, and when the program runs, the if-else statement will be evaluated as follows:

```
if (x = 6) // The variable x is assigned the value of 6.
y += 10; // it is non-zero, so it is "true"; increment y by 10.
```

Every time this code executes, x will be assigned the value 6, and y will be incremented by 10. The original value of x is overwritten by the if's test expression and is never used! Tracking down subtle errors, such as this, has cost this author many sleepless nights. When performing tests in C++ flow-control statements, always check that the test uses == and !=.

**Functions.** As mentioned, C++ functions do not need to be part of a class. You do not need to precede C++ functions with access modifiers, as you would for Java methods. The syntax for declaration and invocation of a C++ function is similar to that of a Java method. Functions can be defined anywhere in a C++ file, except inside another function.

Here is an example of a C++ function, realCube, that has a parameter of type double and returns the cube of a number:

```
double realCube(double x)
{
  return x * x * x;
} // defined after realCube
```

Any function defined after realCube can invoke realCube. But if a function is defined before realCube and needs to call it? In this case, the compiler would issue an error stating that
