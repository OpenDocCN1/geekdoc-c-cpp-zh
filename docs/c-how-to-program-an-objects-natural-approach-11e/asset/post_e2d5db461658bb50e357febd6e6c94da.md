
![](img/7b5e2088e71c7f78681d4ddbcf104c06_245_0.png)

### 4.20 (Modified Diamond-Printing Program)

Modify the application you wrote in Exercise 4.19 to read an odd number in the range 1 to 19 to specify the number of rows in the diamond. Your program should then display a diamond of the appropriate size.

### 4.21 (Removing break and continue)

A criticism of the break and continue statement is that each is unstructured. Actually, these statements can always be replaced by structured statements, although doing so can be awkward. Describe in general how you’d remove any break statement from a loop in a program and replace it with some structured equivalent. [Hint: The break statement exits a loop from the body of the loop. The other way to exit is by failing the loop-condition test. Consider using in the loop-continuation test a second test that indicates “early exit because of a ‘break’ condition.”] Use the technique you develop here to remove the break statement from the application in Fig. 4.8.

### 4.22 (What Does This Code Do?)

What does the following program segment do?

```cpp
for (int i{1}; i <= 5; i++) {
    for (int j{1}; j <= 5; j++) {
        for (int k{1}; k <= 4; k++) {
            cout << '*';
        }
        cout << '\n';
    }
    cout << '\n';
}
```

### 4.23 (Replacing continue with a Structured Equivalent)

Describe in general how you’d remove any continue statement from a loop in a program and replace it with some structured equivalent. Use the technique you develop here to remove the continue statement from the program in Fig. 4.9.

### 4.24 (“The Twelve Days of Christmas” Song)

Find the lyrics to the song “The Twelve Days of Christmas” online, then write an application using iteration and switch to print the song. One switch statement should be used to print the day (“first,” “second,” and so on). A separate switch statement should be used to print the remainder of each verse.

### 4.25 (Peter Minuit Problem)

Legend has it that, in 1626, Peter Minuit purchased Manhattan Island for $24.00 in barter. Did he make a good investment? To answer this question, modify the compound-interest program of Fig. 4.4 to begin with a principal of $24.00 and to calculate the amount of interest on deposit if that money had been kept on deposit until this year (e.g., 397 years through 2023). Place the for loop that performs the compound-interest calculation in an outer for loop that varies the interest rate from 5% to 10% to observe the wonders of compound interest.

This page intentionally left blank

## Functions and an Intro to Function Templates

![](img/7b5e2088e71c7f78681d4ddbcf104c06_247_0.png)

### Objectives

- Construct programs modularly from functions.
- Use math library functions and learn about math functions and constants added in recent C++ versions.
- Declare functions with function prototypes.
- View many key C++ standard library headers.
- Use random numbers to implement game-playing apps.
- Declare constants in scoped enums and use constants without their type names via C++20’s using enum declarations.
- Use inline functions, references and default arguments.
- Define overloaded functions of the same name that handle various argument types.
- Define function templates that can conveniently generate families of overloaded functions.
- Write and use recursive functions.
- Understand the scope of identifiers.
- Zajnproc vrq lnfylun lqhtomh uqrmnhzq tubp j dvql pspru iw dmwwqnddwjqz (see Section 5.19).

### Outline

- 5.1 Introduction
- 5.2 C++ Program Components
- 5.3 Math Library Functions
- 5.4 Function Definitions and Function Prototypes
- 5.5 Order of Evaluation of a Function’s Arguments
- 5.6 Function-Prototype and Argument-Coercion Notes
  - 5.6.1 Function Signatures and Function Prototypes
  - 5.6.2 Argument Coercion
  - 5.6.3 Argument-Promotion Rules and Implicit Conversions
- 5.7 C++ Standard Library Headers
- 5.8 Case Study: Random-Number Generation
  - 5.8.1 Rolling a Six-Sided Die
  - 5.8.2 Rolling a Six-Sided Die 60,000,000 Times
  - 5.8.3 Seeding the Random-Number Generator
  - 5.8.4 Seeding the Random-Number Generator with random_device
- 5.9 Case Study: Game of Chance; Introducing Scoped enums
- 5.10 Function-Call Stack and Activation Records
- 5.11 Inline Functions
- 5.12 References and Reference Parameters
- 5.13 Default Arguments
- 5.14 Function Overloading
- 5.15 Function Templates
- 5.16 Recursion
  - 5.16.1 Factorials
  - 5.16.2 Recursive Factorial Example
  - 5.16.3 Recursive Fibonacci Series Example
  - 5.16.4 Recursion vs. Iteration
- 5.17 Scope Rules
- 5.18 Unary Scope Resolution Operator
- 5.19 In-flyin Lhqtomh Wjtz Qarvc: Qjwa… (text unclear)
- 5.20 Wrap-Up
- Exercises

### 5.1 Introduction

In this chapter, we introduce building custom function definitions. We overview some C++ standard library math functions and constants added in recent C++ versions. We introduce function prototypes and discuss how the compiler uses them, if necessary, to convert the type of an argument in a function call to the type specified in a function’s parameter list. We also present an overview of the C++ standard library’s headers.

Next, we demonstrate simulation techniques with random-number generation. We simulate a popular casino dice game that uses most of the C++ capabilities we’ve presented. In the game, we show how to declare constants in scoped enums and discuss C++20’s using enum declarations for accessing scoped enum constants directly without their type name.

We discuss features that help improve program performance, including inline functions that can eliminate a function call’s overhead and reference parameters for efficiently passing large data items to functions. Many applications you develop will have multiple functions with the same name. You’ll use this “function overloading” technique to implement functions that perform similar tasks for arguments of different types or different numbers of arguments. We introduce function templates, which enable you to conveniently define families of overloaded functions.

We also demonstrate recursive functions that call themselves, directly or indirectly, through another function. We then present C++’s scope rules for determining where identifiers can be referenced in a program. Cujuumtl, ul znkfehdf jsy lqagynb-orbtozi mljapvao thqt w wjtz qarcv aj wazkrvdqkbu (see Section 5.19).

Perf

Sec

### 5.2 C++ Program Components

You typically write C++ programs by combining

- prepackaged functions and classes available in the C++ standard library,
- functions and classes available in a vast number of open-source and proprietary third-party libraries, and
- new functions and classes you and your colleagues write.

The C++ standard library provides a rich collection of functions and classes for

- math,
- string processing,
- regular expressions,
- input/output,
- file processing,
- dates and times,
- containers (collections of data),
- algorithms for manipulating the contents of containers,
- memory management,
- concurrent programming,
- and more.

Functions and classes allow you to separate a program’s tasks into small self-contained units. So far, each program you’ve seen has used a combination of C++ standard library features and the main function. In addition, some programs used open-source library features. In this chapter, you’ll begin defining custom functions and starting in Chapter 9, you’ll define custom classes.

Some motivations for using functions and classes to create program components include:

- Software reuse. For example, in earlier programs, we did not have to define how to create and manipulate strings or read a line of text from the keyboard. C++ provides these capabilities via the <string> header’s string class and getline function.
- Avoiding code repetition.
- Hiding complexity.
- Easier testing, debugging and maintenance.

To promote reusability, every function should perform a single, well-defined task, and the function’s name should express that task effectively. We’ll say lots more about software reusability in our treatment of object-oriented programming. C++20 introduces another construct called modules, which we will discuss in Chapter 16.
