
## Chapter 2

This is also an assignment statement but is a little different because you have an arithmetic expression to the right of the assignment operator. This statement adds together the values stored in the variables apples and oranges and stores the result in the variable fruit.

The next three statements are:

```
cout << endl;                  // Start output on a new line
cout << "Oranges are not the only fruit... " << endl
    << "- and we have " << fruit << " fruits in all.";
cout << endl;                  // Start output on a new line
```

These are all output statements. The first statement is the first line here, and it sends a newline character, denoted by the word endl, to the command line on the screen. In C++, a source of input or a destination for output is referred to as a stream. The name cout specifies the "standard" output stream, and the operator << indicates that what appears to the right of the operator is to be sent to the output stream, cout. The << operator "points" in the direction that the data flows — from the variable or string that appears on the right of the operator to the output destination on the left. Thus in the first statement the value represented by the name endl — which represents a newline character — is sent to the stream identified by the name cout — and data transferred to cout is written to the command the command line.

The meaning of the name cout and the operator << are defined in the standard library header file <iostream>, which you added to the program code by means of the #include directive at the beginning of the program. cout is a name in the standard library and therefore is within the namespace std. Without the using directive it would not be recognized unless you used its fully qualified name, which is std::cout, as I mentioned earlier. Because cout has been defined to represent the standard output stream, you shouldn't use the name cout for other purposes so you can't use it as the name of a variable in your program for example. Obviously, using the same name for different things is likely to cause confusion.

The second output statement of the three is spread over two lines:

```
cout << "Oranges are not the only fruit... " << endl
    << "- and we have " << fruit << " fruits in all.";
```

As I said earlier, you can spread each statement in a program over as many lines as you wish if it helps to make the code clearer. The end of a statement is always signaled by a semicolon, not the end of a line. Successive lines are read and combined into a single statement by the compiler until it finds the semicolon that defines the end of the statement. Of course, this means that if you forget to put a semicolon at the end of a statement, the compiler will assume the next line is part of the same statement and join them together. This usually results in something the compiler cannot understand, so you'll get an error message.

The statement sends the text string "Oranges are not the only fruit... " to the command line, followed by another newline character (endl), then another text string, "- and we have ", followed by the value stored in the variable fruit, then finally another text string, " fruits in all.". There is no problem stringing together a sequence of things that you want to output in this way. The statement executes from left to right, with each item being sent to cout in turn. Note that each item to be sent to cout is preceded by its own << operator.

The third and last output statement just sends another newline character to the screen, and the three statements produce the output from the program that you see.

The last statement in the program is:

```
return 0;                  // Exit the program
```

This terminates execution of the main() function which stops execution of the program. Control returns to the operating system. I'll be discussing all of these statements in more detail later on.

The statements in a program are executed in the sequence in which they are written, unless a statement specifically causes the natural sequence to be altered. In Chapter 3, you'll look at statements that alter the sequence of execution.

## Whitespace

**Whitespace** is the term used in C++ to describe blanks, tabs, newline characters, form feed characters, and comments. Whitespace serves to separate one part of a statement from another and enables the compiler to identify where one element in a statement, such as int, ends and the next element begins. Otherwise, whitespace is ignored and has no effect.

Look at this statement for example:

```
int fruit;                  // ...then another one
```

There must be at least one whitespace character (usually a space) between int and fruit for the compiler to be able to distinguish them but if you add more whitespace characters they will be ignore. The content of the line following the semicolon is all whitespace and is therefore ignored.

On the other hand, look at this statement:

```
fruit = apples + oranges;      // Get the total fruit
```

No whitespace characters are necessary between fruit and =, or between = and apples, although you are free to include some if you wish. This is because the = is not alphabetic or numeric, so the compiler can separate it from its surroundings. Similarly, no whitespace characters are necessary on either side of the + sign but you can include some if you want to aid the readability of your code.

As I said, apart from its use as a separator between elements in a statement that might otherwise be confused, whitespace is ignored by the compiler (except, of course, in a string of characters between quotes). You can therefore include as much whitespace as you like to make your program more readable, as you did when you spread an output statement in the last example over several lines. Remember that in C++ the end of a statement is wherever the semicolon occurs.

## Statement Blocks

You can enclose several statements between a pair of braces, in which case they become a **block**, or a **compound statement**. The body of a function is an example of a block. Such a compound statement can be thought of as a single statement (as you'll see when you look at the decision-making possibilities in

C++ in Chapter 3). In fact, wherever you can put a single statement in C++, you could equally well put a block of statements between braces. As a consequence, blocks can be placed inside other blocks. In fact, blocks can be nested, one within another, to any depth.

> A statement block also has important effects on variables, but I will defer discussion of this until later in this chapter when I discuss something called variable scope.

## Automatically Generated Console Programs

In the last example, you opted to produce the project as an empty project with no source files, and then you added the source file subsequently. If you just allow the Application Wizard to generate the project as you did in Chapter 1, the project will contain several files, and you should explore their contents in a little more depth. Create a new Win32 console project with the name Ex2_01A and this time just allow the Application Wizard to finish without choosing to set any of the options in the Application Settings dialog. The project will have three files containing code: the Ex2_01A.cpp and stdafx.cpp source files, and the stdafx.h header file. This is to provide for basic capability that you might need in a console program and represents a working program at it stands, which does nothing. If you have a project open, you can close it by selecting the File > Close Solution item on the main menu. You can create a new project with an existing project open, in which case the old project will be closed automatically unless you elect to add it to the same solution.

First of all, the contents of Ex2_01A.cpp will be:

```
```cpp
#include "stdafx.h"

int _tmain(int argc, _TCHAR* argv[])
{
    return 0;
}
```
```

This is decidedly different from the previous example. There is an #include directive for the stdafx.h header file that was not in the previous version, and the function where execution starts is called _tmain(), not main().

The Application Wizard has generated the stdafx.h header file as part of the project, and if you take a look at the code in there, you’ll see there are two further #include directives for standard library header files stdio.h and tchar.h. stdio.h is the old-style header for standard I/O that were used before the current ISO/ANSI standard for C++; this covers essentially the same functionality as the <iostream> header. tchar.h is a Microsoft-specific header file defining text functions. The idea is that stdafx.h should define a set of standard system include files for your project you would add #include directives for any other system headers that you need in this file. While you are learning ISO/ANSI C++, you won’t be using either of the headers that appear in stdafx.h, which is one reason for not using the default file generation capability provided by the Application Wizard.

As I already explained, Visual C++ 2005 supports wmain() as an alternative to main() when you are writing a program that’s using Unicode characters — wmain() being a Microsoft-specific that is not part of ISO/ANSI C++. In support of that, the tchar.h header defines the name _tmain so that it will
