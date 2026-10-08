
## Chapter 10: Strings in C

- 10.1 String
- 10.2 Character Array as String
- 10.3 Initializing Strings
- 10.4 Displaying Strings
- 10.5 Manipulating Strings
    - Length of String
    - Comparison of Strings
    - Append Two Strings
    - Reverse a String
    - Converting String to Lower Case
- 10.6 Array of Strings
- Summary
- Review Questions
- Practical Exercises

## Chapter 11: Structures and Unions

- 11.1 What is a Structure
- 11.2 Structures in C Language
- 11.3 Structure Variables
- 11.4 Size of Structure Variables
- 11.5 Assigning Values to Structure Members
- 11.6 Initializing Structure Members
- 11.7 Nested Structure
- 11.8 Array of Structure
- 11.9 Structure and Function
- 11.10 Union
- 11.11 Bit Fields
- Summary
- Review Questions
- Practical Exercises

## Chapter 12: Pointers Revisited

- 12.1 Understanding Pointer Variables
- 12.2 Chain of Pointers
- 12.3 Pointer Expressions
- 12.4 Operations on Pointers
- 12.5 Pointers and Arrays
- 12.6 Pointers and Functions
    - Pointer to Array as Function Parameters
    - Pointer Variable as Function Parameters
    - Functions Returning Pointer
    - Function Pointer
- 12.7 Pointers and Structures
- Summary
- Review Questions
- Practical Exercises

## Chapter 13: Files in C

- 13.1 Concept of File
    - Text File
    - Binary File
    - Text File versus Binary File
- 13.2 Files and Streams
- 13.3 File Operations
- 13.4 Opening and Closing a File
- 13.5 Characters and File
- 13.6 String and File
- 13.7 Integer and File
- 13.8 Function eof()
- 13.9 General I/O in Text Files
- 13.10 I/O in Binary Files
- 13.11 Random File Access
    - Repositioning File Pointer
    - Locating the File Pointer Position
- Summary
- Review Questions
- Practical Exercises

## Chapter 14: Dynamic Memory Allocation

- 14.1 Function for Dynamic Memory Allocation
    - Function malloc
    - Function calloc
    - Function realloc
    - Function free
- 14.2 Concept of Linked List
- Summary
- Review Questions
- Practical Exercises

## Chapter 15: Preprocessor Directives

- 15.1 A Preprocessor Directive
- 15.2 File Inclusion
- 15.3 Macro Expansion
    - Macros with Arguments
    - Advantages of Using Macros
    - Macros versus Functions
- 15.4 #undef Directive
- 15.5 Conditional Compilation
- 15.6 #error Directive
- 15.7 Stringizing Operator
- 15.8 Token-Pasting Operator
- Summary
- Review Questions
- Practical Exercises

## Appendix I: List of Common Header Files and Their Library Functions

## Appendix II: American Standard Code for Information Interchange

## Index

## Introduction

Congratulations on buying the Simplifying C book! The book, Simplifying C, is integrated with the syllabi of several disciplines. It promises to offer a conducive reading for the students of C programming, since C language is taught as the first programming language. This subject is a compulsory subject in many disciplines, such as MCA, BCA, Engineering both at degree and diploma levels. MSc (IT), MSc (Computer Science), DOEACC as well as MBA (IT) courses. The authors have covered the concepts of C programming in reasonable detail considering the requirements of all these courses. The learner does not require any prior programming language knowledge to understand the concepts discussed in this book. Navigating through the chapters and simultaneously practicing the programs given in the book will surely make the learner confident in C programming. Solving the review questions and practical exercises will further make the learner proficient in C programming.

We hope that your learning experience with this book will prove as irresistible to you as it has proved to us while authoring and editing the book.

## About this Book

The book is divided into 15 Chapters starting from the basic to advanced concepts of C programming.

- Chapter 1 introduces the steps to be followed for solving a problem. It discusses three commonly used techniques for problem solving, namely pseudo-code, flowchart, and algorithm. It also discusses the concept of the trace table that is used to verify the correctness of the solution designed.
- Chapter 2 introduces the concept of programming language to users. It discusses history of C language and allows users to write their first C program. It further introduces the user to the structure of a C program. The major components, such as keywords, identifiers, and constants are discussed in detail. The chapter ends with explanation of the execution sequence of a C program.
- In C language, the data used by a program is associated with its type. Chapter 3 discusses the concept of primitive and derived data types. A special attention has been given to the derived data types called pointers and concept of void pointers.
- Inputting data and displaying the result in the format desired by the user is an important activity of any programming language. Chapter 4 discusses the concept of C streams and the inbuilt formatted and unformatted functions available for input and output.
- Chapter 5 discusses how expressions are formed in the C language. In addition, the chapter discusses various operators, such as assignment, relational, increment and decrement, conditional, logical, bitwise, and special in detail.
- Decision making is an important aspect of all programming languages. Chapter 6 discusses the usage of two-way selection and multi-way selection in the C programs. The concepts of repetition and constructs used for implementing repetition in the C language are discussed in Chapter 7.
- C language follows a concept of modular programming. To implement this approach, user defined functions are used in the C language. Chapter 8 elaborates on the use of functions and their types. Recursive functions and command line arguments are also discussed in detail in this chapter.
- A special attention has been given to the derived data type called array. Chapter 9 discusses about dimensions of an array and its usage.
- Chapter 10 concentrates on the character array. Character arrays are used to logically build a data structure called string. The chapter also discusses various operations that can be performed on strings.
- Grouping related data as a single entity is one of the basic requirements in programming. Chapter 11 discusses the concepts of the derived data types, such as structure and union that are used to logically group related data.
- Chapter 12 is an important chapter for the advanced users of C programming. The concepts of pointers have been revisited here. The chapter presents an elaborate discussion on how the pointers are associated with different components of the C language.
- Storing and retrieving data from a secondary storage is a necessity in almost all practical solutions. Chapter 13 discusses the concepts of files. It also explains the file handling function available in the C library in detail.
- Chapter 14 discusses the concept of runtime memory allocation and also gives a brief idea about a popular data structure called the link list.
- Finally, Chapter 15 discusses the usage of preprocessor directives and how they improve the readability of C programs.
- The appendices list the commonly-used C library functions and their usage. It also contains an ASCII table.

Our sole intent has been to provide a book with in-depth and sufficient information, so that you enjoy reading and learning from it. Happy reading!

### How to Use This Book

In this book, code snippets and programs have been tested on a variety of C compilers, such as Turbo C++, Borland, gcc and Visual Studio 6.0. However, you need to add some additional lines of code to compile and execute the C programs, depending upon the compiler you use.

### Conventions

There are a few conventions followed in this book that need to be taken care of. For example, the code explained in this book is in the form of code listing or program, which is immediately followed by the output of the listing/Program. The code with a listing/program number and caption, and its output appears as follows:

▶ Program 1

```c
/* Program to illustrate the use of integer arithmetic */
#include <stdio.h>
main( )
{
/* Declare variables */
```
