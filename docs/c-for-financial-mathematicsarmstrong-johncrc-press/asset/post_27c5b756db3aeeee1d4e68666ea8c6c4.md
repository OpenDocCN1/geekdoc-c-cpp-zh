
4.8.7. Make sure that you can write a **for** loop that prints the numbers from 0 to 9 in increasing order without needing to look anything up in this book. This is the C++ equivalent of being able to count to ten in a foreign language without using a phrase book.

## 4.9 Summary

We have learned how to control the flow of execution in C++ using the following keywords:

- **for**
- **while**
- **do**
- **break**
- **continue**
- **return**
- **switch**
- **case**
- **default**
- **throw**

By far the most useful flow of control statements are **for**, **while**, and **throw**.

### Tip: Which control statement to use

- Use **for** statements for simple loops such as for counting from 0 to 99.
- Use **while** statements for more complex looping logic. Unusual **while** statements are easier to read than unusual **for** statements.
- Use **throw** when errors occur. Don’t just print out a message and continue.

## Chapter 5

### Working with Multiple Files

A realistic C++ project will be divided across many files. This helps you organise your code logically into manageable units. This makes it possible to follow large software projects without having to understand every detail.

### 5.1 The project FMLib

If you have completed all the exercises in the previous chapters, you should now have developed quite a collection of functions.

In particular, during the exercises we have written the functions **normcdf** (to compute the cumulative density of the normal distribution) and **norminv** (to compute its inverse). We will want to use these functions repeatedly.

This means that it is time to start creating a better structure for our project. We will stop throwing code away and start work on a long-term project called FMLib.

The goal is that FMLib will be a library of useful financial maths functions. The FM stands for financial maths.

We’re not the first people to think of writing C++ code for financial mathematics. There are many libraries available that you can already download. However, in this book we will pretend that no libraries exist except those built into the C++ standard. We will build everything else ourselves from scratch.

This is a great way to learn C++, but not an intelligent way to build a real-world trading platform. You should, of course, take full advantage of the work done by other people in writing libraries (and even more importantly the work they have put in to designing, testing, and debugging these libraries). Some libraries that you may want to consider using are Boost, GSL, and Quantlib. Boost is a general purpose C++ library that fills in the many gaps in the C++ standard. GSL is a scientific computing library written in C which contains many useful algorithms. QuantLib is a C++ library for mathematical finance.

At this stage, you will probably find the documentation for these libraries impossible to understand. This is because the documentation assumes considerable expertise in the C++ language.

That is why in the rest of this book we will study how to write our own financial maths library FMLib. Once you have mastered this book you should forget about FMLib and learn to use these other libraries instead.

On the website for this book you can find a download called FMLib5. This contains the version of FMLib relevant to Chapter 5. As the book progresses, there are corresponding versions FMLib6, FMLib7, and so forth. These contain increasingly sophisticated code. By the end of the book, we will have developed a fully fledged library.

One aim of this book is to show you how a software project can evolve from simple beginnings to become large and sophisticated. By seeing how a software project can be put together in stages you will learn how to develop your project in manageable pieces. It will also show you how to *refactor* your code. This simply means how to modify your code as you learn from experience to gradually improve your software design.

For the purposes of this chapter, you should download FMLib5. Unzip it and take a look at its contents.

- The file `main.cpp` contains a `main` method for testing.
- The file `matlib.cpp` contains the definitions of various useful financial maths functions. We'll group together many of the standard functions you might expect in MATLAB into this file. For example, `normcdf` and `norminv` are defined in this file.
- The file `stdafx.h` provides a single place to list the libraries we'll want to use throughout the project.
- The file `matlib.h` is a header file containing the declarations of the functions `normcdf` and `norminv`.

As you can see it contains more than one `.cpp` file and some `.h` files. The purpose of this chapter is to explain how C++ code should be arranged using different files in order to develop larger projects and useful libraries. We will use FMLib5 as our example.

### 5.2 Header files

In C++, you can't directly call functions that are defined in other `.cpp` files. To use a function that is defined in another file, you must first load in a "header file" that contains the declaration of that function using the `#include` command.

In case you have forgotten, we discussed the difference between *declaring* a function and *defining* a function in Section 3.4. Briefly, the declaration says *what a function does* and the definition says *how it does it*.

The rule in C++ is that before you can use a function it *must* have been declared. So you must always **\#include** a file where the function is declared if you want to use a function.

You can think of `.cpp` files as communicating via the `.h` files that they include. If two `.cpp` files both **\#include** the same function declarations, then that function only needs to be defined in one of the two `.cpp` files. The same *definition* is shared across multiple files. If two `.cpp` files don't have a `.h` file in common that mentions a particular function, then they can't share that function.

As a matter of convention, whenever we write a `.cpp` file we will typically write another file with the same name, but the extension `.h`. This header file contains function declarations for all the functions we want to be available outside that `.cpp` file.

Some people prefer to use the file name extension `.hpp` for C++ header files and leave `.h` for C header files.

### 5.3 Creating our project

Let us work through a detailed example of how to create a multi-file project.

Begin by creating a new C++ project called *MyLib*. This is to distinguish it from the model code on the website FMLib. When this section is complete, the projects should in fact be identical.

Our aim is to write a small library that makes available a `normcdf` function and a `norminv` function that compute the cumulative distribution function of the normal distribution and its inverse. We also want to make available a standard constant PI.

In a separate file, we want to write a small main function to show how the library can be used.

#### 5.3.1 Creating the first header file

So that other files can use these functions, we will need to declare them in a *header file*. This is a C++ file with the file name extension `.h`.

You should now create a header file called `matlib.h` following the instructions for your development environment below:

- If you are using Visual Studio to create your C++ projects, you should create all `.h` files by right-clicking on the folder **Header Files**.
- If you are using Unix, simply create header files in the same folder as your `.cpp` files but give them the extension `.h`.
- If you are using XCode, press **CMD + N** and select header file.

Now edit the file you have just created and type in the first line:

```cpp
#pragma once
```

Then enter the *declarations* for all the functions we want to make available from our library. In our example, the complete code required is:

```cpp
#pragma once

const double PI = 3.14159265358979;

/**
 * Computes the cumulative
 * distribution function of the
 * normal distribution
 */
double normcdf( double x );

/**
 * Computes the inverse of normcdf
 */
double norminv( double x );
```

This contains the declarations for all the functions we wish to make available. It contains both the declaration and the definition for PI.

In general, you should put the following in your header file:

- (i) The first line **#pragma once**. We’ll explain why shortly.
- (ii) Declarations of functions you wish to make available from your library.
- (iii) Declarations of global variables you wish to make available.
- (iv) Definitions of constant global variables.

Whereas in your source file you should put:

- (i) Definitions of functions declared in the header.
- (ii) Definitions of global variables missing from the header.

We will expand on these rules throughout this book as we meet more types of declaration and definition.

The reason why constants are treated differently is that the C++ compiler can “inline” them. This means to replace every use of the constant with the actual value. This gives a slight performance boost. As a consequence, however, the definition needs to be in the header, so that every file knows the correct value to inline.
