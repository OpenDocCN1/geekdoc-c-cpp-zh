
This edition comes with a CD which provides

- More than 600 objective/review/debugging questions (8 units)
- 100 Programming exercises
- Model question paper
- 2006 and 2007 solved question paper
- Computer programs for lab

The objective of the supplementary CD is to make the students learn the programming language and enable them to write their own programs using C and data structures.

The author is grateful to Mr A Rama Rao, Loyola Institute of Technology & Management, Guntur and Mr P Chenna Reddy, JNTU College of Engineering, Pulivendula for their useful comments and suggestions.

E BALAGURUSAMY

## Road Map to the Syllabus

(Effective from August 2007)

Jawaharlal Nehru Technological University Hyderabad

I Year B.Tech

| T | P | C |
|---|---|---|
| 4 | 0 | 6 |

## C Programming and Data Structures

## Objectives

- To make the student learn a programming language.
- To teach the student to write programs in C to solve the problems.
- To introduce the student to simple linear and non-linear data structures such as lists, stacks, queues, trees and graphs.

## Syllabus

## Unit I

Algorithm / pseudo code, flowchart, program development steps, structure of C program, a simple C program, identifiers, basic data types and sizes, constants, variables, arithmetic, relational and logical operators, increment and decrement operators, conditional operator, bit-wise operators, assignment operators, expressions, type conversions, conditional expressions, precedence and order of evaluation.

Input-output statements, statements and blocks, if and switch statements, loops- while, do-while and for statements, break, continue, goto and labels, programming examples.

- Go To
- CHAPTER 1 – ALGORITHMS
- CHAPTER 2 – OVERVIEW OF C
- CHAPTER 3 – CONSTANTS, VARIABLES, AND DATA TYPES
- CHAPTER 4 – OPERATORS AND EXPRESSIONS
- CHAPTER 5 – MANAGING INPUT AND OUTPUT OPERATIONS
- CHAPTER 6 – DECISION MAKING AND BRANCHING
- CHAPTER 7 – DECISION MAKING AND LOOPING

## Unit II

Designing structured programs, functions, basics, parameter passing, storage classes- extern, auto, register, static, scope rules, block structure, user-defined functions, standard library functions, recursive functions, header files, C preprocessor, C program examples.

- Go To
- CHAPTER 7 – DECISION MAKING AND LOOPING
- CHAPTER 10 – USER-DEFINED FUNCTIONS

## Unit III

Arrays- concepts, declaration, definition, accessing elements, storing elements, arrays and functions, two-dimensional and multi-dimensional arrays, applications of arrays. pointers- concepts, initialization of pointer variables, pointers and function arguments, address arithmetic, character pointers and functions, pointers to pointers, pointers and multidimensional arrays, dynamic memory management functions, command line arguments, C program examples.

- CHAPTER 8 – ARRAYS
- CHAPTER 9 – HANDLING OF CHARACTER STRINGS
- CHAPTER 11 – POINTERS

## Unit IV

Derived types- structures- declaration, definition and initialization of structures, accessing structures, nested structures, arrays of structures, structures and functions, pointers to structures, self-referential structures, unions, typedef, bitfields, C program examples.

- CHAPTER 12 – STRUCTURES AND UNIONS
- CHAPTER 15 – DYNAMIC MEMORY ALLOCATION AND LINKED LISTS

## Unit V

Input and output – concept of a file, text files and binary files, streams, standard I/O, formatted I/O, file I/O operations, error handling, C program examples.

- CHAPTER 13 – FILE MANAGEMENT IN C

## Unit VI

Searching – linear and binary search methods, sorting – bubble sort, selection sort, insertion sort, quick sort, merge sort.

- CHAPTER 17 – SORTING AND SEARCHING TECHNIQUES

## Unit VII

Introduction to data structures, singly linked lists, doubly linked lists, circular list, representing stacks and queues in C using arrays and linked lists, infix to post fix conversion, postfix expression evaluation.

