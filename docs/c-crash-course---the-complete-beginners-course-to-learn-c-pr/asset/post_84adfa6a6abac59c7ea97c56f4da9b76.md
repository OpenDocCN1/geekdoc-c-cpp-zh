
# C# SERIES

# C# CRASH COURSE

The Complete Beginner's Course to Learn C# Programming in 15 Clear-Cut Lessons

ALPHY BOOKS

# C# CRASH COURSE

The Complete Beginner's Course to Learn C# Programming in 15 Clear-Cut Lessons - Including Dozens of Practical Examples & Exercises

By Alphy Books

Copyright © 2017

All rights reserved. No part of this publication may be reproduced, distributed or transmitted in any form or by any means, including photocopying, recording, or other electronic or mechanical methods, without the prior written permission of the publisher, except in the case of brief quotations embodied in reviews and certain noncommercial uses permitted by copyright law.

Trademarked names appear throughout this book. Rather than use a trademark symbol with every occurrence of a trademark name, names are used in an editorial fashion, with no intention of infringement of the respective owner's trademark.

The information in this book is distributed on an "as is" basis, exclusively for educational purposes, without warranty. Neither the author nor the publisher shall have any liability to any person or entity with respect to any loss or damage caused or alleged to be caused directly or indirectly by the information contained in this book.

# Table of Contents

CHAPTER 1 : INTRODUCTION

CHAPTER 2 : C# PROGRAMMING LANGUAGE

WHY USE C#

WHAT IS C# USED FOR?

WHAT TOOLS DO YOU NEED?

SOME BASIC BEST PRACTICES

LAB QUESTIONS

CHAPTER 3 : DATA TYPES

BASIC DATA TYPE SYNTAX

THE STRING DATA TYPE

CUSTOM DATA TYPES

CONSTANTS

LAB QUESTIONS

CHAPTER 4 : OPERATORS

MATHEMATICAL OPERATORS

RELATIONAL OPERATORS

LOGICAL OPERATORS

THE ASSIGNMENT OPERATOR

LAB QUESTIONS

CHAPTER 5 : LOOPS AND IF STATEMENTS

THE FOR LOOP

THE WHILE LOOP

THE IF STATEMENT

THE SWITCH STATEMENT

LAB QUESTIONS

# CHAPTER 6: INTRODUCTION TO OOP

UNDERSTANDING OOP Basics

THE PUBLIC SPECIFIER

THE PRIVATE SPECIFIER

SETTING CLASSES AS PROTECTED

LAB QUESTIONS

# CHAPTER 7: CLASSES

INTRODUCTION TO CLASSES

CREATING CLASS CONSTRUCTORS

CREATING METHODS IN YOUR CODE

USING Properties

LAB QUESTIONS

# CHAPTER 8: STRUCTURES AND ENUMS

WHY USE A STRUCTURE OR Enum INSTEAD OF A Class?

USING Structures

CREATING Enums

LAB QUESTIONS

# CHAPTER 9: INHERITANCE

UNDERSTANDING BASIC Inheritance

INHERITING FROM A Parent Class

INHERITANCE AND INTERFACES

STATIC Classes

LAB QUESTIONS

# CHAPTER 10: ARRAYS

Declaring an Array in C#

Filling AN ARRAY WITH VALUES

RETRIEVE VALUES FROM AN ARRAY

Using AN ARRAYList

LAB QUESTIONS

# CHAPTER 11: GENERICS

INTRODUCTION TO GENERICS

CREATING YOUR OWN GENERIC TYPES

USING THE LIST GENERIC CLASS

USING THE LIST CLASS FOR CUSTOM CLASS STRUCTURES

LAB QUESTIONS

# CHAPTER 12: FILE I/O

WRITING TO FILES

READING FROM FILES

APPENDING TO A FILE

DELETING A FILE

LAB QUESTIONS

# CHAPTER 13: MULTITHREADING

WHY TO USE MULTITHREADING

CREATING Threads In Your C# Program

DELETING A Thread

LAB QUESTIONS

# CHAPTER 14: POLYMORPHISM

WHY USE POLYMORPHISM?

OVERRIDING FUNCTIONS

OVERLOADING CLASSES

ABSTRACT CLASSES

LAB QUESTIONS

# CHAPTER 15: ERROR HANDLING

USING THE VISUAL STUDIO DEBUGGER

THE TRY CATCH STATEMENT IN C#

LAB QUESTIONS

# FINAL WORDS

> "I would love to change the world, but they won't give me the source code”

Unknown Author

# Chapter 1
Introduction

