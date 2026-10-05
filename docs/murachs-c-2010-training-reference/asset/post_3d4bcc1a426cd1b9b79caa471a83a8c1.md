
# TRAINING & REFERENCE

# murach's C# 2010

JOEL MURACH

A SELF-PACED, PROFESSIONAL BOOK
shows you how to use Visual Studio, C#, and the
.NET classes to develop Windows Forms applications

AN OBJECT-ORIENTED BOOK
THAT shows you how to use business classes, inheritance,
and interfaces the way they're used in the real world

AN INTRODUCTION TO DATABASE PROGRAMMING
that shows you how to start developing professional
database applications with data sources,
DataGridView control, and ADO.NET code

A GUIDE TO WORK-SAVING VISUAL STUDIO AND C# FEATURES
including 2010 features like optional parameters,
named arguments, and code stubs, as well as earlier
features like *LINQ*

# TRAINING & REFERENCE

# murach's C# 2010

Joel Murach

MIKE MURACH & ASSOCIATES, INC.
1-800-221-5528 • (559) 440-9071 • Fax: (559) 440-0963
murachbooks@murach.com • www.murach.com

Author: Joel Murach

Editors: Anne Boehm
Prentiss Knowhton

Cover Design: Zylka Design

Production: Tom Murach
Cynthia Vasquez

# Books for .NET developers

- Murach's C# 2010
- Murach's ADO.NET 4 Database Programming with C# 2010
- Murach's ASP.NET 4 Web Programming with C# 2010
- Murach's Visual Basic 2010
- Murach's ADO.NET 4 Database Programming with VB 2010
- Murach's ASP.NET 4 Web Programming with VB 2010
- Murach's C++ 2008
- Murach's SQL Server 2008 for Developers

# Books for web developers

- Murach's HTML, XHTML, and CSS
- Murach's JavaScript and DOM Scripting
- Murach's PHP and MySQL

# Books for Java programmers

- Murach's Java SE 6
- Murach's Java Servlets and JSP (2nd Ed.)
- Murach's Oracle SQL and PL/SQL

Please check www.murach.com
for the most up-to-date Murach books

© 2010, Mike Murach & Associates, Inc.
All rights reserved.
Printed in the United States of America
10 9 8 7 6 5 4 3 2
ISBN-13: 978-1-890774-59-2

# Contents

Introduction

## Section 1 An introduction to Visual Studio

| Chapter | Title | Page |
| :--- | :--- | :--- |
| Chapter 1 | How to get started with Visual Studio | 3 |
| Chapter 2 | How to design a Windows Forms application | 35 |
| Chapter 3 | How to code and test a Windows Forms application | 57 |

## Section 2 The C# language essentials

| Chapter | Title | Page |
| :--- | :--- | :--- |
| Chapter 4 | How to work with numeric and string data | 97 |
| Chapter 5 | How to code control structures | 135 |
| Chapter 6 | How to code methods and event handlers | 161 |
| Chapter 7 | How to handle exceptions and validate data | 185 |
| Chapter 8 | How to use arrays and collections | 213 |
| Chapter 9 | How to work with dates and strings | 253 |
| Chapter 10 | More skills for working with Windows forms and controls | 279 |
| Chapter 11 | How to debug an application | 321 |

## Section 3 Object-oriented programming

| Chapter | Title | Page |
| :--- | :--- | :--- |
| Chapter 12 | How to create and use classes | 353 |
| Chapter 13 | How to work with indexers, delegates, events, and operators | 393 |
| Chapter 14 | How to work with inheritance | 421 |
| Chapter 15 | How to work with interfaces and generics | 459 |
| Chapter 16 | How to organize and document your classes | 489 |

## Section 4 Database programming

| Chapter | Title | Page |
| :--- | :--- | :--- |
| Chapter 17 | An introduction to database programming | 509 |
| Chapter 18 | How to work with data sources and datasets | 541 |
| Chapter 19 | How to work with bound controls and parameterized queries | 583 |
| Chapter 20 | How to use ADO.NET to write your own data access code | 619 |

## Section 5 Other skills for C# developers

| Chapter | Title | Page |
| :--- | :--- | :--- |
| Chapter 21 | How to work with files and data streams | 661 |
| Chapter 22 | How to work with XML files | 683 |
| Chapter 23 | How to use LINQ | 705 |
| Chapter 24 | How to enhance the user interface | 731 |
| Chapter 25 | How to deploy an application | 755 |

