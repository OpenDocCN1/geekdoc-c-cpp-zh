
Mike McGrath

## C Programming

grasp the nuts and bolts of programming

5th Edition

in easy steps

- PLAIN ENGLISH
- EASY TO FOLLOW
- FULLY ILLUSTRATED
- IN FULL COLOR

- switch
- case
- enum
- register
- typedef
- char
- extern
- return
- union
- const
- float
- short
- unsigned
- continue
- for
- signed
- void
- default
- goto
- sizeof
- volatile
- do
- if
- static
- while

```
#include <stdio.h>
int main() {
  int i, j;
  for (i = 1; i <= 4; i++) {
    printf ("Outer loop iteration %d\n", i);
    for (j = 1; j <= 3; j++) {
      printf ("\t Inner loop iteration %d\n", j);
    }
  }
}
```

![](img/db19f3858a1e321646bf2590afd29547_0_0.png)

Mike McGrath

## C Programming

![](img/db19f3858a1e321646bf2590afd29547_1_0.png)

fifth edition

In easy steps is an imprint of In Easy Steps Limited

16 Hamilton Terrace, Holly Walk, Leamington Spa, Warwickshire, United Kingdom, CV32 4LY

www.ineasysteps.com

5th Edition

Copyright © 2018 by In Easy Steps Limited. All rights reserved. No part of this book may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage or retrieval system, without prior written permission from the publisher.

### Notice of Liability

Every effort has been made to ensure that this book contains accurate and current information. However, In Easy Steps Limited and the author shall not be liable for any loss or damage suffered by readers as a result of any information contained herein.

### Trademarks

All trademarks are acknowledged as belonging to their respective companies.

## 1 Getting Started

- Introducing the C language
- Installing a C compiler
- Writing a C program
- Compiling a C program
- Understanding compilation
- Summary

## 2 Storing Variable Values

- Creating program variables
- Displaying variable values
- Inputting variable values
- Qualifying data types
- Using global variables
- Registering variables
- Converting data types
- Creating array variables
- Describing dimensions
- Summary

## 3 Setting Constant Values

- Declaring program constants
- Enumerating constant values
- Creating a constant type
- Defining constants
- Debugging definitions
- Summary

## 4 Performing Operations

- Doing arithmetic
- Assigning values
- Comparing values
- Assessing logic
- Examining conditions
- Measuring size
- Comparing bit values
- Flagging bits
- Understanding precedence
- Summary

## 5 Making Statements

- Testing expressions
- Branching switches
- Looping for a number
- Looping while true
- Breaking out of loops
- Going to labels
- Summary

## 6 Employing Functions

- Declaring functions
- Supplying arguments
- Calling recursively
- Placing functions in headers
- Restricting accessibility
- Summary

## 7 Pointing to Data

- Accessing data via pointers
- Doing pointer arithmetic
- Passing pointers to functions
- Creating arrays of pointers
- Pointing to functions
- Summary

## 8 Manipulating Strings

- Reading strings
- Copying strings
- Joining strings
- Finding substrings
- Validating strings
- Converting strings
- Summary

## 9 Building Structures

- Grouping in a structure
- Defining type structures
- Using pointers in structures
- Pointing to structures
- Passing structures to functions
- Grouping structures in a union
- Allocating memory
- Summary

## 10 Producing Results

- Creating a file
- Reading & writing characters
- Reading & writing lines
- Reading & writing entire files
- Scanning file streams
- Reporting errors
- Getting the date and time
- Running a timer
- Generating random numbers
- Displaying a dialog box
- Summary

## Reference Section

- ASCII character codes
- Input & output functions
- Character test functions
- String functions
- Math functions
- Utility functions
- Diagnostic functions
- Argument functions
- Date & time functions
- Jump functions
- Signal functions
- Limit constants
- Float constants

## Preface

The creation of this book has provided me, Mike McGrath, a welcome opportunity to update my previous books on C programming with the latest techniques. All examples I have given in this book demonstrate C features supported by current compilers on both Windows and Linux operating systems, and the book’s screenshots illustrate the actual results produced by compiling and executing the listed code.

### Conventions in this book

In order to clarify the code listed in the steps given in each example, I have adopted certain colorization conventions. Components of the C language itself are colored blue; numeric and string values are red; programmer-specified names are black; and comments are green, like this:

```
/* Store then output a text string value. */
char *myMessage = "Hello from C";
printf( myMessage );
```

Additionally, in order to identify each source code file described in the steps, a colored icon and file name appears in the margin alongside the steps:

![](img/db19f3858a1e321646bf2590afd29547_6_0.png)

main.c

![](img/db19f3858a1e321646bf2590afd29547_6_1.png)

header.h

### Grabbing the source code

For convenience I have placed source code files from the examples featured in this book into a single ZIP archive, which you can obtain by following these easy steps:

## 1 Getting Started

*Welcome to the world of C. This chapter demonstrates how to create a C program in text, then how to compile it into executable byte form.*

- Introducing the C language
- Installing a C compiler
- Writing a C program
- Compiling a C program
- Understanding compilation
- Summary

### Introducing the C language

C is a compact, general-purpose computer programming language that was originally developed by Dennis MacAlistair Ritchie for the Unix operating system. It was first implemented on the Digital Equipment Corporation PDP-11 computer in 1972.

![](img/db19f3858a1e321646bf2590afd29547_9_0.png)

Dennis M. Ritchie, creator of the C programming language.

This new programming language was named “C” as it succeeded an earlier programming language named “B” that had been introduced around 1970.

The Unix operating system and virtually all Unix applications are written in the C language. However, C is not limited to a particular platform and programs can be created on any machine that supports C, including those running the Windows platform.

The flexibility and portability of C made it very popular and the language was formalized in 1989 by the American National Standards Institute (ANSI). The ANSI standard unambiguously defined each aspect of C, thereby eliminating previous uncertainty about the precise syntax of the language.

ANSI C has become the recognized standard for the C language and is described, and demonstrated by examples, in this book.

The C language has been around for quite some time and has seen the introduction of newer programming languages like Java, C++, and C#. Many of these new languages are derived, at least in part, from C – but are much larger in size. The more compact C is better to start out in programming because it’s simpler to learn.

It is easier to move on to learn the newer languages once the principles of C programming have been grasped. For instance, C++ is an extension of C and can be difficult to learn unless you have mastered C programming first.

Despite the extra features available in newer languages, C remains popular because it is versatile and efficient. It is used today on a large number of platforms, for everything from micro-controllers to the most advanced scientific systems. Programmers around the world embrace C because it allows them maximum control and efficiency in their programs.

![](img/db19f3858a1e321646bf2590afd29547_10_0.png)

Programs written 20 years ago in C are still just as valid today as they were back then.

### Standard C libraries

ANSI C defines a number of standard libraries that contain tried-and-tested functions, which can be used in your own C programs.

The libraries are contained in “header files” that each has a file extension of “.h”. The names of the standard C library header files are listed in the table below with a description of their purpose:

| Library: | Description: |
|---|---|
| stdio.h | Contains input and output functions, types, and macro definitions. This library is used by most C programs and represents almost one third of the entire C libraries |
| ctype.h | Contains functions for testing characters |
| string.h | Contains functions for manipulating strings |
| math.h | Contains mathematical functions |
| stdlib.h | Contains utility functions for number conversion, storage allocation, etc. |
| assert.h | Contains a function that can be used to add diagnostics to a program |
