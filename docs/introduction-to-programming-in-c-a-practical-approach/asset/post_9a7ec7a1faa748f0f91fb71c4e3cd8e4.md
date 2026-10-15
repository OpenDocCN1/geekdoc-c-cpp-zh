
# INTRODUCTION TO PROGRAMMING IN C

![](img/e9a40527283d17f2243dedbe472072cc_0_0.png)

A PRACTICAL APPROACH

ENRIQUE VICENTE

# INTRODUCTION TO
PROGRAMMING IN C

![](img/e9a40527283d17f2243dedbe472072cc_1_0.png)

A PRACTICAL APPROACH

# Introduction to programming in C.

# A practical approach.

# Enrique Vicente

# Index

- Introduction to programming in C. A practical approach.
- 1.- Presentation
- 2.- The C language
- 4.- Your first program in C
- 6.- Phases of elaboration of a program. Hello World
- 8.- Description of the part of the program
- 9.- Exercises
- 10.- Variables and types of variables
- 11.- Basic concepts .. memory bits and bytes
- 12.- Variables. Integer and real
- 13.- Mathematical operations
- 14.- Conversion of types
- 15.- Example. Calculation of prices with VAT
- 16.- Making decisions
- 17.- Logical comparisons
- 18.- Relational operators and logical operators
- 19.- Selecting options
- 20.- Example: Basic calculator
- 21.- Advanced topics. Loops
- 22.- Arrays
- 23.- Text strings
- 24.- Exercises for the student
- 25.- Variables and Pointers
- 26.- Dynamic memory
- 27.- Structured programming
- 28.- Data structures
- About the Author

## 1.- Presentation

Hello, I'm Enrique Vicente and I'm going to introduce you to the course "**Introduction to programming. A practical approach**".

This course is aimed to computer enthusiasts who want to enter the exciting world of programming.

This course is not recommended to computer scientists with a high level of knowledge because the concepts explained are introductory.

Students at the end of the course will have a vision of how to learn to program in a language such as C, a versatile and portable language that will help them in the future to program in other languages such as C ++, C # or Java.

They will also have the necessary concepts to understand what a computer program is and what difficulties they may encounter when developing a program and how to solve them.

This course is based on examples and exercises that we will follow step by step to guide you in the world of programming.

### Examples and exercises

Students who are interested can obtain the course examples and additional exercises can sign up to the class Google Classroom https://classroom.google.com/ with the code lq5hhp

Sign up and we can continue with more advanced topics, ask questions or consultations on the topics covered in the course.

I would appreciate that the students who have finished the course to write a review giving their opinion and assessment of the course.

**You can follow us on the blog** [https://evginformatica.blogspot.com](https://evginformatica.blogspot.com) where you will find free courses, tutorials and discounts on upcoming Udemy courses.

## 2.- The C language

C is the ideal language to begin in the world of programming.

It is a compact and very portable language since there are C compilers for many of the platforms of nowadays (Windows, Linux, Mac ...) The C language is used on many areas of programming real applications in the business world and is a good start to start professionally.

Once this language is learned, it can serve as a basis for learning other languages such as C ++, C # or Java with an object orientation philosophy.

## 3.- Downloading and installation of the development environment

Once this short introduction is done, we will present the programming environment that we will use throughout the course.

We will need to download from the internet the tool **Microsoft Visual Studio Community 2017**.

We search in Google Visual Studio 2017 and download the Community version

This development environment has several versions: one free, professional and business.

The differences lie in the use that will be give.

If we are going to start programming, we can do it with the Community version, if we are going to use the tool at work, the professional version is recommended since it provides more components and work tools.

The business version is mainly for team work and allows code sharing among several programmers.

Visual Studio is a development tool based on projects that can be in different languages.

To be able to execute our examples we will install the C/C ++ package for console

Once Visual Studio is installed, we must create project "Windows console application" called courseC in the folder c:\

The development environment offer many options, create projects, compile debug execute, .. we will see all that throughout the course.

Note.
If you work with another operating system other than Windows, you can try running the examples on https://repl.it where you can do tests in several languages, including C.

## 4.- Your first program in C

In this section we will talk about concepts such as machine language, source language and how to translate from one to the other.

We will learn the different phases that we must follow to make a computer program and then we will make our first program.

## 5.- Interpreted and compiled languages

Any program written on a computer must be translated into the machine language.

The machine language is a language that depends on the type of CPU and the manufacturer and there are numerous versions.

As the machine language is very complicated and variable depending on the platform there are some languages (more similar to English) that indicate the sequence of steps to follow (program). These languages are called source code languages and are those used to define the programs of a computer.

Once code in source language, we must pass it through a translator that translates it into machine language, which is what the computer really knows.

There are three types of translations depending on how the machine language is generated from the source code.

### Interpreted languages

The translator reads the source program line by line, translates it and the computer executes it.

With this option the development of a program is faster at the time of writing but has the disadvantage that more errors occur and these are more difficult to correct.

Examples of these types of languages are JavaScript or PHP.

### Compiled languages

After editing the program, this is translated in its entirety (compilation).

At this moment, the syntactic errors that can occur due to the structure of the

program are shown to the operator.

With this option, the development slows down because each time the program is changed, it must be compiled, while the treatment of errors is simpler and easier to debug.

Compiled language examples are C, C ++

### Mixed languages

These are languages that are compiled into an intermediate language and then interpreted into machine language.

They have the same advantages as the compiled languages but are more portable and can be run on machines with different operating systems.

Examples C # or Java

## 6.- Phases of elaboration of a program. Hello World

Now we are going to make our first program in C

Open the VisualStudio and go to File - Open project - courseC

Copy the following piece of code:

```
/* firstprogram.c */

#include "pch.h"
#include <stdio.h>

int main ()
{
    printf ("Hello world! \n");
}
```

Yes, we execute it, we will see a screen with the text Hello World ...

The phases that we will follow to make our programs are

### Phase 1. Define the problem to be solved and elaborate an algorithm (steps to follow)

In this phase we must define clearly what we want make with our program, what inputs you will receive and what outputs you will produce.

We must also indicate in natural language (Spanish, English ...) what steps the program should follow to achieve the objective set.

These steps to follow are what we call the Algorithm of our program.