Hello and welcome to your new programming language. This book is an introduction to programming using C#. We'll focus on breadth rather than depth. The goal is to be able to do something interesting as quickly as possible. We'll start out with fairly detailed explanations because it's important to have a thorough understanding of the basics, as we go on, we'll have to leave a lot of stuff out. Some of the topics could have an equally long guide guide themselves. You don't need to understand all aspects of everything you read; what you should retain is knowledge that a particular capability exists and what it is called so that you can look it up when you need it. This is what most programmers do.

The first few sections of the book are fairly self-contained with simple examples. You should certainly not read them without typing them into the interpreter; you'll get even more out of the tutorial if you experiment with the examples yourself.

The remainder of the tutorial is structured around building a program that does something interesting. This will allow us to touch on many aspects of programming that are necessary to write real world programs: reading and writing to disk; error handling; code organization into classes, modules, and packages; regular expressions; and user input. We'll also touch on some general principles in programming, such as clarity and efficiency.

Let's get started!

# Chapter 2
C# Programming Language

You might wonder why you should use C#. This chapter covers reasons why C# is a great language to learn and what it can do for you.

C# is a backend programming language. It processes the input and output for web and desktop applications. There are numerous languages to choose from, so you might wonder why you would choose C# over other programming languages. This chapter gives you some background on the C# language and what it's used for in the programming industry.

# Why Use C#

No developer is tied to any language. You can just use any language-based applications to complete an application. When you want to develop pure Windows-based applications, you'll need to learn one of the .NET framework languages, which include C# and VB.NET. When .NET was originally introduced, VB.NET was the most popular language. This is because old Classic ASP used the VB style to create dynamic webpages. C# has a C-style programming syntax, and it's very close to the Java language syntax. These two boosted C#'s popularity and now it's the preferred language among developers.

C#'s closeness to Java and C make it easier to learn than other languages. If you know any C-style language, you'll pick up on C# pretty easily. VB.NET is considered closer to human language, so it's a higher level language. The problem is that VB.NET is then slower to run because it is closer to human language. This is another reason why developers prefer C# over VB.NET—it processes code faster. The further away from machine language that you get over, the slower it becomes.

Another reason C# is a good language to use is that it's very easy to implement with other Microsoft solutions. You can implement other C# solutions by just adding them to your current solutionion. You can use Entity Framework with MSSQL with C# with little implementation and configuration required. If you are tasked with writing or adding to existing Visual Studio projects, C# is more easily integrated into a Microsoft environment.

You don't have to design much with C#, so if you prefer to work on strictly backend systems, you'll prefer C# over other languages. It's also the solution that backend coders use with automation within a Windows environment. If you decide to work with any Windows system, it will be useful to know C#.

# What is C# Used For?

There are several reasons you would want to use C#. C# lets you work with both desktop and web applications. Specifically, you use C# to work with Windows programs. To run C#, the server needs to run the .NET framework. The .NET framework is only compatible with Windows, so you need to run any C# application on a server or desktop running Windows.

C# is commonly used in web applications. Specifically, the C# language is used to process the dynamic, backend code. For instance, when a user sends information through a web form, the C# language processes it, stores it, and then sends a response. C# MVC still handles the front end that displays the information, and you implement HTML, CSS, and JavaScript for the front end. C# is also used with desktop applications, but you won't see many desktop applications as a primary software anymore. The programming world is turning to cloud applications, which is still beneficial for C# programmers. C# programmers can create APIs and backend code that deals with cloud-based applications.

C# APIs are also called WCF applications. These APIs let developers integrate external functions that work with internal applications. For instance, you can use the Facebook API to integrate into your applications. The same can be done with a C# API. The benefit of publishing an API is that it does not matter what language the third-party developer uses. They can use PHP, Java, JavaScript, and Python to work with your API. As long as the application works with either XML or JSON input or output, the third-party developer can work with your C# API.

C# is also used with database applications. It works with SQL Server to store and request data from a database server. C# can use Entity Framework with MSSQL so the developer can use LINQ queries and POCO classes to work with data. This means that you don't need to go back and forth with database-stored procedures. Instead, the developer can work directly with the database structures and data.

Finally, C# is used for Windows services. These are programs that work in the background of a computer, usually a server. They are used in automation to ensure certain processes happen automatically at a specific time of day.

# What Tools Do You Need?

With C#, you can't use any tool to create your programs. You need Visual Studio, which is freely available as a download from the Microsoft official website. You can buy the professional or enterprise version of the software, but it's not necessary as an individual. It’s especially necessary if you're just starting out as a student.
