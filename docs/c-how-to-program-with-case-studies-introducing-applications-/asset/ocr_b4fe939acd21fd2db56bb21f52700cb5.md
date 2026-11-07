# Outline

+   - 5.1 Introduction
+   - 5.2 Modularizing Programs in C
+   - 5.3 Math Library Functions
+   - 5.4 Functions
+   - 5.5 Function Definitions
+     - 5.5.1 square Function
+     - 5.5.2 maximum Function
+   - 5.6 Function Prototypes: A Deeper Look
+   - 5.7 Function-Call Stack and Stack Frames
+   - 5.8 Headers
+   - 5.9 Passing Arguments by Value and by Reference
+   - 5.10 Random-Number Generation
+   - 5.11 Random-Number Simulation Case Study: Building a Casino Game
+   - 5.12 Storage Classes
+   - 5.13 Scope Rules
+   - 5.14 Recursion
+   - 5.15 Example Using Recursion: Fibonacci Series
+   - 5.16 Recursion vs. Iteration
+   - 5.17 Secure C Programming—Secure Random-Number Generation

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# 5.1 Introduction

Most computer programs that solve real-world problems are much larger than those presented in the first few chapters. Experience has shown that the best way to develop and maintain a program is to construct it from smaller pieces, each of which is more manageable than the original program. This technique is called divide and conquer. We’ll describe some key C features for designing, implementing, operating and maintaining large programs.

# 5.2 Modularizing Programs in C

In C, you use functions to modularize programs by combining the new functions you write with prepackaged C standard library functions. The C standard library provides a rich collection of functions for performing common mathematical calculations, string manipulations, character manipulations, input/output and many other useful operations. Prepackaged functions make your job easier because they provide many of the capabilities you need.

The C standard includes the C language and its standard library—standard C compilers implement both.¹ The functions printf, scanf and pow that we’ve used in previous chapters are from the standard library.

# Avoid Reinventing the Wheel

Familiarize yourself with the rich collection of C standard library functions to help reduce program-development time. When possible, use standard functions instead of writing new ones. The C standard library functions are written by experts, well tested

1. Some C standard library portions are designated as optional and are not available in all standard C compilers.