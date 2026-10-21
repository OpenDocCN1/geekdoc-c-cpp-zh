
You can see that several lines of the program contain comments as well as program statements. You can also use an alternative form of comment bounded by `/*` and `*/`. For example, the first line of the program could have been written:

```
/*  Ex2_01.cpp  */
```

The comment using `//` covers only the portion of the line following the two successive slashes, whereas the `/* ... */` form defines whatever is enclosed between the `/*` and the `*/` as a comment and can span several lines. For example, you could write:

```
/*
    Ex2_01.cpp
    A Simple Program Example
*/
```

All four lines are comments. If you want to highlight some particular comment lines, you can always embellish them with a frame of some description:

```
/*********************************
*   Ex2_01.cpp                   *
*   A Simple Program Example     *
*********************************/
```

As a rule, you should always comment your programs comprehensively. The comments should be sufficient for another programmer or you at a later date to understand the purpose of any particular piece of code and how it works.

## The #include Directive — Header Files

Following the comments, you have an `#include` directive:

```
#include <iostream>
```

This is called a directive because it directs the compiler to do something—in this case to insert the contents of the file `<iostream>` into the program before compilation. The `<iostream>` file is called a header file because it’s usually brought in at the beginning of a program file. Actually `<iostream>` is more properly referred to as a header because in ANSI standard C++ a header need not necessarily be contained in a file. However, I’ll use the term header file in this book because with Visual C++ 2005 all headers are stored in files. The `<iostream>` header file contains definitions that are necessary for you to be able to use C++ input and output statements. If you didn’t include the contents of `<iostream>` into the program, it wouldn’t compile because you use output statements in the program that depend on some of the definitions in this file. There are many different header files provided by Visual C++ that cover a wide range of capabilities. You’ll be seeing more of them as you progress through the language facilities.

An `#include` statement is one of several preprocessor directives. The Visual C++ editor recognizes these and highlights them in blue in your edit window. Preprocessor directives are commands executed by the preprocessor phase of the compiler that executes before your code is compiled into object code, and preprocessor directives generally act on your source code in some way before it is compiled. They all start with the `#` character. I’ll be introducing other preprocessor directives as you need them.

## Namespaces and the Using Declaration

As you saw in Chapter 1, the standard library is an extensive set of routines that have been written to carry out many common tasks: for example, dealing with input and output, performing basic mathematical calculations. Since there are a very large number of these routines as well as other kinds of things that have names, it is quite possible that you might accidentally use the same name as one of the names defined in the standard library for your own purposes. A namespace is a mechanism in C++ for avoiding problems that can arise when duplicate names are used in a program for different things, and it does this by associating a given set of names such as those from the standard library with a sort of family name, which is the namespace name.

Every name that is defined in code that appears within a namespace also has the namespace name associated with it. All the standard library facilities for ISO/ANSI C++ are defined within a namespace with the name `std`, so every item from this standard library that you can access in your program has its own name, plus the namespace name, `std`, as a qualifier. The names `cout` and `endl` are defined within the standard library so their full names are `std::cout` and `std::endl`, and you saw these in action in Chapter 1. The two colons that separate the namespace name from the name of an entity form an operator called the scope resolution operator, and I’ll be discussing other uses for this operator later on in the book. Using the full names in the program will tend to make the code look a bit cluttered, so it would be nice to be able to use their simple names, unqualified by the namespace name, `std`. The two lines in our program that follow the `#include` directive for `<iostream>` make this possible:

```
using std::cout;
using std::endl;
```

These are using declarations that tell the compiler that you intend to use the names `cout` and `endl` from the namespace `std` without specifying the namespace name. The compiler will now assume that wherever you use the name `cout` in the source file subsequent to the first using declaration, you mean the `cout` that is defined in the standard library. The name `cout` represents the standard output stream that by default corresponds to the command line and the name `endl` represents the newline character.

You’ll learn more about namespaces, including how you define your own namespaces, a little later in this chapter.

## The main() Function

The function `main()` in the example consists of the function header defining it as `main()` plus everything from the first opening curly brace (`{`) to the corresponding closing curly brace (`}`). The braces enclose the executable statements in the function, which are referred to collectively as the body of the function.

As you’ll see, all functions consist of a header that defines (amongst other things) the function name, followed by the function body that consists of a number of program statements enclosed between a pair of braces. The body of a function may contain no statements at all, in which case it doesn’t do anything.

A function that doesn’t do anything may seem somewhat superfluous, but when you’re writing a large program, you may map out the complete program structure in functions initially but omit the code for many of the functions leaving them with empty or minimal bodies. Doing this means that you can compile and execute the whole program with all its functions at any time and add detailed coding for the functions incrementally.

## Program Statements

The program statements making up the function body of `main()` are each terminated with a semicolon. It’s the semicolon that marks the end of a statement, not the end of the line. Consequently a statement can be spread over several lines when this makes the code easier to follow and several statements can appear in a single line. The program statement is the basic unit in defining what a program does. This is a bit like a sentence in a paragraph of text, where each sentence stands by itself in expressing an action or an idea, but relates to and combines with the other sentences in the paragraph in expressing a more general idea. A statement is a self-contained definition of an action that the computer is to carry out, but that can be combined with other statements to define a more complex action or calculation.

The action of a function is always expressed by a number of statements, each ending with a semicolon. Take a quick look at each of the statements in the example just written, just to get a general feel for how it works. I will discuss each type of statement more fully later in this chapter.

The first statement in the body of the `main()` function is:

```
int apples, oranges;      // Declare two integer variables
```

This statement declares two variables, `apples` and `oranges`. A variable is just a named bit of computer memory that you can use to store data, and a statement that introduces the names of one or more variables is called a variable declaration. The keyword `int` in the preceding statement indicates that the variables with the names `apples` and `oranges` are to store values that are whole numbers, or integers. Whenever you introduce the name of a variable into a program, you always specify what kind of data it will store, and this is called the type of the variable.

The next statement declares another integer variable, `fruit`:

```
int fruit;                // ...then another one
```

While you can declare several variables in the same statement, as you did in the preceding statement for `apples` and `oranges`, it is generally a good idea to declare each variable in a separate statement on its own line as this enables you to comment them individually to explain how you intend to use them.

The next line in the example is:

```
apples = 5; oranges = 6;    // Set initial values
```

This line contains two statements, each terminated by a semicolon. I put this here just to demonstrate that you can put more than one statement in a line. While it isn’t obligatory, it’s generally good programming practice to write only one statement on a line as it makes the code easier to understand. Good programming practice is about adopting approaches to coding that make your code easy to follow, and minimize the likelihood of errors.

The two statements in the preceding line store the values 5 and 6 in the variables `apples` and `oranges`, respectively. These statements are called assignment statements because they assign a new value to a variable and the `=` is the assignment operator.

The next statement is:

```
fruit = apples + oranges;    // Get the total fruit
```