## Reference aids

| Appendix | Title | Page |
| :--- | :--- | :--- |
| Appendix A | How to install and use the software and files for this book | 783 |
| Index | | 793 |

# Expanded contents

# Section 1 An introduction to Visual Studio

# Chapter 1 How to get started with Visual Studio

- An introduction to .NET development ................................ 4
- Windows Forms and Web Forms applications ............................ 4
- Visual Studio and the .NET programming languages ................. 6
- The .NET Framework ..................................................... 8
- The Visual Studio IDE ................................................................ 10
- How a C# application is compiled and run ............................... 12
- How C# differs from the other, .NET languages ........................ 12
- How C# differs from Java ............................................................ 12
- A tour of the Visual Studio IDE ................................................... 14
- How to start Visual Studio ................................................ 14
- How to open or close an existing project ............................... 16
- Some possible variations ................................................. 18
- How to use the Form Designer ................................................ 18
- How to use the Code Editor ................................................ 20
- How to use the Solution Explorer ....................................... 22
- How to work with Visual Studio's ............................................... 24
- How to test a project ..................................................... 26
- How to build a project ................................................ 26
- How to run a project ................................................................ 26
- How to convert projects and change .NET versions ................... 28
- How to convert projects in earlier versions of C# ........................ 28
- How to change the .NET Framework used by a project ............................... 30

# Chapter 2 How to design a Windows Forms application

- How to set options and create a new project ................... 36
- How to set the Visual Studio options ................................................ 36
- How to import and export settings ............................ 36
- How to create a new project ................................................ 38
- How to design a form ....................................................... 40
- The design of the Invoice Total form ........................................ 40
- How to add controls to a form ................................ 42
- How to set properties ................................................ 44
- Common properties for forms and controls ............................ 46
- How to add features ................................... 48
- The property settings for the Invoice Total form ....................... 50
- How to use the Outline view ........................................ 50
- How to name and save the files of a project ................................ 52
- How to save the files of a project ........................................ 52

# Chapter 3 How to code and test a Windows Forms application

- Introduction to coding .......................................... 58
- Introduction to object-oriented programming ................... 58
- How to refer to properties, methods, and events ................................ 60
- How an application responds to events ................................ 62
- How to add code to a form ................................................................ 64
- How to create an event handler for the default event of a form or control ...... 64
- How to delete an event handler ....................................................... 64
- How IntelliSense helps you enter the code for a form ....................... 66
- The event handlers for the Invoice Total form .......................................... 68
- How to detect and correct syntax errors ................................................ 70

# More coding skills ................................................................. 72

- How to code with a readable style ........................................................ 72
- How to code comments ....................................................... 74
- How to work with the Text Editor toolbar ...................................... 76
- How to collapse or expand blocks of code ................................... 76
- How to zoom in and out ............................................................. 78
- How to highlight symbols ........................................................ 78
- How to print the source code ................................................ 80
- How to use code snippets ....................................................... 82
- How to refactor code ............................................................ 82
- How to get help information ............................................... 84

# How to run, test, and debug a project ................................................ 86

- How to run a project ............................................................ 86
- How to test a project .......................................................... 88
- How to debug runtime errors ....................................... 90

# Section 2 The C# language essentials

# Chapter 4 How to work with numeric and string data

- How to work with the built-in value types ................................... 98
- The built-in value types ........................................ 98
- To declare and initialize variables ........................................ 100
- To declare and initialize constants .......................... 100
- To code arithmetic expressions ................................... 102
- To code assignment statements ................................... 104
- How to work with the order of precedence ................... 106
- To use casting ................................................... 108
- How to use the Math class ........................................ 110

# How to work with strings ............................................... 112

- To declare and initialize a string ...................... 112
- To join and append strings ................................... 112
- To include special characters in strings ................ 114

# How to convert data types ...................................... 116

- The .NET structures and classes that define data types... 116
- To use methods to convert data types ............................... 118
- To use methods to convert numbers to formatted strings 120

# Three other skills for working with data ................ 122

- How to work with scope ....................................... 122
- To declare and use enumerations ............... 124
- How to work with nullable types ............... 126

# Two versions of the Invoice Total application ... 128

- The basic Invoice Total application ............ 128
- The enhanced Invoice Total application ............... 130
