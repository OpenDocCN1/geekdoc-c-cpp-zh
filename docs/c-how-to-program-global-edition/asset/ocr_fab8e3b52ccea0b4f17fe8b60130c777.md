+   5.1 Introduction
+   5.2 Modularizing Programs in C
+   5.3 Math Library Functions
+   5.4 Functions
+   5.5 Function Definitions
+   5.5.1 square Function
+   5.5.2 maximum Function
+   5.6 Function Prototypes: A Deeper Look
+   5.7 Function Call Stack and Stack Frames
+   5.8 Headers
+   5.9 Passing Arguments By Value and By Reference
+   5.10 Random Number Generation
+   5.11 Example: A Game of Chance; Introducing enum
+   5.12 Storage Classes
+   5.13 Scope Rules
+   5.14 Recursion
+   5.15 Example Using Recursion: Fibonacci Series
+   5.16 Recursion vs. Iteration
+   5.17 Secure C Programming

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Making a Difference

# 5.1 Introduction

Most computer programs that solve real-world problems are much larger than the programs presented in the first few chapters. Experience has shown that the best way to develop and maintain a large program is to construct it from smaller pieces, each of which is more manageable than the original program. This technique is called divide and conquer. This chapter describes some key features of the C language that facilitate the design, implementation, operation and maintenance of large programs.

# 5.2 Modularizing Programs in C

In C, functions are used to modularize programs. Programs are typically written by combining new functions you write with prepackaged functions available in the C standard library. We discuss both kinds of functions in this chapter. The C standard library provides a rich collection of functions for performing common mathematical calculations, string manipulations, character manipulations, input/output, and many other useful operations. This makes your job easier, because these functions provide many of the capabilities you need.

Good Programming Practice 5.1
Familiarize yourself with the rich collection of functions in the C standard library.

Software Engineering Observation 5.1
Avoid reinventing the wheel. When possible, use C standard library functions instead of writing new functions. This can reduce program development time. These functions are written by experts, well-tested and efficient.

Portability Tip 5.1
Using the functions in the C standard library helps make programs more portable.