- CHAPTER 14 – DATA STRUCTURES
- CHAPTER 15 – DYNAMIC MEMORY ALLOCATION AND LINKED LISTS

## Unit VIII

Trees- binary trees, terminology, representation, traversals, graphs—terminology, representation, graph traversals (dfs and bfs)

- CHAPTER 16 – BINARY TREES AND GRAPHS

## The C99 Standard

Computer languages are not static; they evolve, reacting to changes in methodologies, applications, generally accepted practices, and hardware. C is no exception. In the case of C, two evolutionary paths were set in motion. The first is the continuing development of the C language. The second is C++, for which C provided the starting point. While most of the focus of the past several years has been on C++, the refinement of C has continued unabated.

For example, reacting to the internationalization of the computing environment, the original C89 standard was amended in 1995 to include various wide-character and multibyte functions. Once the 1995 amendment was complete, work began on updating the language, in general. The end result is, of course, C99. In the course of creating the 1999 standard, each element of the C language was thoroughly reexamined, usage patterns were analyzed, and future demands were anticipated. As expected, C's relationship to C++ provided a backdrop for the entire process. The resulting C99 standard is a testimonial to the strengths of the original. Very few of the key elements of the C were altered. For the most part, the changes consist of a small number of carefully selected additions to the language and the inclusion of several new library functions. Thus C is still C!

Here we will examine those features added by C99, and the few differences between C99 and C89.

## C99

Perhaps the greatest cause for concern that accompanies the release of a new language standard is the issue of compatibility with its predecessor. Does the new specification render old programs obsolete? Have important constructs been altered? Do I have to change the way that I write code? The answers to these types of questions often determine the degree to which the new standard is accepted and, in the longer term, the viability of the language itself. Fortunately, the creation of C99 was a controlled, even-handed process that reflects the fact that several experienced pilots were at the controls. Put simply: If you liked C the way it was, you will like the version of C defined by C99. What many programmers think of is the world's most elegant programming language, still is! In this chapter we will examine the changes and additions made to C by the 1999 standard. Many of these changes were mentioned in passing in Part One. Here they are examined in closer detail. Keep in mind, however, that as of this writing, there are no widely used compilers that support many of C99's new features. Thus, you may need to wait a while before you can 'test drive' such exciting new constructs as variable-length arrays, restricted pointers, and the long long data type.

## C89 vs. C99: AN OVERVIEW

There are three general categories of changes between C89 and C99:

- Features added to C89
- Features removed from C89
- Features that have been changed or enhanced

Many of the differences between C89 and C99 are quite small, and clarify nuances of the C language.
This book will concentrate on the larger changes that affect the way programs are written.

## Features Added

Perhaps the most important features added by C99 are the new keywords:

- inline
- restrict
- _Bool
- _Complex
- _Imaginary

Other major additions include

- Variable-length arrays
- Support for complex arithmetic
- The long long int data type
- The //comment
- The ability to intersperse code and data
- Additions to the preprocessor
- Variable declarations inside the for statement
- Compound literals
- Flexible array structure members
- Designated initializers
- Changes to the printf() and scanf() family of functions
- The __func__ predefined identifier
- New libraries and headers

Most of the features added by C99 are innovations created by the standardization committee, of which many were based on language extensions offered by a variety of C implementations. In a few cases, however, features were borrowed from C++. The inline keyword and // style comments are examples. It is important to understand that C99 does not add C++-style classes, inheritance, or member functions. The consensus of the committee was to keep C as C.

## Features Removed

The single most important feature removed by C99 is the “implicit int” rule. In C89, in many cases when no explicit type specifier is present, the type int is assumed. This is not allowed by C99. Also removed is implicit function declaration. In C89, if a function was not declared before it is used, an implicit declaration is assumed. This is not supported by C99. Both of these changes may require existing code to be rewritten if compatibility with C99 is desired.
