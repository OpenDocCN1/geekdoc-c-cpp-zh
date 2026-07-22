![](Images/cover.jpg)

![](Images/cover.jpg)

## Object-oriented Programming with C++

**A. K. Sharma**Professor and DeanDepartment of Computer Science and EngineeringB. S. Anangpuria Institute of Technology and ManagementFaridabad, Haryana, India

![41625.png](Images/41625.png)

Chennai • Delhi

*Associate Editor—Acquisitions*: Neha Goomer

*Editor—Production*: M. Balakrishnan

**Copyright © 2014 Dorling Kindersley (India) Pvt. Ltd**

This book is sold subject to the condition that it shall not, by way of trade or otherwise, be lent, resold, hired out, or otherwise circulated without the publisher’s prior written consent in any form of binding or cover other than that in which it is published and without a similar condition including this condition being imposed on the subsequent purchaser and without limiting the rights under copyright reserved above, no part of this publication may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording or otherwise), without the prior written permission of both the copyright owner and the publisher of this book.

ISBN 9789332515833

eISBN 9789332540767

**First Impression**

Published by Dorling Kindersley (India) Pvt. Ltd, licensees of Pearson Education in South Asia.

Head Office: 7th Floor, Knowledge Boulevard, A-8(A), Sector 62, Noida 201 309, UP, India.

Registered Office: 11 Community Centre, Panchsheel Park, New Delhi 110 017, India.

*Compositor*: MAP Systems, Bengaluru.

*Printed in India.*

Dedicated to all the objects around me

## Contents

[Preface](#preface.xhtml)

[About the Author](#authors.xhtml)

[1\. INTRODUCTION TO C++](#chapter_01.xhtml)

[1.1 Introduction](#chapter_01.xhtml_ch1)

[1.2 Characters Used in C++](#chapter_01.xhtml_ch2)

[1.3 Basic Data Types](#chapter_01.xhtml_ch3)

*[1.3.1 Data Types Modifi ers](#chapter_01.xhtml_ch4)*

[1.4 C++ Tokens](#chapter_01.xhtml_ch5)

*[1.4.1 Identifi ers](#chapter_01.xhtml_ch6)*

*[1.4.2 Keywords](#chapter_01.xhtml_ch7)*

*[1.4.3 Constants](#chapter_01.xhtml_ch8)*

*[1.4.4 Variables](#chapter_01.xhtml_ch9)*

[1.5 Input–Output Statements](#chapter_01.xhtml_ch10)

[1.6 Structure of a C++ Program](#chapter_01.xhtml_ch11)

*[1.6.1 Comments](#chapter_01.xhtml_ch12)*

[1.7 Escape Sequence (Backslash Character Constants)](#chapter_01.xhtml_ch13)

[1.8 Operators and Expressions](#chapter_01.xhtml_ch14)

*[1.8.1 Arithmetic Operators](#chapter_01.xhtml_ch15)*

*[1.8.2 Relational and Logical Operators](#chapter_01.xhtml_ch16)*

*[1.8.3 Conditional Operator](#chapter_01.xhtml_ch17)*

*[1.8.4 Order of Evaluation of Expressions](#chapter_01.xhtml_ch18)*

*[1.8.5 Some Special Operators](#chapter_01.xhtml_ch19)*

[1.9 Flow of Control](#chapter_01.xhtml_ch20)

*[1.9.1 The Compound Statement](#chapter_01.xhtml_ch21)*

*[1.9.2 Selective Execution (Conditional Statements)](#chapter_01.xhtml_ch22)*

*[1.9.3 Repetitive Execution (Iterative Statements)](#chapter_01.xhtml_ch23)*

*[1.9.4 Nested Loops](#chapter_01.xhtml_ch24)*

[1.10 Arrays](#chapter_01.xhtml_ch25)

*[1.10.1 One-dimensional Arrays](#chapter_01.xhtml_ch26)*

*[1.10.2 Multi-dimensional Arrays](#chapter_01.xhtml_ch27)*

*[1.10.3 Array Initialization](#chapter_01.xhtml_ch28)*

[1.11 Structures](#chapter_01.xhtml_ch29)

*[1.11.1 Defi ning a Structure in ‘C++’](#chapter_01.xhtml_ch30)*

*[1.11.2 Arrays of Structures](#chapter_01.xhtml_ch31)*

*[](#chapter_01.xhtml_ch32)1.11.3 Initializing Structures*

*[1.11.4 Assignment of Complete Structures](#chapter_01.xhtml_ch33)*

*[1.11.5 Nested Structures](#chapter_01.xhtml_ch34)*

[1.12 Functions](#chapter_01.xhtml_ch35)

*[1.12.1 Function Prototypes](#chapter_01.xhtml_ch36)*

*[1.12.2 Calling a Function](#chapter_01.xhtml_ch37)*

*[1.12.3 Parameter Passing in Functions](#chapter_01.xhtml_ch38)*

*[1.12.4 Returning Values from Functions](#chapter_01.xhtml_ch39)*

[1.13 I/O Functions](#chapter_01.xhtml_ch40)

*[1.13.1 getchar( ) and putchar( ) Functions](#chapter_01.xhtml_ch41)*

*[1.13.2 getc( ) and putc( ) Functions](#chapter_01.xhtml_ch42)*

*[1.13.3 gets( ) and puts( ) Functions](#chapter_01.xhtml_ch43)*

[1.14 Strings](#chapter_01.xhtml_ch44)

[1.15 Summary](#chapter_01.xhtml_ch45)

*[Multiple Choice Questions](#chapter_01.xhtml_ch46)*

*[Answers](#chapter_01.xhtml_ch47)*

*[Exercises](#chapter_01.xhtml_ch48)*

*[Answers](#chapter_01.xhtml_ch49)*

[2\. POINTERS](#chapter_02.xhtml)

[2.1 Introduction](#chapter_02.xhtml_ch1)

*[2.1.1 The & Operator](#chapter_02.xhtml_ch2)*

*[2.1.2 The * Operator](#chapter_02.xhtml_ch3)*

[2.2 Pointer Variables](#chapter_02.xhtml_ch4)

*[2.2.1 Dangling Pointers](#chapter_02.xhtml_ch5)*

[2.3 Pointers and Arrays](#chapter_02.xhtml_ch6)

[2.4 Array of Pointers](#chapter_02.xhtml_ch7)

[2.5 Pointers and Structures](#chapter_02.xhtml_ch8)

[2.6 Dynamic Allocation](#chapter_02.xhtml_ch9)

*[2.6.1 Self Referential Structures](#chapter_02.xhtml_ch10)*

[2.7 Summary](#chapter_02.xhtml_ch11)

*[Multiple Choice Questions](#chapter_02.xhtml_ch12)*

*[Answers](#chapter_02.xhtml_ch13)*

*[Exercises](#chapter_02.xhtml_ch14)*

*[Answers](#chapter_02.xhtml_ch15)*

[3\. PROGRAMMING TECHNIQUES: A SURVEY](#chapter_03.xhtml)

[3.1 Introduction](#chapter_03.xhtml_ch1)

[3.2 Unstructured Programming](#chapter_03.xhtml_ch2)

[3.3 Structured Programming](#chapter_03.xhtml_ch3)

*[3.3.1 Procedural Programming](#chapter_03.xhtml_ch4)*

*[3.3.2 Modular Programming](#chapter_03.xhtml_ch5)*

[3.4 Drawbacks of Structured Programming](#chapter_03.xhtml_ch6)

[](#chapter_03.xhtml_ch7)3.5 Object-Oriented Programming

[3.6 Summary](#chapter_03.xhtml_ch8)

*[Multiple Choice Questions](#chapter_03.xhtml_ch9)*

*[Answers](#chapter_03.xhtml_ch10)*

*[Exercises](#chapter_03.xhtml_ch11)*

[4\. CLASSES AND OBJECTS](#chapter_04.xhtml)

[4.1 Introduction to Objects](#chapter_04.xhtml_ch1)

[4.2 Classes](#chapter_04.xhtml_ch2)

[4.3 Declaration of Classes in C++](#chapter_04.xhtml_ch3)

*[4.3.1 Abstraction and Encapsulation](#chapter_04.xhtml_ch4)*

*[4.3.2 Member Function Defi nition](#chapter_04.xhtml_ch5)*

[4.4 Creating Objects](#chapter_04.xhtml_ch6)

*[4.4.1 Calling Member Functions](#chapter_04.xhtml_ch7)*

[4.5 Array of Objects](#chapter_04.xhtml_ch8)

[4.6 Objects as Function Arguments](#chapter_04.xhtml_ch9)

[4.7 Scope Resolution Operator](#chapter_04.xhtml_ch10)

[4.8 Static Data Members](#chapter_04.xhtml_ch11)

[4.9 Properties of Classes and Objects](#chapter_04.xhtml_ch12)

[4.10 Summary](#chapter_04.xhtml_ch13)

*[Multiple Choice Questions](#chapter_04.xhtml_ch14)*

*[Answers](#chapter_04.xhtml_ch15)*

*[Exercises](#chapter_04.xhtml_ch16)*

[5\. MORE ON FUNCTIONS: ADVANCED CONCEPTS](#chapter_05.xhtml)

[5.1 Polymorphism](#chapter_05.xhtml_ch1)

[5.2 Function Overloading](#chapter_05.xhtml_ch2)

[5.3 Inline Functions](#chapter_05.xhtml_ch3)

[5.4 Friend Functions](#chapter_05.xhtml_ch4)

*[5.4.1 Member Functions of a Class as Friends of Another Class](#chapter_05.xhtml_ch5)*

*[5.4.2 Friend Function as a Bridge Between Two Classes](#chapter_05.xhtml_ch6)*

[5.5 Friend Classes](#chapter_05.xhtml_ch7)

[5.6 Recursion](#chapter_05.xhtml_ch8)

*[5.6.1 Types of Recursion](#chapter_05.xhtml_ch9)*

[5.7 Summary](#chapter_05.xhtml_ch10)

*[Multiple Choice Questions](#chapter_05.xhtml_ch11)*

*[Answers](#chapter_05.xhtml_ch12)*

*[Exercises](#chapter_05.xhtml_ch13)*

*[Answers](#chapter_05.xhtml_ch14)*

[](#chapter_06.xhtml)6\. CONSTRUCTORS AND DESTRUCTORS

[6.1 Constructors](#chapter_06.xhtml_ch1)

[6.2 Types of Constructors](#chapter_06.xhtml_ch2)

*[6.2.1 Default Constructor and User Defi ned Constructor](#chapter_06.xhtml_ch3)*

*[6.2.2 Parameterized Constructors](#chapter_06.xhtml_ch4)*

*[6.2.3 Copy Constructor](#chapter_06.xhtml_ch5)*

*[6.2.4 Constructors with Default Arguments](#chapter_06.xhtml_ch6)*

*[6.2.5 Rules for Constructor Defi nition and Usage](#chapter_06.xhtml_ch7)*

[6.3 Destructors](#chapter_06.xhtml_ch8)

[6.4 Summary](#chapter_06.xhtml_ch9)

*[Multiple Choice Questions](#chapter_06.xhtml_ch10)*

*[Answers](#chapter_06.xhtml_ch11)*

*[Exercises](#chapter_06.xhtml_ch12)*

[7\. INHERITANCE: EXTENDING CLASSES](#chapter_07.xhtml)

[7.1 Introduction to Code Reuse](#chapter_07.xhtml_ch1)

[7.2 Containership](#chapter_07.xhtml_ch2)

[7.3 Inheritance](#chapter_07.xhtml_ch3)

*[7.3.1 Visibility Modes](#chapter_07.xhtml_ch4)*

[7.4 Types of Inheritance](#chapter_07.xhtml_ch5)

*[7.4.1 Multilevel Inheritance](#chapter_07.xhtml_ch6)*

*[7.4.2 Multiple Inheritance](#chapter_07.xhtml_ch7)*

[7.5 Function Overriding](#chapter_07.xhtml_ch8)

*[7.5.1 Virtual Functions](#chapter_07.xhtml_ch9)*

[7.6 Role of Constructors and Destructors in Inheritance](#chapter_07.xhtml_ch10)

[7.7 Virtual Base Class](#chapter_07.xhtml_ch11)

[7.8 Summary](#chapter_07.xhtml_ch12)

*[Multiple Choice Questions](#chapter_07.xhtml_ch13)*

*[Answers](#chapter_07.xhtml_ch14)*

*[Exercises](#chapter_07.xhtml_ch15)*

[8\. TEMPLATES: CODE SHARING (GENERICITY)](#chapter_08.xhtml)

[8.1 Introduction to Code Sharing](#chapter_08.xhtml_ch1)

[8.2 Templates](#chapter_08.xhtml_ch2)

[8.3 Generic Classes](#chapter_08.xhtml_ch3)

[8.4 Templates with More than One Generic Parameter](#chapter_08.xhtml_ch4)

[8.5 Summary](#chapter_08.xhtml_ch5)

*[Multiple Choice Questions](#chapter_08.xhtml_ch6)*

*[Answers](#chapter_08.xhtml_ch7)*

*[Exercises](#chapter_08.xhtml_ch8)*

[](#chapter_09.xhtml)9\. OPERATOR OVERLOADING

[9.1 Introduction](#chapter_09.xhtml_ch1)

[9.2 Operator Overloading](#chapter_09.xhtml_ch2)

[9.3 Binary Operators](#chapter_09.xhtml_ch3)

*[9.3.1 Arithmetic Assignment Operators](#chapter_09.xhtml_ch4)*

[9.4 Unary Operators](#chapter_09.xhtml_ch5)

[9.5 Input/Output Operators](#chapter_09.xhtml_ch6)

[9.6 Rules for Operator Overloading](#chapter_09.xhtml_ch7)

[9.7 Summary](#chapter_09.xhtml_ch8)

*[Multiple Choice Questions](#chapter_09.xhtml_ch9)*

*[Answers](#chapter_09.xhtml_ch10)*

*[Exercises](#chapter_09.xhtml_ch11)*

[10\. FILE HANDLING IN C++](#chapter_10.xhtml)

[10.1 File Concepts](#chapter_10.xhtml_ch1)

[10.2 Files and Streams](#chapter_10.xhtml_ch2)

[10.3 Opening and Closing a File (Text Files)](#chapter_10.xhtml_ch3)

*[10.3.1 Function get( )](#chapter_10.xhtml_ch4)*

*[10.3.2 Function getline( )](#chapter_10.xhtml_ch5)*

*[10.3.3 Function put( )](#chapter_10.xhtml_ch6)*

[10.4 Opening the Files by Using Function Open( )](#chapter_10.xhtml_ch7)

[10.5 Reading and Writing Blocks and Objects (Binary Files)](#chapter_10.xhtml_ch8)

*[10.5.1 Storing Objects in Files](#chapter_10.xhtml_ch9)*

[10.6 Detecting End of File](#chapter_10.xhtml_ch10)

[10.7 Summary](#chapter_10.xhtml_ch11)

*[Multiple Choice Questions](#chapter_10.xhtml_ch12)*

*[Answers](#chapter_10.xhtml_ch13)*

*[Exercises](#chapter_10.xhtml_ch14)*

[11\. EXCEPTION HANDLING](#chapter_11.xhtml)

[11.1 Introduction](#chapter_11.xhtml_ch1)

[11.2 Traditional Error Handling](#chapter_11.xhtml_ch2)

[11.3 Exception Handling in C++](#chapter_11.xhtml_ch3)

*[11.3.1 Multiple Throw Statements and Multiple Catch Blocks](#chapter_11.xhtml_ch4)*

*[11.3.2 Throwing Objects](#chapter_11.xhtml_ch5)*

[11.4 Summary](#chapter_11.xhtml_ch6)

*[Multiple Choice Questions](#chapter_11.xhtml_ch7)*

*[Answers](#chapter_11.xhtml_ch8)*

*[Exercises](#chapter_11.xhtml_ch9)*

[](#chapter_12.xhtml)12\. INTRODUCTION TO UML

[12.1 Introduction to Uml](#chapter_12.xhtml_ch1)

[12.2 Class Diagrams (Static)](#chapter_12.xhtml_ch2)

*[12.2.1 Relationships Among Classes](#chapter_12.xhtml_ch3)*

[12.3 Use Case Diagrams (Static)](#chapter_12.xhtml_ch4)

[12.4 Behavioral Diagrams (Dynamic)](#chapter_12.xhtml_ch5)

*[12.4.1 Interaction Diagrams](#chapter_12.xhtml_ch6)*

*[12.4.2 State Chart Diagrams](#chapter_12.xhtml_ch7)*

*[12.4.3 Activity Diagrams](#chapter_12.xhtml_ch8)*

[12.5 Implementation Diagrams](#chapter_12.xhtml_ch9)

*[12.5.1 Component Diagram](#chapter_12.xhtml_ch10)*

*[12.5.2 Deployment Diagram](#chapter_12.xhtml_ch11)*

[12.6 Summary](#chapter_12.xhtml_ch12)

*[Multiple Choice Questions](#chapter_12.xhtml_ch13)*

*[Answers](#chapter_12.xhtml_ch14)*

*[Exercises](#chapter_12.xhtml_ch15)*

[13\. POLYMORPHISM: A REVIEW](#chapter_13.xhtml)

[13.1 Polymorphism](#chapter_13.xhtml_ch1)

[13.2 Taxonomy of Polymorphism](#chapter_13.xhtml_ch2)

*[13.2.1 Universal Polymorphism](#chapter_13.xhtml_ch3)*

*[13.2.2 Ad Hoc Polymorphism](#chapter_13.xhtml_ch4)*

*[Appendix](#appendix.xhtml)*

*[Index](#index.xhtml)*

## Preface

My quest for object-oriented programming (OOP) started at University of Roorkee in November 1989 when my guru Prof. J. P. Gupta asked me the question: “what is object-oriented programming?” I did not have a compelling answer at that time. However, I started looking into the available literature to find the answers. A critical look at the literature revealed that OOP was more of a philosophy than a programming paradigm. In fact, it is nearer to the oriental philosophy which states that the world around us is not absolute but relative to an individual’s capacity to perceive the world around him or her. In fact, whatever we perceive through our senses is nothing but an object.

When we look around, we find that we are surrounded by objects ...

## About the Author

![image](Images/author.png)

A. K. Sharma is currently Professor (CSE) and Dean (PG and Research) at B. S. Anangpuria Institute of Technology and Management. Earlier, he was Professor and Dean, Faculty of Engineering and Technology, YMCA University of Science and Technology, Faridabad.

A member of the board of studies and academic council of several renowned universities, Dr Sharma has guided more than twenty students in doctoral programs leading to their Ph.D. degrees. He has published more than 250 research papers in national and international journals of repute and made presentations in numerous academic conferences. He heads a group of researchers actively working on the design of Web crawlers.

## **1**

## **INTRODUCTION TO C++**

##### 1.1 INTRODUCTION

The ‘C’ programming language was created as a structured programming tool for writing large and complex system programs such as operating systems. No wonder that in 1973, Unix operating system was developed using ‘C’. The software developers liked ‘C’ because of its characteristics such as speed, compactness, and ability to harness the power of the hardware through low-level features.

Niklaus Wirth has defined that a program is composed of two components Algorithms and Data structures, as given below:

**Algorithms + Data Structures = Programs**

Thus, there can be two approaches towards the development of software, i.e. to develop programs either centered around *functions* or with an emphasis given to *data*. The ...

## 2

## POINTERS

##### 2.1 INTRODUCTION

Pointers are one of the most important features of C++. The beginners of C and C++ find pointers hard to understand and manipulate, though the treatment of pointers in C++ is comparatively simpler than in C. In an attempt to unveil the mystery behind this aspect, the basics of pointers that generally remain in background are being discussed in the following sections.

#### 2.1.1 The & Operator

When a variable *x* is declared in a program, a storage location in the main memory is made available by the compiler. For example, [Fig. 2.1](#chapter_02.xhtml_ch2fig1) shows the declaration of *x* as an integer variable and its storage location in the main memory.

![Figure 2.1](Images/ch02fig01.png)

**Figure 2.1** *The variable x and its equivalent representation in memory*

From [Fig. 2.1](#chapter_02.xhtml_ch2fig1), it may be observed that *x* is the name associated by the compiler to a location in the memory of the computer. Let us assume that, at the time of execution, the physical address of this memory location (called *x* ) is 2712\. Now, a point worth noting is that this memory location is viewed by the programmer as variable *x* and by the operating system as an address 2712. The address of the variable *x* can be obtained by ‘&’, an address of the operator. This operator when applied to a variable, gives the physical memory address of the variable. Thus, &*x* will provide the address 2712. Consider the following program segment:

![image](Images/pg60-1.png)

The output of the above program segment would be as shown below:

![image](Images/pg60-2.png)

The contents of variable *x* (memory location 2712) are shown in [Fig. 2.2](#chapter_02.xhtml_ch2fig2).

![Figure 2.2](Images/ch02fig02.png)

**Figure 2.2** *The contents of variable x*

It may be noted here that the value of address of *x* (i.e. 2712) is assumed, and the actual value is ‘*machine and execution*’ time dependent.

#### 2.1.2 The * Operator

The * is an indirection operator or value at address operator. In simple words, we can say that if the address of a variable is known, then the * operator provides the contents of the variable. Consider the following program segment:

![image](Images/pg60-3.png)

The output of the above program segment would be as shown below:

![image](Images/pg61-1.png)

Consider the following program:

![image](Images/pg61-2.png)

The output would be 50 because * and & operators complement each other; therefore the 50 is stored in the variable called *a*.

##### 2.2 POINTER VARIABLES

An address of a variable can be stored in a special variable called **pointer** variable. A pointer variable contains the address of another variable. Let us assume that *y* is such a variable. Now, the address of variable *x* can be assigned to *y* by the statement: *y* = &*x*. The effect of this statement is shown in [Fig. 2.3](#chapter_02.xhtml_ch2fig3).

![Figure 2.3](Images/ch02fig03.png)

**Figure 2.3** *The address of x is being stored in pointer variable* y

From [Fig. 2.3](#chapter_02.xhtml_ch2fig3), it is clear that *y* is the variable that contains the address (i.e. 2712) of another variable *x*, whereas, the address of *y* itself is 1232 (assumed value). In other words, we can say that *y* is a pointer to variable *x*. See [Fig. 2.4](#chapter_02.xhtml_ch2fig4).

![Figure 2.4](Images/ch02fig04.png)

**Figure 2.4** y *is a pointer to* x

A pointer variable *y* can be declared in C++ as shown below:

int **y;*

The above declaration means that *y* is a pointer to a variable of type int. Similarly, consider the following declaration:

![image](Images/pg62-1.png)

The above declaration means that *p* is a pointer to a variable of type char.

Consider the following program segment:

![image](Images/pg62-2.png)

The output of the above program segment would be as shown below. We have shown only the assumed addresses as per [Fig. 2.3](#chapter_02.xhtml_ch2fig3).

![image](Images/pg62-3.png)

Let us now, consider the following statements:

![image](Images/pg62-4.png)

The first statement declares val to be a variable of type float and initializes it by value 35.67\. The second statement declares pt to be pointer to a variable of type float. Please notice that pt can point to a variable of type float, but it is currently not pointing to any variable as shown in [Fig. 2.5](#chapter_02.xhtml_ch2fig5).

![Figure 2.5](Images/ch02fig05.png)

**Figure 2.5** *The pointer pt is not pointing to any variable*

The pointer pt can point to the variable val by assigning the address of val to pt as shown below.

pt = &val;

Once the above statement is executed, the pointer pt gets the address of val, and we can say that logically pt points to the variable val as shown in [Fig. 2.6](#chapter_02.xhtml_ch2fig6).

![Figure 2.6](Images/ch02fig06.png)

**Figure 2.6** *The pointer pt pointing to variable val*

However, one must keep in mind that the arrow is for illustration sake. Actually, the pointer pt contains the address of val. The address is an integer that is not a simple value but a reference to a location in the memory.

Examples of some valid pointer declarations are:

1.  int **p* ;
2.  char **i*, **k* ;
3.  float *pt;
4.  int **ptr;

The example (iv) means the ptr is a pointer to a location which itself is a pointer to a variable of type integer.

It may be noted here that a pointer can also be incremented to point to an immediately next location of its type. For example, if the contents of a pointer *p* of type integer are 5224, then the content of *p* ++ will be 5226 instead of 5225 (see [Fig. 2.7](#chapter_02.xhtml_ch2fig7)). The reason being an int is always of 2 bytes size and therefore stored in two memory locations as shown in [Fig. 2.7](#chapter_02.xhtml_ch2fig7). The amount of storage taken by the various types of data is tabulated in [Table 2.1](#chapter_02.xhtml_ch2tab1)

![Figure 2.7](Images/ch02fig07.png)

**Figure 2.7** *The variable of type int occupies two bytes*

**Table 2.1 Amount of Storage Taken by Data Types**

| Data Type | Amount of Storage |
| character | 1 byte |
| integer | 2 byte |
| Float | 4 byte |
| Long | 4 byte |
| Double | 8 byte |

Thus, a pointer of float type will point to an address of 4 bytes of locations, and therefore increment to this pointer will increment its contents by 4 locations. It may be further noted more than one pointer can point to the same location. Consider the following program segment:

![image](Images/pg64-1.png)

The following statement

*p*1=&  *x*;

makes the pointer *p*1 to point to variable *x* as shown in [Fig. 2.8](#chapter_02.xhtml_ch2fig8).

![Figure 2.8](Images/ch02fig08.png)

**Figure 2.8** *Pointer p1 points to variable x*

The following statement

*p*2 = *p*1

makes *p*2 to point to the same location, which is being pointed by *p*1 as shown in [Fig. 2.9](#chapter_02.xhtml_ch2fig9).

![Figure 2.9](Images/ch02fig09.png)

**Figure 2.9** *Pointer p1 and p2 pointing to x*

The contents of variable *x* are now reachable by both the pointers *p*1 and *p*2\. Thus, two or more entities can cooperatively share a single memory structure with the help of pointers. In fact, this technique can be used to provide efficient communication between different parts of a program.

The pointers can be used for a variety of purposes in a program. Some of them are given below.

1.  To pass address of variables from one function to another
2.  To return more than one value from a function to the calling function
3.  For the creation of linked structures such as linked lists and trees.

Consider the following program:

![image](Images/pg65-1.png)

The output would be 51 because the contents pointed by pointer *j* are being incremented before the display.

##### **Example 1**. *Write a program that reads from keyboard two variables* x *and* y *of type integer. It prints the exchanged contents of these variables with the help of pointers without altering the variables.*

*Solution:* We will use two pointers *p*1 and *p*2 for variables *x* and *y*. A third pointer *p*3 will be used as a temporary pointer for the exchange of pointers *p*1 and *p*2\. The scheme is shown in [Fig. 2.10](#chapter_02.xhtml_ch2fig10).

The program is given below:

![image](Images/pg65-2.png)

A sample output is given below:

![image](Images/pg66-1.png)

![Note](Images/note.png)**Note**: The output shows the exchanged values because of exchange of pointers (see [Fig. 2.10](#chapter_02.xhtml_ch2fig10)), whereas the contents of *x* and *y* have remained unaltered.

![Figure 2.10](Images/ch02fig10.png)

**Figure 2.10** *Exchange of contents of variables by exchanging pointers*

#### 2.2.1 Dangling Pointers

A dangling pointer is that pointer which has been created but does not point to any entity. Such an un-initialized pointer is dangerous in the sense that a dereference operation on it will result in an unpredictable operation or may result in a runtime error.

Consider the following code:

![image](Images/pg66-2.png)

![Figure 2.11](Images/ch02fig11.png)

**Figure 2.11** *The dangling pointer*

The first statement declares the pointer called ptr. At runtime it will be created as shown in [Fig. 2.11](#chapter_02.xhtml_ch2fig11). It may be noted that currently ptr is a dangling pointer. The second statement is trying to load a value (i.e. 50) to a location that is pointed by ptr. Obviously, this is a dangerous situation because the results will be unpredictable. The C++ compiler does not consider it as an error though some compilers may give a warning.

Therefore, if pointers are being used, the following steps must be followed:

*Step 1*. Declare the pointer.

*Step 2*. Allocate the variable or entity to which the pointer is to be pointed.

*Step 3*. Point the pointer to the entity.

Let us assume that it is desired that the pointer ptr should point to a variable val of type int. The correct code in that case would be as given below:

![image](Images/pg67-1.png)

![Figure 2.12](Images/ch02fig12.png)

**Figure 2.12** *The correct assignment*

The result of above program segment is shown in [Fig. 2.12](#chapter_02.xhtml_ch2fig12).

##### 2.3 POINTERS AND ARRAYS

Pointers and arrays are very closely related to each other. In C++, the name of an array is a pointer that contains the base address of the array. In fact, it is a pointer to the first element of the array. Consider the array declaration given below:

**int list[ ] = {20, 30, 35, 36, 39};**

This array will be stored in the contiguous locations of the main memory with starting address equal to 1001(assumed value), as shown in [Fig. 2.13](#chapter_02.xhtml_ch2fig13). Since the array list is of integer type, each element of this array occupies two bytes. The name of the array contains the starting address of the array, i.e. 1001

![Figure 2.13](Images/ch02fig13.png)

**Figure 2.13** *The contiguous storage allocation with starting address = 1001*

Consider the following program segment:

![image](Images/pg68-1.png)

Once the above program segment is executed, the output would be as shown below:

![image](Images/pg68-2.png)

We could have achieved the same output also by the following program segment also:

![image](Images/pg68-3.png)

Both the above given approaches are equivalent because of the following equivalence relations:

![image](Images/pg68-4.png)

The left-side approach is known as pointer method and right side as array indexing method. Let us now write a program that prints out a list by array indexing method.

![image](Images/pg68-5.png)

The output of this program is given below:

![image](Images/pg68-6.png)

The above program can also be written by pointer method as shown below:

![image](Images/pg69-1.png)

It may be noted in the above program that we have used the term * (list + *i* ) to print an *i* th element of the array. Let us analyze this term. Since the list designates the address of zeroth element of the array, we can access its value through value at address operator, i.e. *. The following terms are equivalent:

![image](Images/pg69-2.png)

Thus, we can refer to the *i* th element of array list by either of the following ways:

*(list + *i*) or *(*i* + list) or list [*i*]

So far, we have used the name of an array to get its base address and manipulate. However, there is a small difference between an ordinary pointer and the name of an array. The difference is that the array name is a **pointer constant** and its contents cannot be changed. Thus, the following operations on list are illegal because they try to change the contents of list, a pointer constant.

![image](Images/pg69-4.png)

Consider the following program:

![image](Images/pg69-5.png)

The output of above program would be:

*p*

*p*

From the above program, it looks as if the following declarations are equivalent as text [3] and *p*[3] behave in identical manner.

![image](Images/pg70-1.png)

It may be noted that the above declarations are not at all equivalent, though the behaviour may be same. In fact, the array declaration ‘text [6]’ asks from the complier for six locations of char type whereas the pointer declaration char **p* asks for a pointer that can point to any variable of following types:

1.  char—a character
2.  string—a string of characters
3.  Null—nowhere

Consider the following declarations:

![image](Images/pg70-2.png)

Since *p* is a pointer variable and has been assigned the starting address of array list, the following operations become perfectly valid on this pointer:

*p*+ +, *p*- - etc.

Let us now write a third version of the program that prints out the array. We will use pointer variable *p* in this program.

![image](Images/pg70-4.png)

The output of above program is given below:

![image](Images/pg70-5.png)

From our discussion on arrays, we know that the strings are stored and manipulated as array of characters, with last character being a null character (i.e. \0).

For example, the string ENGINEERING can be stored in an array (say text) as shown in [Fig. 2.14](#chapter_02.xhtml_ch2fig14).

![Figure 2.14](Images/ch02fig14.png)

**Figure 2.14** *The array called ‘Text’*

We can declare this string as a normal array by the following array declaration:

char text [11];

Consider the following declaration:

![image](Images/pg71-2.png)

In the above set of statements, we have declared a pointer *p* that can point to a character or string of characters. The next statement assigns the starting address of character string ‘text’ to the variable pointer *p* (see [Fig. 2.15](#chapter_02.xhtml_ch2fig15)).

![Figure 2.15](Images/ch02fig15.png)

**Figure 2.15** *Pointer p points to the array called ‘Text’*

Since text is a pointer constant, its contents cannot be changed. On the contrary, *p* is a pointer variable and can be manipulated like any other pointer as shown in the program given below.

![image](Images/pg71-3.png)

The output of the program is given below:

![image](Images/pg72-1.png)

Consider the following program:

![image](Images/pg72-2.png)

The output would be

6-6

6

##### **Example 2**. *What would be the output of the following?*

![image](Images/pg72-4.png)

*Solution:* The output would be *i*.

##### **Example 3**. *What would be the output of the following?*

![image](Images/pg72-5.png)

*Solution:* The output would be 15.

##### 2.4 ARRAY OF POINTERS

Like any other array, we can also have an array of pointers. Each element of such an array can point to a data item such as variable, array etc. For example, consider the declaration given below:

float **x* [20];

This declaration means that *x* is an array of 20 elements, and each element is a pointer to a variable of type float. Let us now construct an array of pointers to strings.

![image](Images/pg73-2.png)

The above declaration gives an array of pointers called item. Each element of item points to a string as shown in [Fig. 2.16](#chapter_02.xhtml_ch2fig16).

![Figure 2.16](Images/ch02fig16.png)

**Figure 2.16** *Array of pointers to strings*

The advantage of having an array of pointer to strings is that manipulation of strings becomes convenient. For example, the string-containing table can be copied into a pointer ptr without using strcpy( ) function by the following set of statements.

![image](Images/pg73-3.png)

It may be noted that once the above set of statements are executed, both the pointers item[1] and ptr will point to the same string table as shown in [Fig. 2.17](#chapter_02.xhtml_ch2fig17).

![Figure 2.17](Images/ch02fig17.png)

**Figure 2.17** *Effect of statement ptr = item[1]*

However, the changes made by the pointer ptr to the string table will definitely disturb the contents of the string pointed by the pointer item [1] and vice versa. Therefore, utmost care should be taken by the programmer while manipulating pointers pointing to same memory locations.

##### 2.5 POINTERS AND STRUCTURES

Similar to the other types of pointers, we can have a pointer to a structure, i.e. we can also point a pointer to a structure. A pointer to a structure variable can be declared by prefixing the variable name by a *. Consider the following declaration:

![image](Images/pg74-1.png)

Once the above declarations are made, we can assign the address of the structure variable abc to the structure pointer ptr by the following statement:

ptr = &abc;

Since ptr is a pointer to the structure variable abc, the members of the structure can also be accessed through a special operator called arrow operator i.e. → (minus sign followed by greater than sign). For example, the members *a* and *y* of the structure variable abc pointed by ptr can be assigned values 30 and 50.9 respectively by the following statement:

![image](Images/pg74-3.png)

The arrow operator ‘→’ is also known as a **pointer-to-member** operator.

##### **Example 4**. *Write a program that defines a structure called item for the record structure given below. It reads the data of the record through dot operator and prints the record by arrow operator. Use suitable data types for the members of the structure Item.*

![image](Images/pg74-4.png)

*Solution:* We will use a pointer ptr to point to the structure called Item. The required program is given below.

![image](Images/pg74-5.png)

From the above program, we can see that the members of a static structure can be accessed by both dot and arrow operators. However, dot operator is used for simple variable whereas the arrow operator for pointer variables.

##### **Example 5**. *What is the output of the following program?*

![image](Images/pg75-1.png)

*Solution:* From the above program, it can be observed that ptr is a pointer to an array of structures called polygon. The statement ptr ++ moves the pointer from the zeroth location (i.e. {1, 2}) to first location (i.e. {1, 4}). Now, the statement *x* ++ has incremented the field *x* of the structure by one (i.e. 1 has incremented to 2).

The output would be 2.

##### 2.6 DYNAMIC ALLOCATION

We know that in a program when a variable *x* is declared, a storage location is made available to the program as shown below.

![Figure 2.18](Images/ch02fig18.png)

**Figure 2.18** *Memory allocation to variable x*

This memory location remains available, even if it is not needed, to the program as long as the program is being executed ([Fig. 2.18](#chapter_02.xhtml_ch02fig18)). Therefore, the variable *x* is known as a static variable. Dynamic variables, on the other hand, can be allocated from or returned to the system according to the needs of a running program. However, a dynamic variable does not have a name and can be referenced only through a pointer.

Consider the declaration given below.

![Figure 2.19](Images/ch02fig19.png)

**Figure 2.19** *The dangling pointer p*

The above declaration gives us a dangling pointer *p* that points to nowhere (see [Fig. 2.19](#chapter_02.xhtml_ch2fig19)). Now, we can connect this dangling pointer either to a static variable or to a dynamic variable. In our previous discussion on pointers, we have always used pointers with static variables. Let us now see how the pointer can be connected to a dynamic variable.

In C++, dynamic memory can be allocated by an operator called ‘new’. The format of dynamic allocation is given below.

<pointer> = **new** <varType>

where <**pointer**> is a pointer to a variable of type varType

![image](Images/pg76-1.png)

Consider the following declaration

![image](Images/pg76-2.png)

The above set of statements are executed in the following manner:

1.  The pointer *p* is created. It is dangling, i.e. not connected anywhere (see [Fig. 2.20](#chapter_02.xhtml_ch2fig20)(a))
2.  A dynamic variable of type integer is taken through new operator and the dangling pointer *p* is connected to the variable (see [Fig. 2.20](#chapter_02.xhtml_ch2fig20)(b))

![Figure 2.20](Images/ch02fig20.png)

**Figure 2.20** *The effect of new operator*

It may noted from [Fig. 2.20](#chapter_02.xhtml_ch2fig20)(b) that a dynamic variable is anonymous in the sense that it has no name, and therefore it can be referenced only through the pointer p. For example, a value (say 50) can be assigned to the dynamic variable by the following statement:

**p* = 50;

The above statement means that it is desired to store a value 50 in a memory location pointed to by the pointer *p*. The effect of this statement is shown in [Fig. 2.21](#chapter_02.xhtml_ch2fig21).

![Figure 2.21](Images/ch02fig21.png)

**Figure 2.21** *The effect of assignment of * p = 50*

It may observed that *p* is simply a pointer or an address and **p* gives the access to the memory location or the variable where it is pointing to. It is very important to learn the difference between the pointer and its associated dynamic variable. Let us consider the following program segment.

![image](Images/pg77-2.png)

The outcome of the above program segment would be as shown in [Fig. 2.22](#chapter_02.xhtml_ch2fig22).

![Figure 2.22](Images/ch02fig22.png)

**Figure 2.22** *Value assignment through pointers*

Let us now see the effect of the following assignment statement on the memory allocated to the pointers Aptr and Bptr.

Aptr = Bptr;

The above assignment makes Aptr to point to the same location or variable, which is already being pointed by Bptr as shown in [Fig. 2.23](#chapter_02.xhtml_ch2fig23). Thus, both Aptr and Bptr are now pointing to the same memory location.

![Figure 2.23](Images/ch02fig23.png)

**Figure 2.23** *Both pointers pointing to the same location*

A close observation would reveal that the dynamic variable containing value 15 is now lost in the sense that it is neither available to Aptr anymore and nor it is available to the system. The reason being that the system gave it to the pointer Aptr and now Aptr is pointing to some other location. This dynamic variable being anonymous (i.e. without name) is no more accessible. Even if we want to reverse the process, we cannot simply do it. This phenomenon of losing dynamic variables is known as **memory bleeding**. Thus, utmost care should be taken while manipulating the dynamic variables. It is better to return a dynamic variable whenever it is not required in the program.

A dynamic variable can be returned to the system by function called delete. The general form of usage of this operator is given below.

delete <pointer>;

where **delete**: is a reserved word

<**pointer**>: is the pointer to the dynamic variable to be returned to the system

Let us consider pointers shown in [Fig. 2.23](#chapter_02.xhtml_ch2fig23). If it is desired to return the dynamic variable pointed by pointer Bptr, we can do so by the following statement:

delete Bptr;

Once the above statement is executed, the dynamic variable is returned back to the system, and we are left with two dangling pointers Bptr and Aptr as shown in [Fig. 2.24](#chapter_02.xhtml_ch2fig24). The reason for this is obvious because both were pointing to the same location. However, the dynamic variable containing value 15 is anonymous and not available anymore and hence a total waste of memory.

![Figure 2.24](Images/ch02fig24.png)

**Figure 2.24** *The two dangling pointers and a lost memory variable*

##### **Example 6**. *Write a program that dynamically allocates an integer. It initializes the integer with a value, increments it and prints the incremented value.*

*Solution:* The required program is given below:

![image](Images/pg79-1.png)

A sample output is given below:

![image](Images/pg79-2.png)

##### **Example 7**. *Write a program that dynamically allocates a structure whose structure diagram is given below. It reads the various members of the structure and prints them.*

![image](Images/pg79-3.png)

*Solution:* We will use the following steps to write the required program

1.  Declare a structure called student.
2.  Declare a pointer ptr to the structure student.
3.  Ask for dynamic memory of type student pointed by the pointer ptr.
4.  Read the data of the various elements using arrow operator.
5.  Print the data.
6.  Return the dynamic memory pointed by ptr.

The required program is given below.

![image](Images/pg79-4.png)

A sample output is given below:

![image](Images/pg80-1.png)

An array can also be dynamically allocated as demonstrated in the following example program.

##### **Example 8**. *Write a program that dynamically allocates an array of integers. A list of integers are read from the keyboard and stored in the array. The program determines the smallest in the list and prints its location in the list.*

*Solution:* The solution to this problem is trivial and the required program is given below.

![image](Images/pg80-2.png)

A sample output is given below:

![image](Images/pg81-1.png)

From the above example, it can be observed that the size of a dynamically allocated array can be specified even at the run time and the required amount of memory is allocated. This is in sharp contrast to static arrays for whom the size has to be declared at the compile time.

#### 2.6.1 Self Referential Structures

When a member of a structure is declared as a pointer to the structure itself, then the structure is called as **self referential structure**. Consider the following declaration.

![image](Images/pg82-1.png)

The structure chain consists of two members—val and *p*. The member val is a variable of type int, whereas the member *p* is a pointer to a structure of type chain. Thus, the structure chain has a member that can point to a structure of type chain or may be itself. This type of self referencing structure can be viewed as shown in [Fig. 2.25](#chapter_02.xhtml_ch2fig25).

![Figure 2.25](Images/ch02fig25.png)

**Figure 2.25** *Self referential structure chain*

Since pointer *p* can point to a structure variable of type chain, we can connect two such structure variables A and B to obtain a linked structure as shown in [Fig. 2.26](#chapter_02.xhtml_ch2fig26).

![Figure 2.26](Images/ch02fig26.png)

**Figure 2.26** *Linked structure*

The linked structure given in [Fig. 2.26](#chapter_02.xhtml_ch2fig26) can be obtained by the following steps:

1.  Declare structure chain.
2.  Declare variables A and B of type chain
3.  Assign the address of structure B to member p of structure A.

These above steps have been coded in the program segment given below.

![image](Images/pg82-2.png)

From [Fig. 2.26](#chapter_02.xhtml_ch2fig26) and the above program segment, we observe that the pointer p of structure variable B is dangling, i.e. it is pointing to nowhere. Such pointer can be assigned to NULL, a constant indicating that there is no valid address in this pointer. The following statement will do the desired operation:

*B* . *p* =NULL;

The data elements in this linked structure can be assigned by the following statements:

![image](Images/pg83-2.png)

The linked structure now looks like as shown in [Fig. 2.27](#chapter_02.xhtml_ch2fig27).

![Figure 2.27](Images/ch02fig27.png)

**Figure 2.27** *Value assignment to data elements*

We can see that the members of structure *B* can be reached to by two methods:

1.  From its variable name *B* through dot operator.
2.  From the pointer *p* of variable *A* because it is also pointing to the structure *B*. However, in this case, the arrow operator is needed.

Consider the statements given below:

![image](Images/pg83-3.png)

Once the above statements are executed, the output would be:

![image](Images/pg83-4.png)

The linked structures have great potential and can be used in numerous programming situations such as lists, trees etc.

##### **Example 9**. *Write a program that uses self referential structures to create a linked list of dynamic nodes of following structure. While creating the linked list, the student data is read. The list is also travelled to print the data.*

![image](Images/pg83-5.png)

*Solution:* We will use the following self referential structure for the purpose of creating a node of the linked list.

![image](Images/pg83-6.png)

The required linked list would be created by using three pointers ([Fig. 2.28](#chapter_02.xhtml_ch02fig28)). First far and back. The following algorithm would be employed to create the list.

Steps:

1.  Take a new node in pointer called first.
2.  Read first→ name and first →roll.
3.  Point back pointer to the same node being pointed by first, i.e. back =first.
4.  Bring a new node in the pointer called far.
5.  Read far→name and far→roll.
6.  Connect next of back to for, i.e. back→next =far.
7.  Take back to far, i.e. back = far.
8.  Repeat steps 4 to 7 till whole of the list is constructed.
9.  Point next of far to NULL, i.e. far→ next=NULL.
10.  Stop.

![Figure 2.28](Images/ch02fig28.png)

**Figure 2.28** *Creation of a linked list*

The required program is given below:

![image](Images/pg85-1.png)

##### **Example 10**. *Modify the program developed in [Example 9](#chapter_02.xhtml_ch2ex9) such that:*

1.  *Assume that the number of students in the list is not known.*
2.  *The list of students is split into the two sublists pointed by two pointers: front_half and back_half. The front_half points to the front half of the list and the back_half to the back half. If the number of students is odd, the extra student should go in the front list.*

*Solution:* The list of students would be created in the same fashion as done in Problem 1\. The following steps would be followed to split the list in the desired manner.

1.  Travel the list to count the number of students.
2.  Compute the middle of the list.
3.  Point the pointer called front_half to first and travel the list again starting from the first and reach to the middle.
4.  Point back-half to the node that succeeds the middle of the list.
5.  Attach NULL to the next pointer of the middle node.
6.  Print the two lists, i.e. pointed by front-half and back-half.

The required program is given below:

![image](Images/pg86-1.png)

##### **Example 11**. *Give the output of the following program:*

![image](Images/pg88-1.png)

*Solution*: The output would be

![image](Images/pg88-2.png)

##### 2.7 SUMMARY

A pointer is a variable that can only store the address of another variable. If a programmer assigns a new pointer, already poing to a new dynamic variable, the earlier dynamic variable is lost. This is also known as memory bleeding. Pointers always contain integers because a pointer can only contain an address, an integer quantity. A pointer can also be incremented to point to an immediately next location of its type. An un-initialized pointer is a dangling pointer that may contain any erroneous address. A NULL pointer does not point to any address location.

##### ![question](Images/question.png)MULTIPLE CHOICE QUESTIONS

1.  What happens to the dynamic variable if the pointer pointing to it is deleted?
    1.  It is lost
    2.  It is returned to system
    3.  It can be pointed by a new pointer
    4.  None of these
2.  Are the expressions (**p* )++ and ++**p* equivalent?
    1.  Yes
    2.  No
    3.  Cannot be compared
    4.  None of these
3.  What does the term ***j* means?
    1.  It is double pointer
    2.  *j* points to two addresses
    3.  *j* is a pointer to a pointer
    4.  None of these
4.  The address of a variable can be obtained by
    1.  New operator
    2.  * operator
    3.  = Operator
    4.  & operator
5.  The content at address is the
    1.  * operator
    2.  & operator
    3.  = operator
    4.  New operator
6.  A pointer contains the
    1.  Name of a variable
    2.  Type of a variable
    3.  Size of a variable
    4.  Address of a variable
7.  The increment of a pointer pointing to a float variable will increment its contents by
    1.  1 location
    2.  2 locations
    3.  4 locations
    4.  8 locations
8.  A dangling pointer is:
    1.  Un-instantiated pointer
    2.  Un-initialized pointer
    3.  Points to NULL
    4.  Un-defined pointer
9.  The name of an array is a
    1.  Constant pointer
    2.  Pointer variable
    3.  Pointer to a pointer
    4.  None of these
10.  A dynamic variable is a
    1.  Anonymous variable
    2.  Is a lost variable
    3.  Is a deleted variable
    4.  A NULL entity

##### ANSWERS

1.  b
2.  a
3.  c
4.  d
5.  a
6.  d
7.  c
8.  b
9.  a
10.  a

##### ![Exercise](Images/exe.png)EXERCISES

1.  Explain ‘&’ and ‘*’ operators in detail with suitable examples.
2.  Find the errors in the following program segments
    1.  ![image](Images/pg90-1.png)

    2.  ![image](Images/pg90-2.png)

3.  1.  What will be the output of the following programs:

        ![image](Images/pg90-3.png)

    2.  ![image](Images/pg90-4.png)

4.  What will be the output of the following program:

    ![image](Images/pg90-5.png)

5.  Find the errors in the following program segment:

    ![image](Images/pg90-6.png)

6.  What will be the output of the following program segment?

    ![image](Images/pg91-1.png)

7.  What will be the output of the following program?

    ![image](Images/pg91-2.png)

8.  What will be the output of the following program?

    ![image](Images/pg91-3.png)

9.  What would be the output of the following program?

    ![image](Images/pg92-1.png)

10.  What would be the output of the following program?

    ![image](Images/pg92-2.png)

11.  What would be the output of the following program?

    ![image](Images/pg92-3.png)

12.  Explain how new and delete operators manage memory allocation and deallocation.
13.  Write a program that creates a linked list of dynamic nodes consisteing of N nodes. The structure of an individual node is given below![image](Images/pg93-1.png)

##### ANSWERS

**4.** 5 5 10 30 120

**6.** *y x z*

**7.** 35.2 37.2 35.42 36.29

**8.** RETUPMOC

**9.** b

**10.** 50

**11.** 51

## 3

## PROGRAMMING TECHNIQUES: A SURVEY

##### 3.1 INTRODUCTION

FORTRAN, a computer language, was developed in mid-1950s. Nowadays, there are hundreds of programming languages available in the market. However, only a small number of them are popular among the programmers. For example, FORTRAN, BASIC, COBOL, Pascal, ‘C’, ‘C++’, PROLOG, JAVA, etc. are very popular computer languages.

Since a programming language is responsible for human-system communication, it consists of symbols, characters, and grammar rules which allow programmers to communicate with computers. As discussed earlier in [Chapter 1](#chapter_01.xhtml), a programming language can be defined as “a language used for expressing a set of computer instructions”. The set of instructions is called a program.

In fact, ...

## 4

## CLASSES AND OBJECTS

##### 4.1 INTRODUCTION TO OBJECTS

We perceive the world around us through our senses. The senses recognize objects present around us. For instance, *visible objects* like human beings, buildings, cars, soil, earth, water, cloud, etc. are all perceived by eyes. The *non-visible* objects like air, sound, and smell are perceived through touch, ears, and nose respectively. *Distant or abstract* objects are generally perceived through spoken words of an expert. For instance, the structure of an atom or existence of BOSON, the God particle, can only be perceived through their description by experts. Thus, the world around us is composed of nothing but objects of varying descriptions as shown in [Fig. 4.1](#chapter_04.xhtml_ch4fig1).

![Figure 4.1](Images/ch04fig01.png)

**Figure 4.1** *Some of the objects present around us*

An object can be precisely defined as: *an entity around us, perceivable through our senses.* If we look around, we find that we are surrounded by several objects (Fig. 4.1). For example in a University, students, professors, desks, fans, pens, writing pads, computers, etc. are all examples of objects.

Now, a closer look at various objects around us reveals that there are many types of objects as described below:

1.  *Objects that operate independently*. Examples: toys, photocopying machines, cameras, etc.
2.  *Objects that work in associations with each other*. Examples: computer–mouse, company–employee, car–driver, etc.
3.  *Objects that frequently interact with each other*. Example: telephones, fax machines, nodes of computer networks, etc.
4.  *Objects that are contained in other objects*. Example: ALU contained in a CPU, engine contained in a car, speaker contained in a phone, etc.

**An object has following three characteristics:**

1.  *Identity*: it is the name associated with an object. It helps in identifying the object, i.e. what we call the object as? For example, cup is the name of the object that is used to store, serve and drink hot beverages such as tea or coffee.
2.  *States*: an object can be in many states, for example, a cup, can be in the following states:
    1.  Full
    2.  Empty
    3.  Cold/hot
    4.  Broken
3.  *Behaviours*: what the object does or what is it capable of doing? For example, a cup can be filled, drunk from, washed, broken, etc. Similarly, a person can sit, stand, sleep, walk, talk, etc.

Consider the clay pitcher given in [Fig. 4.2](#chapter_04.xhtml_ch4fig2).

![Figure 4.2](Images/ch04fig02.png)

**Figure 4.2** *A clay pitcher*

It has the following characteristics:

1.  Identity: pitcher
2.  States:
    1.  Upright/upside down
    2.  Full/empty
    3.  Broken
    4.  Material – clay
    5.  Colour – brown
3.  Behaviours:
    1.  Can be filled
    2.  Can be emptied
    3.  Can be transported
    4.  Can be broken

In normal programming, when we write a program about (say) pitcher. The states are represented by variables and the behaviours as functions. The main() function sends the variables to various functions to model the overall functionality or behaviour of the pitcher. Thus, by nature, we first break the pitcher into variables and functions (i.e. pieces) then we try to glue the pieces through function calls to model its behaviour as shown in [Fig. 4.3](#chapter_04.xhtml_ch4fig3).

![Figure 4.3](Images/ch04fig03.png)

**Figure 4.3** *Normal programming*

Now the problem is that in a very large program, when we have large number of broken objects at hand then it becomes difficult for a programmer to keep track of the history of all the variables which are time and again passed to hundreds of functions and the results received from them. As the size and complexity of a program increases, the function and module management becomes equally difficult for the programmer. Therefore, the programming becomes cumbersome and difficult and only few hardcore programmers succeed.

However, *in real life we don’t break the pitcher or for that matter we don’t break any object at all*. The objects interact with each other without losing their characteristics (see [Fig. 3.7](#chapter_03.xhtml_ch3fig7)). Therefore, their management is quite easy and comfortable in real life.

Now the question is – can we create a software object that doesn’t lose its characteristics while being maneuvered in a program. Yes the answer is Object Oriented Programming (OOP) wherein we can define and create software object which behave like real life objects. Before we delve more into OOP, let us first understand another concept called ‘class’ as discussed in following section.

##### 4.2 CLASSES

Human has a very strong ability to categorize objects. When we see an object we immediately identify it to be belonging to a particular group or category. Consider the objects given in [Fig. 4.4](#chapter_04.xhtml_ch4fig4).

![Figure 4.4](Images/ch04fig04.png)

**Figure 4.4** *Collection of objects*

The collection of objects shown in [Fig. 4.4](#chapter_04.xhtml_ch4fig4) can be easily identified to be belonging to the category called cups. But the question is how we can say that these objects belong to a group or set called cups? The simple answer is that all these objects have common characteristics belonging to the category called cups. In OOP, a category is called a **class**.

In fact, the objects around us can be categorized into classes. For instance, we can easily locate a class of “furniture”, representing the objects such as: chairs, tables, desks, etc. In OOP terminology, we can say that a chair is an instance of the class furniture. Similarly, a dining table is also an instance of the class furniture and so on. If we consider book as a class then Ramayana, Gita, Jungle book are also instances of the class book. Thus, it can be said that *an object is an instance of a class*.

![Note](Images/note.png)**Note**: The objects belonging to a class may have different states but their behaviours remain the same. For instances, the cups given in [Fig. 4.4](#chapter_04.xhtml_ch4fig4) differ from each other in shape but the behaviours such as ‘*can be filled*’ or ‘*can be carried*’ remain the same for all instances of cups.

The precise definition of class is: “*A class defines common states and behaviours of a group of objects*”. Pictorially a class is represented as shown in [Fig. 4.5](#chapter_04.xhtml_ch4fig5).

![Figure 4.5](Images/ch04fig05.png)

**Figure 4.5** *Pictorial representation of a class*

The class that models a pitcher is given in [Fig. 4.6](#chapter_04.xhtml_ch4fig6).

![Figure 4.6](Images/ch04fig06.png)

**Figure 4.6** *Pitcher class*

In fact in OOP, we develop a program using the concept similar to building a system from its basic components. For a given problem, the following steps are followed:

1.  Identify the objects that comprise the problem.
2.  Categorize the objects into classes.
3.  Establish the relationship between the classes.
4.  Create instances of objects as per the requirement.
5.  Manage the objects to solve the problem.

##### 4.3 DECLARATION OF CLASSES IN C++

From the above discussion it is evident that the classes are central to OOP and a class can be used to create objects of its type. In C++, a class can be defined by the keyword “class”. The format of class declaration is given below:

![pg110-1.png](Images/pg110-1.png)

where *class* is a keyword; *<name>* is the user defined name of the class. It is a C++ identifier. *Private* is a keyword; *public* is a keyword.

It may be observed that a class declaration is similar to a structure declaration. Therefore, everything related to structure applies to classes. However, there is a difference in the sense that a structure is open and accessible to all whereas the access to members of the class is rather restricted. The class has clearly two sections: *private* and *public*. There is also a third special section available in a class. This section called *protected* and is discussed later in this book.

*Private members*: the members declared in private section are not accessible outside the class. Therefore, the most important members that need to be secured are placed in private section. The states (i.e. variables) are always made private. The reason being that the *internal state of an object should only be changed by an internal behaviour or function and not by outside stimuli*. For example, the temperature of human body remains constant irrespective of climatic conditions being summer or winter. However, an infection in the body may give rise to high body temperature. This feature of hiding states and data structures is called *data or information hiding*.

Similarly, the behaviours (i.e. the functions) which implement the business logic are also hidden from outside by making them private members. The *set* functions which can modify a state of the object are also made private. This feature of hiding implementation or set functions is also called as *implementation hiding*.

*Public members*: the functions that need to interact with outside world are made public. These functions interact with the outside world for the following purposes:

1.  *Taking input from users or other objects*. For example, the function that reads data from a user (say read_data()) needs to be made public.
2.  *Providing information about states of the object to users*. These functions are also called as *get* functions. For example, the function that informs about the grade of a student (say get_grade()) has to made public.
3.  *Providing services offered by the object to users or other objects*. For instance the push() and pop() functions of a stack object are made public.

It may be noted that the public functions act as interface to the outside world. In other words we can say that the important data, information, and implementation are hidden in private section behind a public interface as shown in [Fig. 4.7](#chapter_04.xhtml_ch4fig7).

![Figure 4.7](Images/ch04fig07.png)

**Figure. 4.7** *Data and implementation hiding behind public interface*

#### 4.3.1 Abstraction and Encapsulation

From [Figure 4.7](#chapter_04.xhtml_ch04fig07), the following points are observed:

1.  Only public interface is visible.
2.  The data, information, and implementation are hidden.

The visible part which provides only the bare minimum details about the object is called *abstraction*. The data, information and implementation are hidden. In other words, we can say that data, information and implementation have been placed in a capsule and the activity is called as *encapsulation*. An example of abstraction and encapsulation is given in [Fig. 4.8](#chapter_04.xhtml_ch4fig8).

![Figure 4.8](Images/ch04fig08.png)

**Figure 4.8** *Abstraction and encapsulation*

In a human head, there are many components like arteries, veins, muscles, eyes, ears, nose, mouth, cheek bones, retina, iris, brain, etc. But most of these have been encapsulated. Only the necessary components that are needed to interact with others have been abstracted as interface (see [Fig. 4.8](#chapter_04.xhtml_ch4fig8)).

By default, a class contains private members, i.e. all states and behaviours are private and not accessible to outsiders. Thus, the class encapsulates the data, information, and the implementation. When a user, by design, declares some members as public then those members become the interface or abstraction. Thus, the unnecessary details are ignored. The terms abstraction and encapsulation can be precisely defined as:

*Abstraction*: the activity of separating essential members of a class in the form of public interface is known as abstraction. It provides a simple view of the object so that the user can easily use the object.

*Encapsulation*: the activity of hiding data and implementation within a class as a unit is called as encapsulation. It creates a separation between the interface and the implementation thereby reducing the dependency between the components of the system.

In fact the abstraction has to be good so that the object can be used with ease without going into the details of the implementation. In fact it separates the behaviour of the object from its implementation. For example, in a camera there are 2–3 buttons and an eye-piece to interact with. Similarly, a house encapsulates many things but offers doors and windows as abstraction.

#### 4.3.2 Member Function Definition

The member functions can be defined inside as well as outside the class declaration. If a member function is very small then it can be defined inside the class itself. Such function definitions are considered by default to be inline. A discussion on inline functions is given later in this book. Let us consider the following class declaration:

![pg112-1.png](Images/pg112-1.png)

In this class two public functions readvar ( ) and dispvar ( ) have been defined. It may be noted that the actual code for the function is written inside the class definition itself. On the contrary, if a member function is large then it should be defined outside the class declaration. The prototypes of such functions, however, must be provided in the class definition. For example, the above defined class can be rewritten as given below:

![pg113-1.png](Images/pg113-1.png)

The operator ‘::’ is known as *scope resolution* operator. This is used to associate member functions to their corresponding class. For example, in the above function declarations, it conveys to the compiler that the functions readvar( ) and dispvar( ) belong to the class called test. The format of a member function declaration is given below:

![pg113-2.png](Images/pg113-2.png)

where type: is the data type of value to be returned;

class_name: the name of the class to which the function belongs;

function_name: the name of the function being declared;

parameter list: list of formal arguments.

From the above discussion, it is clear that a class combines data and functions into a single programming unit.

##### **Example 1**. *Define a class called student which models the following states and behaviours of a student:*

***States***

*Name*

*Roll*

*Marks*

*Grade*

***Behaviours***

*Read_data()*

*Display_grade()*

*Compute_grade()*

*Compute the grade as per the following rules:*

![pg114-1.png](Images/pg114-1.png)

*Solution*: We would model the states as variables and place them in private section for the purpose of data hiding. The behaviours read_data() and display_grade() would be modeled as functions and placed in public section as these functions are needed by the user to interact with the student object. Since the compute_grade() is an **implementation function**, it would be placed in private section from implementation hiding point of view. The required class is given below:

![pg114-2.png](Images/pg114-2.png)

##### 4.4 CREATING OBJECTS

An object is an instance of a class and it can be created of its class type. The syntax for defining an object is given below:

**<class_name>       <object_name>;**

where <class_name> is the name of the class and <object_name> is the name of the object being defined.

For example, we can create an object **studObj** of class **student** by the following declaration :

**student       studObj;**

The above declaration says that *studObj* is an object of class student.

In some situations, especially while sorting of objects, it is required that one object may be copied to another object. C++ allows assignment of objects of same type. It copies the source object bit-wise to the destined object. The concept is illustrated through the statements given below:

![pg115-3.png](Images/pg115-3.png)

#### 4.4.1 Calling Member Functions

Once an object has been created, its member functions (public) can be called in the program with the help of a dot operator, i.e. the object name is connected to the function name with a dot. For example, if we desire to call read_data( ) function of object ‘studOb’ then the following statement can be used.

**studOb.read_data();**

The above statement says that a function read_data() of object studOb is being called / invoked.

##### **Example 2**. *Use the class student defined in [Example 1](#chapter_04.xhtml_ch4ex1). Write a menu driven program that tests the class student for following services:*

1.  *Read the data of a student.*
2.  *Display the grade of a student.*

*Solution*: We would use a do–while loop to display a menu for asking the choice from the user. The required program is given below:

![page116-2.png](Images/page116-2.png)

![page117-1.png](Images/page117-1.png)

##### **Example 3**. *Define a class called employee with the following specifications*:

***States***

*name*

*BP: basic pay*,

*DA: dearness allowance*

*HRA: house rent allowance*

*salary*

***Behaviours***

*computeSal(): computes the salary*

*readData (): accepts the data values*

*dispSal(): prints the data on the screen.*

*The salary is computed by the following formula:*

*Salary = BP + DA + HRA*

*where DA and HRA are 65% and 20% of the BP, respectively.*

*Write a program that reads the name and BP of the employee and prints the salary.*

*Solution*: We would model the states as variables and place them in private section for the purpose of data hiding. The behaviours readData() and dispSal() would be modeled as functions and placed in public section as these functions are needed by the user to interact with the employee object. Since the computeSal() is an implementation function, it would be placed in private section from implementation hiding point of view.

The required class with a complete program is given below:

![page118-1.png](Images/page118-1.png)

##### 4.5 ARRAY OF OBJECTS

C++ allows declaration of arrays of objects like arrays of any other type. An individual object within the array can be accessed by a subscript. The following example illustrates the usage of an array of objects of class student type.

##### **Example 4**. *Use the student class of [Example 1](#chapter_04.xhtml_ch4ex1). Write a program which reads records of *N* number of students in an array of objects and prints the list of students in the following format:*

![page119-1.png](Images/page119-1.png)

*Solution*: The required program, that uses an array of objects of class student type to read and print a list of students, is given below:

![page120-1.png](Images/page120-1.png)

##### 4.6 OBJECTS AS FUNCTION ARGUMENTS

C++ considers objects as built-in data type and therefore, an object can be passed to a function as an argument. An object can be passed in either of the two ways given below. However, each method has its own merits and demerits.

1.  Pass by value
2.  Pass by reference

1.  *Pass by value*: in *pass by value* method of argument passing, the objects are passed to functions by value. A copy of the object is received by the called function, not the actual object. The called function can only use the services of the object because only public members of the object are accessible to the function. For instance, consider the following function (test()) that receives an object of student type through ‘*pass by value*’ and reads its data and displays its grade.

    ![page121-1.png](Images/page121-1.png)

    The output of the program is given below:

    ![page121-2.png](Images/page121-2.png)

    It may be noted that the function main is also trying to display the grade but only garbage is being shown. The reason being that the object studOb, created in main() is different from the object sOb created in test() as shown in [Fig. 4.9](#chapter_04.xhtml_ch4fig9). Therefore, the grade computed by sOb is shown by sOb only and not by studOb of main().

    ![Figure 4.9](Images/ch04fig09.png)

    **Figure 4.9** *The object being passed by ‘pass by value’ method*

2.  *Pass by reference*: in some situations, it is desired that the changes done to an object in the called function should be reflected back into the calling function. This can be resolved with the help of pass by reference method of argument passing of C++. In this method, the address of an object is passed to the function as an argument. The address of the object is represented by preceding the object name with the character ‘&’.

    For instance, consider the following modified function (test()) that receives an object of student type by *‘pass by reference’* and reads its data and displays its grade.

    ![page122-1.png](Images/page122-1.png)

The output of the program is given below:

![page123-1.png](Images/page123-1.png)

It may be noted that the function main is also able to display the grade. The reason being that in pass by reference, only the address of the object has been passed resulting in both test() and main() referring to the same object as sOb and studOb, respectively, as shown in [Fig. 4.10](#chapter_04.xhtml_ch4fig10).

![Figure 4.10](Images/ch04fig10.png)

**Figure 4.10** *Pass by reference – sOb & studOb refer to the same object*

A function can return an object if it has been declared to return the corresponding class of objects. For example, a function some( ) which returns an object of class (say) student type can be defined as shown below:

![page123-2.png](Images/page123-2.png)

##### 4.7 SCOPE RESOLUTION OPERATOR

From our earlier discussion in this chapter we know that, when a member function of a class is large then it is prototyped inside the class and defined outside with the help of a scope resolution operator. The scope resolution operator is a double colon (::) used to connect the definition of functions to their classes. The general form of usage of this operator is shown below:

<return type>   <   class_name   >   ::    <   function _name   >   (parameter list)

In addition to above, we can use the scope resolution operator to access hidden global variables inside a class definition. Consider the program segment given below:

![page124-1.png](Images/page124-1.png)

We can observe that the variable val declared outside the class is global and the variable val declared separately inside the class is local. Now, in normal circumstances we cannot access such a global variable inside the class because any reference to variable val would be considered as local by the compiler. Thus, the global variable val becomes hidden inside the class on account of presence of a local variable with the same name.

We can use the scope resolution operator (::) on the hidden global variable to make it accessible inside the class as shown below:

![page124-2.png](Images/page124-2.png)

![Note](Images/note.png)**Note**: The major difference between scope resolution operator and the dot operator in context of classes and objects is: “The dot operator is used to specify a member of an object whereas the scope resolution operator is used to specify the class name while defining a member function of the class”. The scope resolution operator is also used to make hidden global variable visible inside a class or a block.

##### **Example 5**. *Give the output of following program:*

![page125-1.png](Images/page125-1.png)

*Solution*: The output would be:

![page125-2.png](Images/page125-2.png)

##### **Example 6**. *Write a class matAdd that is capable of adding two matrix objects matOb1 and matOb2 of its own type. Also write a main() function to test the working of the class.*

*Solution*: Let us include the members in the required class called addMat as shown in the class diagram

![page125-3.png](Images/page125-3.png)

where readMat() reads a matrix; displayMat() displays a matrix; addOb() adds two objects of type addMat class.

![Note](Images/note.png)**Note**: The function addOb() has been included as one of the functions of the class. In the absence of this function it would be impossible to add two matrix objects because the data members have been declared private and hence not accessible out side the class. It is left as an exercise for the readers to declare addOb() as stand alone function (not part of the class) and try to add the matrix objects.

The required program is given below:

![page126-1.png](Images/page126-1.png)

A sample output of the program is given below:

![page127-1.png](Images/page127-1.png)

##### **Example 7**. *A class called clock24 has following members:*

***States***

*hour*

*minute*

***Behaviours***

*readtime();*

*showtime();*

*Write a complete program in C++ to input two different objects timeOb1 and timeOb2 of type clock24\. Print their sum (assuming 24 hours clock time).*

*Solution*: The required program is given below:

![page128-1.png](Images/page128-1.png)

The sample output of the program is given below:

![page129-1.png](Images/page129-1.png)

##### **Example 8**. *Compute the size of the object of class matAdd*.

*Solution*: The member wise size and the total size are given below:

1\. *i*, *j*, *m*, *n* = 4 * 2 bytes (each) = 8 bytes

2\. mat[10][10] = 100 * 2 bytes = 200 bytes
Total size = 208 bytes – **Ans.**

##### 4.8 STATIC DATA MEMBERS

When different instances of a class are created then each instantiated object gets its own set of states, i.e. variables. For example, every student object ([Examples 1](#chapter_04.xhtml_ch4ex1) & [2](#chapter_04.xhtml_ch4ex2)) gets its own set of variables to store name, roll no., marks, etc.

However, a data member can be declared as **static** within a function of a class so that it becomes common to all instances of the class. In simple words we can say that a static variable is shared among all instantiated objects of the class.

A static variable, declared within a function of a class has following characteristics:

1.  The static variable is initialized to zero at the time of creation of first object of the class.
2.  It is shared by all instances of the class.
3.  The scope of the static variable is within the function of the class.
4.  Its lifetime starts with the creation of first object and ends with the destruction of last object of the class.

##### **Example 9**. *Write a class called ***testStatic*** that declares a normal integer variable called individual as its private member. It uses public function called disp() which declares a static variable called *common* and displays the contents of both individual and common variables for various instances of objects.*

*Solution*: The required program is given below. It may be noted that in function main(), we are passing the number of the object as an argument to the function disp():

![page130-1.png](Images/page130-1.png)

The output of the program is given below:

![page130-2.png](Images/page130-2.png)

Kindly note that the static variable is common to all the three objects and its contents are getting accumulated (1–3–6) with each invocation of the disp(). However, the normal variable of each object has independent location and stores only the number of the object. Therefore, the variable (normal) that contains data of an individual object is also called an ***instance variable***. Similarly, the static variable that holds data that is common and relevant to all objects is also called as a ***class variable****.* In fact, there is always only one copy of the class variable irrespective of the number of objects instantiated from the class.

In the light of above we can say that the variables individual and common of class testStatic are instance and class variables, respectively.

##### **Example 10**. *What is wrong with the following class declaration?*

![page131-1.png](Images/page131-1.png)

*Solution*:

1.  The keyword public must be followed by a colon.
2.  No variable can be initialized inside a class declaration.

##### 4.9 PROPERTIES OF CLASSES AND OBJECTS

From our discussions on various features of classes, we can observe that the general properties of classes are:

1.  Classes consist of both data (variables) and functions.
2.  Since a class is only processed at compiler level, no variable can be initialized inside a class declaration.
3.  Classes allow private, protected and public members.
4.  A member function defined inside the class is by default an inline function.
5.  A member of a class is by default a private member unless otherwise specified.
6.  A private member is not available outside the class. However, a member function can always access such a member.
7.  Objects can be passed as parameters to functions.
8.  Objects can be returned from a function.

The general properties of objects are:

1.  *Objects are alive* because an object comes into existence. It gets the resources like memory. It has a lifetime.
2.  *Objects are active* because an object provides services through its interface.
3.  *Objects are intelligent* because every object has the coded logic to provide a service or to solve the problem at hand.

##### 4.10 SUMMARY

Any perceivable entity is an object. Every object can be identified as belonging to a class. The activity that combines data and functions into one unit is known as encapsulation. Data and functions are linked on a fundamental level in the form of encapsulation. It enables data, information, and implementation hiding. An abstraction separates the essential part from the implementation details. A static variable, defined in a member function, is common to all instances of the class.

##### ![Question](Images/question.png)MULTIPLE CHOICE QUESTIONS

1.  The world around us is composed of:
    1.  functions
    2.  modules
    3.  data
    4.  objects
2.  An object can be perceived through our:
    1.  imagination
    2.  senses
    3.  intuition
    4.  emotions
3.  Which of the following is not a characteristic of a general object?
    1.  identity
    2.  structure
    3.  states
    4.  behaviours
4.  A class defines common ____ and ____ of a group of objects.
    1.  identity, states
    2.  identity, behaviours
    3.  states, behaviours
    4.  data, data structure
5.  Implementation hiding is carried out by:
    1.  encapsulation
    2.  abstraction
    3.  static functions
    4.  scope resolution operator
6.  An interface is composed of:
    1.  private members
    2.  public members
    3.  stand alone functions
    4.  none of these
7.  A private member can be accessed by:
    1.  a stand alone function
    2.  the interface of the object
    3.  only the private members of the class
    4.  by all the members of the class
8.  A global variable can be accessed within a class by:
    1.  prefixing it by a scope resolution operator
    2.  by declaring it as static
    3.  by a dot operator
    4.  none of these
9.  A member of a class is by default:
    1.  public
    2.  static
    3.  private
    4.  global
10.  An object is ____ of a class.
    1.  copy
    2.  part
    3.  property
    4.  instance

##### ANSWERS

1.  d
2.  b
3.  b
4.  c
5.  a
6.  b
7.  d
8.  a
9.  c
10.  d

##### ![Exercise](Images/exe.png)EXERCISES

1.  Describe the basic concepts of object-oriented programming.
2.  What do you understand by a class in C++?
3.  Write the differences between a structure and a class.
4.  Define the terms class and object. What is the relation between the two?
5.  How does a class accomplish data hiding?
6.  Define the terms: abstraction and encapsulation.
7.  Explain how classes are declared in a C++ program.
8.  Explain the purpose of access specifiers in a class.
9.  Why it is considered a good practice for declaring data members as private?
10.  Explain in brief the rules for definition and declaration of function in a class.
11.  Write a class called boxVolume with length, width and height as data members and readData(), dispData() and computeVol() as functions. Also write a main() function to test the boxVolume class.
12.  Write a class called *bankACNT* that models a bank account having following members:

    **States**

    Name of the client

    Account number

    Type of account

    Balance amount

    **Behaviours:**

    initVal() – to initialize the values

    depAmount() – –to deposit amount

    withdrawAmount() – –to withdraw some amount

    checkBalance() – to check the balance amount

    dispInfo() – –to display the A/C No. and balance

    Write a main() function to test the class bankACNT.

13.  Create a class to represent a book. With following members:

    **States**

    Book

    Title

    Author

    Acc_No

    Code

    date_issued

    date_received

    **Behaviours**

    read_data( )

    compute_fine( )

    dispFine()

14.  Write a program that uses the class book of excercise 13 and manipulates the data of a book through various member functions. Assume rules for the computation of fine for the late reture of a book.
15.  Write a program that creates a list of *N* number of employee objects having following members.

    **States**

    Name

    Age

    empID

    sex

    address

    H.No.

    Street

    Dist.

    State

    **Behaviours:**

    readData()

    dispData()

    The program prints the list of employees in the format given below:

    ![page135-1.png](Images/page135-1.png)
16.  Write a C++ program that inputs today’s date: mm/dd/yy and determines and prints tomorrow’s date correctly. Choose appropriate class declaration and its member data and functions.
17.  Differentiate between instance and class variables.
18.  Write a program that counts the number of objects in a class.
19.  What are the general properties of classes?

## 5

## MORE ON FUNCTIONS: ADVANCED CONCEPTS

##### 5.1 POLYMORPHISM

*“The meeting ends with thanks to the Chair”,* announced the secretary. This message was taken differently by different persons. The Chairman went to his/her office. The accounts clerk distributed the remuneration to the members. The internal members proceeded it to their respective departments. The external experts marched towards the parking place to pick up their vehicles. The secretary took his/her personal assistant along to his/her office for dictation of the minutes of the meeting. And the peon began picking up the papers, littered over the tables. This behaviour is called as *polymorphic* in the sense that the same message was processed in different forms by different group of people. ...

## 6

## CONSTRUCTORS AND DESTRUCTORS

##### 6.1 CONSTRUCTORS

We know that a class is more important than the objects it represents. The reason being that once a class is defined, any number of objects of the class type can be churned out at the run time of the program. We also know that the class is a set of specifications that are used by the compiler for the purpose of construction of objects.

In fact for the creation of an object, the compiler creates a function having the same name as the class itself as shown in [Fig. 6.1](#chapter_06.xhtml_ch6fig1). It may be noted that the name of the class is *myClass* and the name of the function created by the compiler is also *myClass*. This function is called as a **constructor** function. As the name suggests, the constructor function creates an object of its corresponding class type on demand in a program.

![Figure 6.1](Images/ch06fig01.png)

**Figure 6.1** *The constructor function and its operation*

Thus, the constructor function ‘myClass()’ would create an object ‘myOb’ of myClass type as and when the following object creation statement is executed:

myClass myOb;

It may be further noted that the class is a compile time entity whereas the object is a run time entity. Therefore, the object will get the memory and the resources and not the class.

For that reason, the constructor function allocates the memory space for the data items or state variables of each object. However, the member functions are allocated space only once for all instances of objects. But the inline functions are duplicated for every created object.

Now the most important question is that, who calls the constructor function especially when it is a run time entity? The answer is that the compiler inserts the following line in the class (say myClass) at compile time and binds it with its constructor function (see [Fig. 6.1](#chapter_06.xhtml_ch6fig1)).

myClass ( ) { };

It is important to know that the syntax of the constructor is special in the sense that not only its name is same as the name of the class but also it has no return type (not even void).

Since the constructor is the first function to be called before the construction of an object, the programmer can use constructors for variety of purposes as discussed in the following sections.

##### 6.2 TYPES OF CONSTRUCTORS

In C++, there are four types of constructors:

1.  The default constructor.
2.  User defined constructor.
3.  Parameterized constructors.
4.  The copy constructor.

#### 6.2.1 Default Constructor and User Defined Constructor

Consider [Fig. 6.1](#chapter_06.xhtml_ch6fig1). It may be further noted that the compiler has on its own included the following statement in the class definition:

myClass() { }

This is called as a *default constructor*. It can be precisely defined as *the constructor which is defined and called by the compiler. It does no processing but reserves memory for the object. It takes no parameters.*

Thus, a default constructor with empty body does not do anything worthwhile but it is legal. At the time of creation of an object, it is executed and memory is allocated for the object.

However, the programmer can also explicitly define *a user defined constructor* for his/her own advantage in situations similar to as given below.

Many programming situations demand initialization of data members of an object before it is used in a program. For example, in a stack object, the top of the stack must be initialized to –1 to indicate that the stack is initially empty. Let us initialize the top to –1 in the class called stack, given below, and see what happens.

![page178-1.png](Images/page178-1.png)

When the class is compiled, the compiler gives an error on the following statement because we know very well that the class is a compile time entity and will not get the memory and therefore no variables can be initialized within the class.

int top = -1;

In fact, in almost every useful program, some data elements are needed to be initialized before they are used. We can use a default constructor in these situations by putting the initialization statements inside the body of the constructor as shown below:

stack () {int top = -1;}

Now the above arrangement is valid and at the time of creation of object it will work as follows:

1.  The constructor function called *stack()* would be called.
2.  The constructor will provide the memory to the various elements of the class, i.e. the array called *stak[]* and the *top*.
3.  At the time of providing space to the variable top, it will load the desired value –1 into it.

The modified class called *stack* is given below:

![page179-1.png](Images/page179-1.png)

##### **Example 1**. *Write a program that demonstrates the working of a constructor by using the class called stack to simulate its operations: push and pop, for integer values. Modify the push and pop functions so that the following messages are displayed in the calling function main().*

“*Stack is full”, “Stack is empty*”

*Solution*: We would modify the push() and pop() functions to return following values as per the remarks given against them and accordingly the messages would be displayed in function main().

![page180-1.png](Images/page180-1.png)

The complete menu driven program is given below:

![page180-2.png](Images/page180-2.png)

It may be noted that the stack class is inflexible in terms of size of the stack, i.e. it will always create a stack of 20 locations. This problem can be solved by parameterized constructors.

#### 6.2.2 Parameterized Constructors

We can also include arguments in the constructor function definition. *The constructors with arguments are also known as parameterized constructors*. This is helpful in a situation where the programmer wants to provide explicit initial values at the time of creation of an object.

Consider the stack class defined in above sections. As explained above that it will always create a stack of 20 locations. If the user desires to create a stack of a particular size then he can do so by sending the size (say Sz) as an argument at the time of creation of the object. The parameterized stack constructor is given below:

![page182-1.png](Images/page182-1.png)

The modified class is given below:

![page182-2.png](Images/page182-2.png)

The programmer would now create the stack object by the following statements:

stack sOb ( Sz);

where Sz is the size of the stack as specified by the user.

##### **Example 2**. *Design a class called Queue that simulates the queue data structure for N locations, where N is user defined. The class must initialize the Front and Rear location indicators to suitable values through a constructor function. The elements are added and removed from the locations pointed by Rear and Front respectively*.

*Solution:* We would use a parameterized constructor that takes the user specified number of locations (say *N*) for the proposed Queue class and will also initialize Front and Rear to location 0 to mark that the queue is empty.

The required class is given below:

![page183-1.png](Images/page183-1.png)

##### **Example 3**. *Write a program that tests the Queue class for a given size of a queue.*

*Solution*: The required program is given below:

![page184-1.png](Images/page184-1.png)

It may be noted in the above program that the argument for the constructor has been provided during the creation of the object by the following statement:

Queue qOb (Sz);

The format of passing arguments to constructor function is:

<class name> <object name> (argument-list);

This method of passing argument to constructor function is called as *implicit* call. It is a widely used way of providing arguments for the constructor function. However, there is also another way of providing arguments to constructors as shown below:

Queue qOb = Queue (Sz);

This method of passing argument to constructor function is called as explicit call. Since implicit call method of providing arguments is shorter, most of the programmers prefer this method more often.

#### 6.2.3 Copy Constructor

An object can be copied to another with the help of an assignment statement. Consider a simple class called ‘test’ given below:

![page185-1.png](Images/page185-1.png)

Kindly note that the class ‘test’ has two constructors: default constructor and a parameterized constructor, i.e. the constructors have been overloaded. Let us construct two objects Ob1 and Ob2 of class test type in such a way that Ob1 is constructed by the default constructor and Ob2 by the parameterized constructor initializing variable val to 50 through the argument item. The main() function, given below, does this task and prints the contents of val of both the objects. Thereafter, it copies the contents of Ob2 to Ob1 by an assignment statement and again prints the contents of val of both the objects.

![page185-2.png](Images/page185-2.png)

The output of the above code is given below:

![page186-1.png](Images/page186-1.png)

As predicted, the contents of un-initialized val of object Ob1 are random and garbage whereas the val of object Ob2 has been properly initialized to 50\. The point worth noting is that after the assignment of Ob2 to Ob1, the val of both the objects have the same contents.

In fact the following statement has copied the object Ob2 to Ob1 bit by bit.

Ob1 = Ob2;

The above method of copying one object to another of same class type is perfectly alright. However, this method fails in certain situations. For instance, consider an object (say Obptr2) having a pointer (p), pointing to a location containing some information (say ‘My Data’). When this object is copied to another object (say Obptr1) by assignment operator then the pointers of both the objects would point to the same location as shown in [Fig. 6.2](#chapter_06.xhtml_ch6fig2). The reason being that the assignment operator copies the contents of one object to another bit by bit and therefore both the pointers get the same address.

![Figure 6.2](Images/ch06fig02.png)

**Figure 6.2** *Object copy operation through assignment operator*

Now, this abnormal situation would cause many types of problems such as both the objects work on the same location, the changes done by one object to the common location may not be acceptable to another object, etc.

Thus, for copying objects with pointers, we need a mechanism that allows member-wise copy of the objects so that separate space may be allocated to the pointer of the target object.

C++ provides a special constructor called copy constructor that allows the programmer to member-wise copy of one object to another. However, the programmer must write the code for member-wise copy of various members of the source object to the corresponding members of the target object. The copy constructor is, however, defined in the class as a parameterized constructor receiving an object of its own type as argument passed by reference. Consider the class given below:

![page187-1.png](Images/page187-1.png)

It may be noted that the above class ‘myClass’ has a special parameterized constructor that receives an object by reference of its own class type. Now, if we have an obj1 of myClass type and we desire to create a new object obj2 of myClass type, initialized with the contents of obj1 then the following declaration can be used:

![page187-2.png](Images/page187-2.png)

The declaration (i) declares an object obj1 of class myClass type whereas (ii) it declares another object obj2 of class myClass as well as passes the object Obj1 to the copy constructor for member-wise copy as per the programmer’s desire.

##### **Example 4**. Modify the class test, defined above, such that it has a copy constructor that copies an object of test type to another object of test type but while copying the member val of source object, it multiplies it with a number (say 5) and then stores it into the member val of target object.

*Solution*: The required modified class ‘test’ is given below:

![page187-3.png](Images/page187-3.png)

##### **Example 5**. *Write a function main() that creates an object Ob1 of test type with initial value (say 15) and then copies it to an object Ob2 of test type with the help of the copy constructor. Thereafter, it prints the contents of both the objects.*

*Solution*: The required function main() is given below:

![page188-1.png](Images/page188-1.png)

The output of the above is given below:

![page188-2.png](Images/page188-2.png)

It may be noted that the copy constructor has not only copied the object but as desired, it has also multiplied the contents of the source object’s member val (i.e. 15) by 5 before copying it into the corresponding member of the target code. It may be further noted that this would not have been possible by an ordinary assignment operation that uses a default copy constructor.

Let us now take an example of the following class called ‘studData’ that uses a pointer to store personal data of a student who studies in a University.

![page188-3.png](Images/page188-3.png)

It may be noted that the above class has two types of information: common data to all the students such as name of the University and name of the section. For each student there is a personal data accessible through a pointer.

Let us now write a complete program that creates an object ob1 of studData type, reads its data, copies the object to another object Ob2 and prints the data of both the objects. Thereafter, it modifies the personal data of Ob2 and prints the data of both the objects.

![page189-1.png](Images/page189-1.png)

A sample output is given below:

![page190-1.png](Images/page190-1.png)

It may be noted that as predicted, both the objects contain same data after the following copy operation.

Ob2 = Ob1; // Copy the object

However, the strange part is that even after giving new personal data to object Ob2, both the objects show the same data. The only difference is that now the personal data pertains to a student called ‘Sham’ whereas prior to changes, both the objects had the personal data of a student called ‘Ram’. However, the intention was to assign Ob1 to Ram and Ob2 to Sham. The anomaly has occurred because the pointers (ptr) of both the objects are pointing to the same location as was earlier shown in [Fig. 6.2](#chapter_06.xhtml_ch6fig2).

The solution to above problem is to use a copy constructor to copy the objects member wise as per our requirement. The modified class studData is given below:

![page191-1.png](Images/page191-1.png)

It may be noted that we have not only included the copy constructor but have also removed the setPass() function because it had become unnecessary. Let us now write a main() function to test it. We will not repeat the code for readData() and showData() as it remains the same. The required main() function is given below:

![page191-2.png](Images/page191-2.png)

The sample output is given below:

![page192-1.png](Images/page192-1.png)

Kindly note that the copy constructor has done the required task, i.e. the pointers (ptr) of both the objects are pointing to two different locations (see [Fig. 6.3](#chapter_06.xhtml_ch6fig3)). Therefore, each object is having its own separate personal data.

![Figure 6.3](Images/ch06fig03.png)

**Figure 6.3** *The copy operation through copy constructor*

#### 6.2.4 Constructors with Default Arguments

Similar to a normal function, a constructor can also have default values. For example, we can rewrite the class called stack as shown below:

![page193-1.png](Images/page193-1.png)

![Note](Images/note.png)**Note**: A default argument “int Sz = 20” has been specified in the constructor defined in the above given class. Now, an object of class address can be created without specifying the argument. The compiler will always take the default argument “Sz = 20” for the initialization purpose whenever the argument state is missing. However, care must be taken that the default arguments must be the trailing arguments.

#### 6.2.5 Rules for Constructor Definition and Usage

The rules for constructor definition in C++ and its usages are:

1.  The name of the constructor must be same as that of the class.
2.  A constructor can have a parameter list.
3.  The constructor functions can be overloaded.
4.  A constructor with no arguments is the default constructor.
5.  If there is no constructor in a class, a default constructor is generated by the compiler.
6.  The constructor is executed automatically.
7.  The popular abbreviation for constructor is **ctor**.

It may be noted here that an object can be defined at a local level inside a function (say myFun()) or at a global level. When the object is local then it is created as many times as the myFun() is called. Therefore, its constructor is also called every time myFun() is called. When the object is global in nature then its constructor is called at the start of the program.

##### 6.3 DESTRUCTORS

A destructor is an inverse of a constructor in the sense that it removes the memory of an object which was allocated by the constructor during the creation of the object. It carries the same name as the class, but with a tilde (~) as prefix as shown below:

![page194-1.png](Images/page194-1.png)

The rules for destructor definition and usage are

1.  The destructor has the same name as that of the class prefixed by the tilde character ‘~’.
2.  The destructor cannot have arguments.
3.  It has no return type, not even void type.
4.  Destructors cannot be overloaded, i.e. there can be only one destructor in a class.
5.  If there is no destructor in a class, a default destructor is generated by the compiler.
6.  The destructor is executed automatically when the control reaches at the end of class scope.
7.  The popular abbreviation for destructor is *dtor*.

Now the most important question is as to of what use is the destructor function to a programmer? Since the destructor function is the last function to be executed, no fruitful use of this function can be made by the programmer. *However, if we have to find its use then it can be best used for debugging purpose.* In fact, some appropriate message can be included in the destructor function to inform that the object in question is being destroyed. If the message is not displayed by an object then the programmer may infer that the object in question is misbehaving and the program control is struck somewhere within the object itself.

##### **Example 6**. *Write a class called testDest that illustrates the working of a destructor. It displays the following message as soon as its object is destroyed.*

“I am being destroyed”

*Write a smallest possible main() function for testing the working of the destructor.*

*Solution*: The required class with destructor and the minimal main() function is given below:

![page194-2.png](Images/page194-2.png)

The output of above program is given below:

![page195-1.png](Images/page195-1.png)

It may be noted that the constructor and the destructor are called automatically by the system as and when the object is created or destroyed – as the case may be.

##### 6.4 SUMMARY

Constructor is a function that creates an object. It is a special function that returns no value not even the void. It helps the programmer to automatically initialize certain data members of an object at the time of its creation. The name of the constructor is same as the class. A copy constructor initializes one object with values from another object of the same class type. The destructor function destroys the object. It removes the memory held by an object. It is the last member function to be called. It also carries the same name of the class with a tilde (~) as prefix. The destructor function can be used for debugging purposes.

##### ![Question](Images/question.png)MULTIPLE CHOICE QUESTIONS

1.  A constructor function returns:
    1.  an integer
    2.  a float
    3.  no value
    4.  void
2.  A constructor function automatically initializes the data members of an object at the time of its:
    1.  declaration
    2.  creation
    3.  destruction
    4.  compilation
3.  The name of the constructor function is:
    1.  same as class name
    2.  same as program name
    3.  user defined name
    4.  none of these
4.  Is constructor function a friend of the class?
    1.  yes
    2.  no
5.  What happens if an object is passed by value to a copy constructor?
    1.  the size of the object increases
    2.  the size of the object decreases
    3.  system may run out of memory
    4.  compiler runs out of memory
6.  A constructor with no arguments is called:
    1.  copy constructor
    2.  default constructor
    3.  parameterized constructor
    4.  none of these
7.  When an object consists of pointer variables, it must be copied through:
    1.  assignment operator
    2.  a user defined function
    3.  copy constructor
8.  What is the popular abbreviation for constructor?
    1.  conc
    2.  tor
    3.  cons
    4.  ctor
9.  What is the popular abbreviation for destructor?
    1.  dtor
    2.  tor
    3.  dest
    4.  ~des
10.  What happens if there is no constructor defined in a class?
    1.  the object is not created
    2.  the program terminates
    3.  the objects gets created
    4.  none of these

##### ANSWERS

1.  c
2.  b
3.  a
4.  b
5.  c
6.  b
7.  c
8.  d
9.  a
10.  c

##### ![Exercise](Images/exe.png)EXERCISES

1.  What is a constructor? Explain its utility.
2.  Define the terms: default constructor and parameterized constructor.
3.  Modify [Example 1](#chapter_04.xhtml_ch4ex1) of [Chapter 4](#chapter_04.xhtml) such that the class contains a constructor function.
4.  Design a constructor with default values for [Example 4](#chapter_04.xhtml_ch4ex4) of [Chapter 4](#chapter_04.xhtml).
5.  Design a suitable constructor function for [Example 9](#chapter_04.xhtml_ch4ex9) of [Chapter 4](#chapter_04.xhtml).
6.  Explain copy constructor in detail.
7.  Define the term destructor.
8.  Describe the importance of destructor function.
9.  Write a program that illustrates the working of a destructor function.
10.  Given the following C++ code, answer the questions (a) and (b).

    ![page196-1.png](Images/page196-1.png)

    1.  In object-oriented programming, what is Function1 referred to as and when does it get invoked/called?
    2.  In object-oriented programming, what is Function2 referred to as and when does it get involved/called?
11.  Write a program in C++ that creates a class called ‘time’ with data members: hour, minutes, and seconds of type integer, integer, and float, respectively. The class uses two constructors. One constructor is used to initialize the time data elements to zero. The second constructor is used to set the time components to a predetermined time, passed by the user as arguments. The class also has two member functions: dispTime() and addTime(). The dispTime() displays the time in: hh:mm::ss.ss format. The other function addTime() adds two objects T1 and T2 of time type such that T3 = T1 & T2, where T3 is also of type ‘time’.

## 7

## INHERITANCE: EXTENDING CLASSES

##### 7.1 INTRODUCTION TO CODE REUSE

Almost all programming languages support functions that allow a piece of code to be reused again and again in a calling program. However, functions provide rather limited support for code reuse. In object-oriented programming (OOP), code reuse is a central feature. In fact, we can reuse the code written in a class in another class by either of the two mechanisms given below:

1.  Containership
2.  Inheritance

##### 7.2 CONTAINERSHIP

In day-to-day life, we come across objects which are composed of other objects. For instance, a computer is composed of objects like motherboard, hard disk, CD-ROM drive, monitor, etc. The motherboard contains a CPU and other components. The CPU contains ALU, CU and ...

## 8

## TEMPLATES: CODE SHARING (GENERICITY)

##### 8.1 INTRODUCTION TO CODE SHARING

There are many programming situations where same set of operations is applied on different data types. For example, the following function exchanges the contents of two variables of type int.

![image](Images/pg235-1.png)

Now, consider a situation where we also need to exchange the contents of variable of type: float and char. Accordingly, we will have to define the following two functions:

Function for float type variables:

![image](Images/pg235-2.png)

Function for char type variables:

![image](Images/pg235-3.png)

It may be noted that 99% of the code in the above three functions is same except the type declaration: int, float and char. Now the pertinent question arises that “Can’t we write a *generic* function that can accept all types of parameters?”. If yes, then a tremendous amount of typing effort can be saved. This will not only increase the productivity of the programmer but also reduce the size of the program. However, the programmer must demarcate the program code into two categories: type dependent and type independent codes.

In fact, there are plenty of applications of such generalized (generic) codes. For instance, a compiler needs to maintain variety of tables: symbol table, literal table, opcode table, compiler directive table, function name table, etc. All tables are operated in search–insert fashion and the code for these operations is almost same. Similarly the compiler maintains as many stacks as types of data it works upon.

Code sharing is implemented in C++ through **templates**. A detailed discussion on this feature is given in the following sections.

##### 8.2 TEMPLATES

A template in C++ is used to create generic functions and classes. The format of template declaration is given below:

![image](Images/pg236-1.png)

where template is a keyword; “<” is the standard left angled bracket or sign for less than operator; class is a keyword; ugType, user defined generic type; “>” is the standard right angled bracket or sign for greater than operator.

The user-defined type (ugType) becomes the generic type. Let us now rewrite the function exchange() of [Section 8.1](#chapter_08.xhtml_ch1) as a generic function.

![image](Images/pg236-2.png)

It may be noted that we have used a generic type called ‘myType’ to declare the variables in the generic function ‘exchange’. This generic type (myType) would get substituted at run time by whichever type of data is sent by the programmer. Thus, templates use run time polymorphism to bind the data with their types.

##### **Example 1**. *Write a program that uses the generic function exchange() and tests it for variety of types of data.*

*Solution*: The required program is given below:

![image](Images/pg237-1.png)

The output of the program is given below:

![image](Images/pg237-2.png)

It may be noted that the generic function exchange() has been able to work with various types of data.

##### **Example 2**. *Write a function template called search() that searches an element (generic type) from a given list of *N* elements. It returns 1 when the element is found 0 otherwise. Also write a generic function called readList() that reads a list of *N* elements.*

*Solution*: We will use an array of *N* locations of generic type. However, the size of array *N* and the index *i* will be declared as integers because these variables are type dependent.

The required functions are given below:

![image](Images/pg238-1.png)

##### **Example 3**. *Write a menu driven function main() that tests the working of the generic functions developed in [Example 2](#chapter_08.xhtml_ch8ex2) for integer and float values.*

*Solution*: The required function main() is given below:

![image](Images/pg238-2.png)

A sample output is given below:

![image](Images/pg239-1.png)

![image](Images/pg239-2.png)

![image](Images/pg240-1.png)

##### 8.3 GENERIC CLASSES

Similar to functions, we can also create generic classes in the form of class templates. The format of a *class template* is given below:

![image](Images/pg240-2.png)

where template is a keyword; “<” is the standard left angled bracket or sign for less than operator; class is a keyword; ugType, user defined generic type; “>” is the standard right angled bracket or sign for greater than operator.

![Note](Images/note.png)**Note** : The template declaration followed by class declaration is jointly called as a *class template*.

##### **Example 4**. *Write a class template called stack that offers the following services for generic type of data.*

1.  *Push an element on a stack.*
2.  *Pop an element from a stack.*

*Solution*: The required class is given below:

![image](Images/pg240-3.png)

It may be noted that when a member function of a generic class is declared outside the class then it has to be separately defined as a template. The format of defining a member function is given below:

![image](Images/pg241-1.png)

![Note](Images/note.png)**Note** : <ugType> has to be written within a pair of angled brackets (< and >).

For example, the push() function of generic class called ‘stack’ has been declared as given below:

![image](Images/pg241-2.png)

![Note](Images/note.png)**Note** : An object of generic type class can be created by qualifying (or type casting) the statement by the type for which the object is desired. The format of object creation for a generic class is given below:

![image](Images/pg242-1.png)

where class name is the name of the class; “<” is the standard left angled bracket or sign for less than operator; typeOb is the type of data for which the object is required; “>” is the standard right angled bracket or sign for greater than operator; object name, name of the object to be created.

For example, an object named ‘chOb’ of type stack that works on char type of data can be created by the following statement:

![image](Images/pg242-2.png)

Kindly note that angled brackets are necessary for type casting the required object. The name of the class juxt aposed with the type in angled brackets (i.e. stack <char>) is called a *template class*.

##### **Example 5**. *Write the function main to test both the stacks for values 70 and 23.54 to be pushed and popped from the integer and float stacks, respectively.*

*Solution*: The required function main() is given below:

![image](Images/pg242-3.png)

The output of the above program is given below:

![image](Images/pg243-1.png)

It may be noted that same class has been used to instantiate two different objects capable of working on integer and float type data, respectively. Therefore, a generic class is also known as a **parameterized class**.

There is only one piece of generic code which is being shared by different objects working on different types of data. Thus, we can say that *templates help us in* **sharing the code** *among structurally similar family of objects or functions*.

##### 8.4 TEMPLATES WITH MORE THAN ONE GENERIC PARAMETER

A template can have more than one generic parameter as shown by the following declaration:

template <class genType1, class genType2>

The above template declaration is using two generic types: genType1 and genType2\. The advantage of this feature of C++ is that a function template or class template can be called for more number of generic parameters.

Consider the following function template:

![image](Images/pg243-2.png)

It may be noted that it is using two generic types: *T* and *U*. It adds two formal parameters *x* and *y* of type *T* and *U*, respectively. The sum is stored in a variable called ‘result’ of type U. Thereafter the contents of ‘results’ are printed.

##### **Example 6**. *Write a complete program that uses the generic function test(), developed above and tests it for various combination of parameters of different types.*

*Solution*: We would test the generic function for various combinations of values of types int, float and char. The complete program is given below:

![image](Images/pg244-1.png)

The output of this program is given below:

![image](Images/pg244-2.png)

It may be noted that the generic function is able to work with two generic parameters. It is giving correct results for various combinations of different types of data.

##### 8.5 SUMMARY

A generic function and class can accept parameters of different types. It allows code sharing with a view to reduce typing effort, increase productivity and reduce the size of the program. The code of a program can be comfortably divided into two parts: type dependent and type independent. The ‘generic type’ gets substituted at runtime by the type of data supplied to the generic function or class. A template declaration followed by a class declaration is jointly called a ‘**class template**’. The name of class juxt aposed with a type in angled brackets is called a ‘**template class**’. A template can have more than one generic parameter.

##### ![Question](Images/question.png)MULTIPLE CHOICE QUESTIONS

1.  A generic function increases:
    1.  productivity
    2.  program length
    3.  typing effort
2.  A template in C++ is used to create _______ functions
    1.  virtual
    2.  generic
    3.  recursive
    4.  friend
3.  The templates use_____ polymorphism to bind the data with their types
    1.  compile time
    2.  runtime
4.  A generic class is called as:
    1.  base class
    2.  derived class
    3.  parameterized class
    4.  friend class
5.  Templates help us in sharing the code among structurally ______ family of objects or functions
    1.  dissimilar
    2.  superior
    3.  conflicting
    4.  similar

##### ANSWERS

1.  a
2.  b
3.  b
4.  c
5.  d

##### ![Exercise](Images/exe.png)EXERCISES

1.  What is a generic function?
2.  How ‘code sharing’ is implemented in C++?
3.  What is a template and how it is defined?
4.  Write a template called areaSq() that computes and returns the area of a square. It takes an argument called ‘side’ of generic type. Test this function for a given side of type: int, float, double.
5.  Write a generic function called ‘sort()’ that sorts a list of given *N* data items of generic type into ascending order.
6.  Write a function main() that tests the above function ‘sort()’ through a menu driven interface.
7.  Differentiate between ‘class template’ and ‘template class’.
8.  Write a ‘class template’ called ‘queue’ that offers the following services for generic type of data.
    1.  add an element on a queue
    2.  remove an element from a queue
9.  Write a template function called ‘searchTab()’. It maintains a symbol table having following format:

    | Symbol | Value |
    |  |  |

    The symbol is an array of character types whereas the value can be of any one of the available type for a particular table, i.e. int, float, char, etc.

10.  Write a function main() that tests the above function ‘searchTab()’ for a symbol of type int.
11.  Write a function main() that tests the above function ‘searchTab()’ for a symbol of type float.

## 9

## OPERATOR OVERLOADING

##### 9.1 INTRODUCTION

Let us consider a situation where we have a class called ‘length’ which represents the length of an item (say cloth) in feet and inches. Its class diagram is shown in [Fig. 9.1](#chapter_09.xhtml_ch9fig1).

![Figure 9.1](Images/ch09-fig01.png)

**Figure 9.1** *A class called ‘length’*

Now if we desire to add two objects of this class type, one of the options is to use a friend function (say **add()**) as shown below:

![image](Images/pg247-1.png)

The following main() function tests the above given class.

![image](Images/pg248-1.png)

A sample ...

## 10

## FILE HANDLING IN C++

##### 10.1 FILE CONCEPTS

We know that every program or sub-program consists of two major components: algorithm and data structures. The algorithm takes care of the rules and procedures required for solving the problem and the data structures contain the data. The data is manipulated by the procedures for achieving the goals of the program as shown in [Fig. 10.1](#chapter_10.xhtml_ch10fig1).

![Figure 10.1](Images/ch10-fig01.png)

**Figure 10.1 *The structure of a program or sub-program***

In object-oriented programming (OOP), an object is central to the ideology. The object has two components: states and behaviours. The states and behaviours model the data and procedures, respectively. Each behaviour is implemented as a subprogram having arrangement similar to that in [Fig. 10.1](#chapter_10.xhtml_ch10fig1).

A data structure is volatile by nature in the sense that its contents are lost as soon as the execution of the program is over. Similarly, an object also loses its states after the program is over. If we want to permanently store our data or want to create persistent objects then it becomes necessary to store the same in a special data structure called file. The file can be stored on a second storage media such as hard disk. In fact, vary large data is always stored in a file.

Now, any thing stored on a permanent storage such as hard disk is called a file. For example, MBR (master boot record), FAT (file allocation table), partition table, programs, data files, etc. are examples of files.

Let us consider the information recorded in [Fig. 10.2](#chapter_10.xhtml_ch10fig2).

![Figure 10.2](Images/ch10-fig02.png)

**Figure 10.2** *Information about students*

Each entry into the table shown in [Fig. 10.2](#chapter_10.xhtml_ch10fig2) is a set of three data items: Roll number, Name and Marks. The first entry states that the Roll number and total marks of a student named as Ajay are 001 and 50, respectively. Similarly the second entry relates to a student named as Ram whose Roll number is 002 and total marks equal to 70\. Each entry of the table is also known as a record of a student. The term *record* can be defined as *a set of related data items of a particular entity such as a person, machine, place, or operation. An individual data item within a record is known as a* field*.* When a field assumes unique values then it is called a *key-field*. For example, ‘Roll’ is the key-field in the record of the student as shown in [Fig. 10.3](#chapter_10.xhtml_ch10fig3).

![Figure 10.3](Images/ch10-fig03.png)

**Figure 10.3** *Structure of a record*

Thus, the record of a student is made up of following three fields:

1.  Roll number
2.  Name
3.  Marks

Let us assume that a particular class has 30 students. Now, the entire information of the class consisting of 30 records is referred to as a file. The arrangement of records in the file is shown in [Fig. 10.4](#chapter_10.xhtml_ch10fig4).

![Figure 10.4](Images/ch10-fig04.png)

**Figure 10.4** *File: collection of records*

A *file* can be precisely defined as *a logical collection of records where each record consists of a number of items known as fields*. The records in a file can be arranged in the following three ways:

1.  *Ascending/descending order*: the records in the file can be arranged according to ascending or descending order of a key field. For example, the records in the file of [Fig. 10.4](#chapter_10.xhtml_ch10fig4) are in ascending order of its Roll field.
2.  *Alphabetical order*: if the key field is of alphabetic type then the records are arranged in alphabetical order.
3.  *Chronological order*: in this type of order, the records are stored in the order of their occurrence, i.e. arranged according to dates or events. If the key-field is a date, i.e. date of birth, date of joining, etc. then this type of arrangement is used.

When the data of a file is stored in the form of readable and printable characters then the file is known as a **text file**. It is a special type of file that does not contain records but only characters. On the other hand, if a file contains non-readable characters in binary code then the file is called as a **binary file**. For instance, the program files created by an editor are stored as text files whereas the executable files generated by a compiler are stored as binary files.

In the following sections, an introduction to files supported by C++ is given.

##### 10.2 FILES AND STREAMS

In C++, a stream is a data flow from a source to a sink. The sources and sinks can be any of the input/output (I/O) devices or files. For input and output, there are two different streams called input stream and output stream as shown in [Fig. 1.2](#chapter_01.xhtml_ch1fig2). We have already used the following unformatted I/O streams in our previous programs:

| Stream | Description |
| cin | Standard input stream |
| cout | Standard output stream |
| cerr | Standard error stream |

The standard source and sink are keyboard and monitor screen, respectively. These unformatted streams are initialized whenever the header file <iostream.h> is included in a program. However, we need to use the operators ‘<<’ and ‘>>’ to implement these streams.

The important stream classes required for file I/O are ifstream, ofstream and fstream. A brief discussion on these streams is given below:

*ifstream*: It is the input file stream class. Its member function open( ) associates the stream with a specified file in an input mode. For example, if it is desired to open a file called “xyz. dat” for input then the following statements can be used.

![image](Images/pg265-1.png)

The above declaration means creating an input stream called myfile and associating it with the file called “xyz.dat”. In addition to open(), ifstream class inherits the following functions from istream class.

(i) get( ); (ii) getline( ); (iii) read( ); (iv) seekg( ); (iv) tellg( )

*ofstream*: It is the output file stream class. Its member function open( ) associates the stream with a specified file in an output mode. For example, if it is desired to open a file called “abc.bat” for output then the following statement can be used:

![image](Images/pg265-2.png)

The above declaration means creating an output stream called yourfile and associating it with the file called “abc.dat”. In addition to open(), ofstream inherits the following functions from ostream class

(i) put( ); (ii) write( ); (iii) seekp( );, (iv) tellp( )

*fstream*: It supports files for simultaneous input and output. It is derived from ifstream, ofstream and iostream classes. The functions associated with this stream are:

1.  open: This associates the stream with a specified file.
2.  close: It closes the stream.
3.  close all: It closes all the opened streams.
4.  seekg: Sets current ‘get’ position in a stream.
5.  seekp : Sets current ‘put’ position in a stream.
6.  tellg: Returns the current ‘get’ position in a stream.
7.  tellp: Returns the current ‘put’ position in a stream.

The header file ‘fstream.h’ contains all the class declarations required for file I/O. Even ‘iostream.h’ is included in ‘fstream.h’ and therefore, ‘fstream.h’ should be included in a program that manipulates files.

##### 10.3 OPENING AND CLOSING A FILE (TEXT FILES)

A file can be opened in C++ by two methods:

1.  By using the constructor of the stream class to be used.
2.  By using the open( ) function of the stream class to be used.

The first method is simple to start with. Let us consider a situation wherein we desire to open a file called “message.dat” containing the following text:

> *“When you feel angry, keep your mouth shut.*
> 
> *Don’t talk and your anger will be fifty percent gone.*
> 
> *Drink some cold water and it will be seventy five*
> 
> *percent gone. Get out of the house and take a walk,*
> 
> *and it will be one hundred percent gone.”*

We will open this file by using the default constructor of the ofstream class by the following statement:

ofstream  myfile  (“message.dat”);

The above declaration means open an output stream called myfile and initialize it with the name “message.dat”. The “message.dat” is the name of the file lying on the hard disk. However, in the program it will be known as myfile. Thus, whatever is written in myfile stream in the program, will actually be written into the file “message.dat”. Since a simple text is to be written into the file, we can use the operator << to write the data. The following program creates the required file:

![image](Images/pg266-1.png)

It may be noted from the above program that the stream myfile has been used inside the program instead of ‘cout’ stream to write the text in the file with the help of the operator ‘<<’. Moreover, a function close( ) has been used to close the file at the end of the program.

The desired file called “message.dat” has been created by the above program in the current directory. Let us open the file in a text editor (say notepad) to verify the contents. The snapshot of notepad is given in [Fig. 10.5](#chapter_10.xhtml_ch10fig5):

![Figure 10.5](Images/ch10-fig05.png)

**Figure 10.5** *The contents of ‘message.dat’*

It may be observed that not only the above program has created the desired file: ‘message.dat’ but also it contains the correct contents.

We can open the created file for input by using the default constructor of the ifstream class by the following statement:

ifstream yourfile (“message”);

The above declaration means: open an input stream called yourfile and initialize it with the name “message.dat”. Thus, the file “message.dat” will be known as yourfile in the program. Since it is a simple text file, we can use the operator ‘>>’ to read the data from the file. However, there is a limitation of the operator ‘>>’ in reading a string containing blanks or white space characters. The operator ‘>>’ stops the input at the occurrence of first white space in the input string. Thus, we can read a word at time from the text file by the ‘>>’ operator.

However, for reading entire lines of text, C++ provides get( ) and getline( ) functions as input member functions of the ifstream class. It also provides a put( ) function as output member function of the ofstream class. These functions are discussed in the following sections.

#### 10.3.1 Function get( )

This function is similar to operator ‘>>’ except that it includes white space characters or blanks in the input string. However, it stops at ‘\n’, the new line character. This function can be used in one of the following variations:

1.  get (ch) (i)
2.  get (ch, n) (ii)

The first variation of get( ) reads a character at a time from the stream whereas the second variation reads a string of characters of length *n* – 1\. In fact, it reads *n* – 1 number of characters for a specified size *n*.

Let us now write a program that reads the file “message.dat” for us. We will use function get( ) to read a line at a time from the file in a variable called row and repeat this task as many times as there are text lines in the file. The program is given below:

![image](Images/pg268-1.png)

![Note](Images/note.png)**Note**: while reading a line the get( ) function stops at ‘\n’. Therefore, in the above program an extra get( ) has been used in the form of yourfile.get(ch) to read the end of line, i.e. ‘\n’.

The output of the above program is given below:

![image](Images/pg268-2.png)

It may be noted that the above program has not only opened the file “message.dat” but also read the text of the file and displayed on the computer screen.

#### 10.3.2 Function getline( )

The format of the function getline( ) is shown below:

getline (ch, N)

This function reads a line of characters that terminates with ‘\*n*’, i.e. a new line character. It reads the characters from a line till it encounters a ‘\n’ or *N* – 1 characters are read, where *N* is the specified length of the character to be read from the file.

A modified program that uses getline( ) function to read the file “Message.dat” is given below:

![image](Images/pg269-1.png)

The getline( ) and get( ) functions have another variation, wherein their argument list can contain a third argument as shown in the following format:

1.  getline(ch, n, c)
2.  get(ch, n, c)

The third argument ‘c’ is known as the terminating character. The default terminating character is ‘\n’, i.e. the new line character.

##### **Example 1**. *Modify the above program to read a line from the file “message.dat”, terminated by the alphabet ‘k’.*

*Solution*: The required program is given below:

![image](Images/pg270-1.png)

The output of this modified program is given below:

![image](Images/pg270-2.png)

Kindly note that the stream yourfile has read the characters from beginning of the line till it encountered the character “k”.

However, it is worth noting that the above programs work only with a particular file called “message.dat”. It is quite an inflexible arrangement whereas in a real life situation, we would like these programs to work with any user specified text file.

The desired flexibility can be brought by the following two simple steps:

1.  Read the name of file to be opened at run time in a variable of type char.
2.  Open the stream in a desired mode and associate the stream with the variable that contains the name of the file to be opened.

The following example opens a file for which the user supplies the name at run time.

##### **Example 2**. *Write a program that prompts the user to enter the name of the file to be opened (say “message.dat”). It associates the file name with the output stream (say yourfile) and displays its contents.*

*Solution*: The required program that reads the name of the file, to be opened, at run time is given below:

![image](Images/pg271-1.png)

The output of the program is given below:

![image](Images/pg271-2.png)

It may be noted that the program has now prompted the user to enter the name of the file to be read. The advantage is that the program has become flexible, i.e. the user can give name of any of the existing files at run time.

Though opening of a file through a constructor is an easy method but the following points should be kept in mind while opening the files:

1.  Only one file can be connected to a stream.
2.  A file opened in any mode (input or output) must be closed by the function close( ).
3.  If a file is opened for output then a new file would be created if no file with the same name already exists otherwise the contents of the existing file will be deleted.

#### 10.3.3 Function put( )

This function writes a single character at a time to the output stream. For example, the following statement will write the character content of character variable ‘ch’ into the stream called testfile.

testfile.put  (ch);

##### **Example 3**. *Write a program that writes the following piece of text in a user defined file (say “thought.dat”.). Verify the creation of the file by opening the same in output mode and printing its contents on the screen.*

*“True education is that destroys narrow-mindedness”*

*Solution*: We would use the function ‘put()’ to write the above given text of 47 characters into a user specified file. The required program is given below:

![image](Images/pg272-1.png)

The above program writes the text “*True education is that destroys narrow-mindedness*” character by character into a file whose name is provided by the user at run time. The program reads the line from the file and displays it on the screen. The output of the program is given below:

![image](Images/pg273-1.png)

##### 10.4 OPENING THE FILES BY USING FUNCTION OPEN( )

A file can also be opened in a program by a function called open( ). However, we must specify the stream to be associated with the file. For example a file called “test.dat” can be opened for output by the following set of statements:

![image](Images/pg273-3.png)

The statement (i) declares the stream newfile to be of type ofstream, i.e. output stream. The statement (ii) assigns the file stream to the file called “test.dat”. Thus, in the program the file “test.dat” would be known as newfile. The major advantage of this method is that more than one files can be opened at a time in a program.

##### **Example 4**. *Write a program that creates a text file called ‘copy.dat’ which is an exact copy of a given textfile called ‘thought.dat’.*

*Solution*: We will open two streams orgFile and copyFile in input and output streams, respectively. The physical files ‘thought.dat’ and ‘copy.dat’ would be assigned to orgFile and copyFile, respectively. The get() and put() functions would be used to copy the contents of orgFile to copyFile. The required program is given below:

![image](Images/pg273-2.png)

In order to verify the effectiveness of the above program, let us open the ‘copy.dat’ in notepad. The snapshot of the notepad is given below:

![image](Images/pg274-1.png)

It may noted that the above program has created an exact copy of the ‘thought.dat’ into a new file called as ‘copy.dat’.

##### 10.5 READING AND WRITING BLOCKS AND OBJECTS (BINARY FILES)

In the previous sections, we have used text files. Let us now write binary files which are more versatile and popular among programmers. The major advantage of such files is that they require less memory space for storage of data. Moreover, these files can be used to read or write structured data such as structures, class objects, etc.

For binary files, the functions read() and write() are used to read and write objects, respectively. Blocks of data can also be read or written by these functions. The general form of read( ) function is given below:

<name> . read ((char *) & <block>, size);

where <name> is the name of the input stream; <block> is the name of the block to be read from the stream; size is the size of the block which can be obtained by a function called size of( ).

The general form of write( ) function is given below:

<name> . write ((char *) & <block>, size);

where <name> is the name of the output stream; <block> is the name of the block to be written into the stream; size is the size of the block.

![Note](Images/note.png)**Note**: The type cast (i.e. (char *)) is necessary in the read( ) and write( ) functions.

Let us write the record given below in a file called “Test.dat”.

![image](Images/pg275-1.png)

The steps required to do this task are:

1.  Create a structure called officer-data.
2.  Initialize a structure variable with the given data or read it from the keyboard.
3.  Open an output stream (say ofile).
4.  Associate the stream ofile with the file “Test.dat”.
5.  Obtain the size of the structure by the function size of ( ).
6.  Write the structure into the file by write( ) function.

The above given steps are implemented in the program given below:

![image](Images/pg275-2.png)

The following data was submitted during the run of the above program

![image](Images/pg276-1.png)

A program that reads the block of data from the file called “Test.dat” and displays it as given below:

![image](Images/pg276-2.png)

The output of above program is given below:

![image](Images/pg277-1.png)

It may be noted that the record of the officer was correctly written and read by the above two programs.

##### **Example 5**. *Write a program which creates a file containing the records of officers working in a University. The name of the file is provided by the user.*

*Solution*: The required program is given below:

![image](Images/pg277-2.png)

##### **Example 6**. *Write a program which reads a file containing the records of officers working in a University. The name of the file is provided by the user. The records of the officers are displayed in the following format:*

![image](Images/pg278-2.png)

*Solution*: The required program is given below:

![image](Images/pg278-1.png)

A sample output of the program is given below:

![image](Images/pg279-1.png)

#### 10.5.1 Storing Objects in Files

Normally the contents of an object are lost as soon as the object goes out of scope or the program execution is over. If the information contained in the object is very important then we must try to save it on auxiliary storage such as hard disk so that it can be reused as and when required. In fact, similar to records, objects can also be written into and instantiated from a file. The objects which remember their data and information are called as **persistent objects**.

Thus, a persistent object exists in two forms: in the primary memory, i.e. RAM and the secondary memory such as hard-disk. The RAM-copy of the object represents the current state of the object for that moment, the disk copy of the object represents the old state of the object.

The program can make changes to the object in the primary memory and before going out of scope, the object is written onto the disk in a file. The following example is using the student object for the purpose of illustrating the above discussed concept.

##### **Example 7**. *Consider the class called student of [Example 1](#chapter_10.xhtml_ch10ex1) of [Chapter 4](#chapter_04.xhtml) which models the following states and behaviours of a student:*

***States***

*Name*

*Roll*

*Marks*

*Grade*

***Behaviours***

*Read_data()*

*Display_grade()*

*Compute_grade()*

*Perform the following operations*

1.  *Create an object of student type and reads its data.*
2.  *Write the object onto a file (say “student.dat”).*
3.  *Read the object from the file.*
4.  *Display the data onto the screen.*

*Solution*: The required program is given below:

![image](Images/pg280-1.png)

A sample output of the program is given below:

![image](Images/pg282-1.png)

It may be noted that the student data was supplied for the object ‘sOb1’. Its grade was computed and it was stored into a file called “student.dat”. The stored object was read in another object called ‘sOb2’ from the file. From the output, it is verified that the contents have remained intact.

From above, it may be appreciated that this arrangement can be used to store objects on files for their usage at later stage.

##### **Example 8**. *Write a program which opens a file whose name is provided by the user (say “studFile.dat”). The program writes *N* (say 5) number of objects of student types into the file.*

*Solution*: The required program is given below:

![image](Images/pg282-2.png)

![Note](Images/note.png)**Note**: In this section, only an introduction to persistent objects is being given. A little more effort is required to make those objects persistent which are objects of derived classes and are having pointers.

##### 10.6 DETECTING END OF FILE

As far as files are concerned, till now we have been reading or writing a certain number of characters or objects. While reading a file, a situation can arise when we do not know the number of objects to be read from the file, i.e. we do not know where the file is going to end? A simple method of detecting **end of file** (eof) is by testing the stream in a while loop as shown below:

![image](Images/pg284-1.png)

The condition <stream> will evaluate to 1 as long as the end of file is not reached and it will return 0 as soon as end of file is detected. In simple words, we can say that the while loop will terminate as soon as the eof of <stream> is reached. Consider the following program segment

![image](Images/pg284-2.png)

The while loop in this program executes till eof of xfile is reached. The following example illustrates the usage of detection of eof.

##### **Example 9**. *Write a program which opens a file created in [Example 8](#chapter_10.xhtml_ch10ex8) (“studFile.dat”). The program reads the objects from the file till the end of the file.*

*Solution*: The required program is given below:

![image](Images/pg285-1.png)

The output is given below:

![image](Images/pg286-1.png)

The end of file can also be detected by a function called ‘eof()’. This function returns a non-zero value when it detects the end of file else it returns a zero. An example of usage is given in the following program segment:

![image](Images/pg287-1.png)

##### **Example 10**. *Modify the function main() of [Example 9](#chapter_10.xhtml_ch10ex9) such that it uses the function ‘eof()’ for detecting the end of the file.*

*Solution*: The required modified function main() is given below:

![image](Images/pg287-2.png)

##### **Example 11**. *Write an interactive menu driven program that creates a text file (say “input.dat”) and then displays its contents. The program also creates another text file (say “output.dat”) as copy of the former. However, while copying it converts all the characters into their equivalent uppercase characters.*

*Solution*: We will use toupper() function to convert the characters read from the original file. The required program is given below:

![image](Images/pg287-3.png)

The output is given below:

![image](Images/pg289-1.png)

##### 10.7 SUMMARY

Any thing stored on a permanent storage is called a *file*. A set of related data items is known as a record. The smallest unit of a record is called a *field*. A key field is used to uniquely identify a record. A file is a logical collection of records. In a serial file, the records are stored in the order of their arrival without considering the key field. On the other hand, in a sequential file, the records are written in a particular order of the key field. The key field is also known as a *primary key*. ‘ifstream’ and ‘ofstream’ are input and output streams, respectively. The objects that remember their data and information are called *persistent* objects. The function *eof()* returns 0 when it detects the end of file. An opened file must be closed after its usage.

##### ![Question](Images/question.png)MULTIPLE CHOICE QUESTIONS

1.  A program consists of two major components: algorithm and
    1.  logic
    2.  code
    3.  data structures
    4.  output
2.  An object has two components: states and
    1.  abstraction
    2.  behaviours
    3.  encapsulation
    4.  variables
3.  Any thing stored on a permanent storage is called a:
    1.  file
    2.  data
    3.  information
    4.  object
4.  A set of related data items of a particular entity is called a:
    1.  record
    2.  file
    3.  data
    4.  field
5.  A field having a unique value is called:
    1.  main field
    2.  local field
    3.  global field
    4.  key field
6.  A logical collection of records is called a:
    1.  pile
    2.  group
    3.  file
    4.  class
7.  The stream that supports both input output is called:
    1.  ifstream
    2.  fstream
    3.  ofstream
    4.  iostream
8.  A file can be opened by a ______ constructor
    1.  copy
    2.  default
9.  The functions read() and write() are used to read() and write()
    1.  data
    2.  file
    3.  objects
    4.  information
10.  The RAM copy of the object represents its:
    1.  current sate
    2.  old state

##### ANSWERS

1.  c
2.  b
3.  a
4.  a
5.  d
6.  c
7.  b
8.  b
9.  c
10.  a

##### ![Exercise](Images/exe.png)EXERCISES

1.  Define the terms: field, record and file.
2.  In how many ways the records can be arranged in a file?
3.  Write an explanatory note on the relationship between files and streams.
4.  What are the different methods of opening a file? Explain in brief.
5.  Differentiate between get() and getline() functions of ifstream class.
6.  How the end of file can be detected? Explain in brief.
7.  Write a program which counts the number of records in a given file.
8.  Give suitable declarations for the file containing components where each component consists of the following information.

    name: 20 characters

    empId: integer type

    netSal: float type

9.  Write a program which creates an exact copy of a given file called Ofile in the form of a new file called Nfile. Choose appropriate component type for this problem.
10.  Write a program which counts the number of times a given alphabet appears in a text file.
11.  Write a program which searches a given file for a record equal to an input value of empId. The component record structure of the file is as given in Question 8.
12.  Write a program which reads a text file called document and generates a table of frequency count of alphabets appearing in the text. The output should be displayed in the following form![image](Images/pg291-1.png)
13.  A product record is given below.

    ![image](Images/pg291-2.png)

    Choose appropriate data types for the fields. Write a program which reads a file of such records and prints them in the following format.

    ![image](Images/pg291-3.png)
14.  Assuming that a text file named ‘book’, already contains some text written into it, write a function named noVowel (), that reads the file ‘book’ and creates a new file named newBook, which shall contain only those words from the file ‘book’ which don’t start with an upper case vowel, i.e. with ‘A’, ‘E’, ‘I’, ‘O’, ‘U’. For example if the file ‘Book’ contains: “One and Only One”. Then the file ‘newBook’ shall contain: “and”.
15.  What is eof? Explain its utility.
16.  Write an interactive menu driven C++ program that creates a text file (say myDoc) and then display the file. Create another text file (say lowDoc) by converting each line of the ‘myDoc’ file into a lowercase string. Display the contents of ‘lowDoc’ file.
17.  Write an interactive menu driven C++ program that creates a text file (say myDoc) and then displays the file. Create another text file (say revDoc) by reversing each line of the ‘myDoc’ file. Display the contents of ‘revDoc’ file.

## 11

## EXCEPTION HANDLING

##### 11.1 INTRODUCTION

When a teacher is in a class, his/her lecture can be disrupted by either of the following two events:

1.  Somebody from outside the class *interrupts* the lecture by knocking on the door. This event is an *asynchronous* event because the teacher has nothing to do with this disruption. At his/her convenience, the teacher suspends his/her lecture and listens to what the visitor has to say.

    This is a situation similar to a device interrupting the CPU for seeking a particular service. The CPU suspends the execution of the current program, saves its context, and jumps to an interrupt service routine.

    There is no specific time for the interrupt to occur. The CPU need not handle the interrupt immediately but only when ...

## 12

## INTRODUCTION TO UML

##### 12.1 INTRODUCTION TO UML

In order to understand a complex problem or system, we need to represent it in a simple way called ‘model’. For example, when a large apartment building in a housing society is built, first its plan is drawn by the architect on a paper and then a small prototype is prepared. When all the stake holders (builder, clients, etc.) agree on the plan and the looks of the prototype, the project gets approved for construction. The prototype is nothing but the model of the proposed building. Similarly, when software is to be constructed, its model needs to be prepared.

A model can be precisely defined as *a hypothetical description of a complex entity or process, constructed to understand a problem or system*.

Once the model is in place, it can be modified for improvement or approved for final construction. However, we need to have necessary tools for the construction of a model. For software modeling, a language is required that can express the various components and the relationship among them. For instance, in object oriented software construction, we need to specify and depict pictorially the components like classes, objects, relationships, hierarchies, etc.

A number of object oriented languages have been proposed by proponents like Rumbaugh, Booch, Jacobson, Coad-Yourdon, etc. Each had its own symbols and specifications for expressing object-oriented programming (OOP) components. In 1994, an effort was started to unify all the methodologies to form a Unified Modeling Language (UML). In 1997, UML 1.0 was offered to the user as a standard OOP modeling language.

UML can be precisely defined as “*a language that models the structural, architectural, and behavioral features of a system*”.

Some important UML diagrams are given below:

1.  Class diagram
2.  Use-case diagram
3.  Behavioral diagrams
    1.  Interaction diagrams
        1.  Sequence diagram
        2.  Collaboration diagram
    2.  State chart diagram
    3.  Activity diagram
4.  Implementation diagrams
    1.  Component diagram
    2.  Deplayment diagram

A model can be of following two types:

*Static model*: A representation of a system at a specific time at rest. It shows the states and parameters of a system at that particular instance in time, e.g. class diagrams.

*Dynamic model*: This model depicts the dynamism of the system in terms of its behaviors over a period of time. In fact it is the collection of procedures that govern the overall behaviour of the system, e.g. UML interaction diagrams.

##### 12.2 CLASS DIAGRAMS (STATIC)

A class symbolizes a specific feature of the system. It can be represented by a rectangle having three sections: name, states (attributes) and behaviours (operations) as shown in [Fig. 12.1](#chapter_12.xhtml_ch12fig1). Where an attribute defines the range of values a state can take, an operation represents the implementation of a service or behaviour of the object that the class represents. The access specifiers can be assigned to various members of the class by prefixing the symbols:– (private), + (public), and # (protected).

![Figure 12.1](Images/ch12-fig01.png)

**Figure 12.1** *A class diagram*

Depending upon requirement, the class diagram can be as short as shown in [Fig. 12.2](#chapter_12.xhtml_ch12fig2)(a) or as detailed as shown in [Fig. 12.2](#chapter_12.xhtml_ch12fig2)(b).

![Figure 12.2](Images/ch12-fig02.png)

**Figure 12.2** *(a, b) Class diagrams*

An object is represented by a similar diagram but its name is qualified by its corresponding class name. An object called ‘studOb’ of type ‘student’ class is shown in [Fig. 12.3](#chapter_12.xhtml_ch12fig3).

![Figure 12.3](Images/ch12-fig03.png)

**Figure 12.3** *An object*

It may noted that the object contains the actual data in contrast to a class which has only attributes names. The reason is simple that class is a compile time entity and the objects are instances of the class created at run time. Therefore, the objects get the memory for storing the data for its states. An *object diagram* is an instance of the class diagram.

#### 12.2.1 Relationships Among Classes

The various relationships that exist between classes are composition, generalizations and dependencies. A brief discussion on each of them is given below:

*Composition*: An object can be composed of components bound by two types of relationships: association and aggregation. Both represent a ‘has-a’ relationship.

*Association*: A loose relationship between two objects in which both the objects are visible. For instance, a computer *has a* mouse. Similarly, a teacher has students to teach. Or other way round, a student has a teacher to be taught by. This type of association is shown by a simple line or link between the participating classes as shown in [Fig. 12.4](#chapter_12.xhtml_ch12fig4).

![Figure 12.4](Images/ch12-fig04.png)

**Figure 12.4** *An association*

This type of relationship is flexible in the sense that different teachers can be associated with different students or vice-versa. As discussed earlier in the book, an association is implemented in C++ as a pointer of one class embedded in other class. For example, the class teacher would contain a pointer of student’s type.

*Aggregation*: A tight relationship between two objects wherein only one object is visible. In fact one object acts as a container of other object and therefore only the container remains visible. For example, a car has an engine. Now we see only the car object and not the engine object. Similarly, CPU is an aggregation of three objects: ALU, CU and registers.

The aggregation is represented by a link with an open diamond at the container class end. Consider the aggregation shown in [Fig. 12.5](#chapter_12.xhtml_ch12fig5) wherein it is shown that a University has department.

![Figure 12.5](Images/ch12-fig05.png)

**Figure 12.5** *The aggregation*

The aggregation is modeled as containership in C++. For the aggregation shown in [Fig. 12.5](#chapter_12.xhtml_ch12fig5), the University class would contain an object of department type.

It may be noted that both association and aggregation are ‘has-a’ relationships. Both have their own advantages. The association provides flexibility in relationship. For example, an optical mouse can be very easily replaced by a wireless mouse in a computer system. On the other hand, the aggregation is an inflexible but more secured relationship. For instance, engine object is very much secured within the car object.

Multiplicity of association can be shown by appropriately annotating the association links as shown in [Fig. 12.6](#chapter_12.xhtml_ch12fig6).

![Figure 12.6](Images/ch12-fig06.png)

**Figure 12.6** *Multiplicity of associations*

Thus the relationship that the University has many departments can be represented by the diagram shown in [Fig. 12.7](#chapter_12.xhtml_ch12fig7).

![Figure 12.7](Images/ch12-fig07.png)

**Figure 12.7** *One to many relationship*

*Generalization*: In this OOP strategy, common elements are identified among the different classes. It follows two approaches: ‘top down’ and ‘bottom up’. In top down approach, we create specialized classes from existing classes. On the other hand, in bottom up approach, from different classes, a super class is created. In both the cases a hierarchy of classes is created with the help of inheritance leading to ‘a kind of’ (ako) relationship. Inheritance is represented by a solid line starting from the derived class with an arrow like triangle pointing to the base class, i.e. the apex of the triangle point to the base class a shown in [Fig. 12.8](#chapter_12.xhtml_ch12fig8).

![Figure 12.8](Images/ch12-fig08.png)

**Figure 12.8** *Inheritance (generalization)*

Consider the hierarchy given in [Fig. 12.9](#chapter_12.xhtml_ch12fig9). From top to down, it can be said that an ‘infrared mouse’ is a kind of ‘wireless mouse’ which itself is a kind of ‘mouse’. In bottom up approach, we can say that wireless mouse is a generalization of ‘infrared mouse’ and ‘radio frequency mouse’.

![Figure 12.9](Images/ch12-fig09.png)

**Figure 12.9** *Hierarchy of classes*

*Dependency*: It is a special relationship between two classes where one class depends upon other class. This relationship is shown as a *dashed directed line* from dependent class to the class on which it depends. Consider the relationship shown in [Fig. 12.10](#chapter_12.xhtml_ch12fig10).

![Figure 12.10](Images/ch12-fig10.png)

**Figure 12.10** *Dependency relationship*

In fact dependency is a relationship of usage of one class by another. For instance, the ‘Tax’ class is using the ‘taxRules’ class. Therefore, it is dependent upon ‘taxRules’ class. On the other hand, two classes are called ‘*orthogonal*’ if they do not depend on each other. If a class is modified then it has no effect on the functioning of the other class.

##### 12.3 USE CASE DIAGRAMS (STATIC)

A system has a boundary surrounded by an environment. The system has some objectives which are achieved through functions or classes called *use cases*. Some entities of the environment called as ‘actors’ interact with the system as shown in [Fig. 12.11](#chapter_12.xhtml_ch12fig11).

![Figure 12.11](Images/ch12-fig11.png)

**Figure 12.11** *A use case diagram*

*A use case diagram is a graph that represents interactions between actors and use cases.* where:

1.  An ‘*actor*’ is an entity or a class that can initiate an action. It is generally not a part of the system or sub-system under consideration. An actor must be appropriately named. For example, in a classroom, the teacher and student are actors. Similarly in a library, the library member, clerk, librarian, etc. are all actors.
2.  A *use case* is a class or a function that provides a service to the system. It describes the interaction between an actor and the system. Each use case realizes the aim of an actor. The name of the use case should be so chosen that it properly represents the functionality of the system.
3.  An edge is a path of communication from an actor to a use case or vice-versa.

Therefore, the following need to be identified before a use case is drawn:

1.  Actors.
2.  Use cases defining what is to be done, i.e. functionality.
3.  Relationships between actors and use cases.

For example, consider the use case diagram of the book issue scenario of a library given in [Fig. 12.12](#chapter_12.xhtml_ch12fig12). It consists of two actors: member and library clerk. The use cases are ‘request a book’, ‘search book’, and ‘issue book’.

It may be noted that the name of a use case indicates about the service it provides and collectively all the use cases realize the objectives of the system.

![Figure 12.12](Images/ch12-fig12.png)

**Figure 12.12** *Use case diagram of book issue scenario*

Similarly, a classroom scenario consists of two actors: ‘teacher’ and ‘student’ and the possible use cases are: ‘write on black board’, ‘deliver lecture’, ‘ask question’, ‘answer question’ and ‘jot down’. The use case diagram for this scenario is given in [Fig. 12.13](#chapter_12.xhtml_ch12fig13).

![Figure 12.13](Images/ch12-fig13.png)

**Figure 12.13** *Use case diagram of a classroom scenario*

In fact, we can say that a use case diagram represents the context of a system. It helps us in understanding the overall behaviour of the system in context of the goals of the actors associated with the system. The usage of a use case diagram can be summarized as given below:

1.  Gather system requirements.
2.  Identify factors that influence the system. The factors can be either internal or external.
3.  Draft a broader view of the system.
4.  Represent the interaction among the actors and the use cases.

##### 12.4 BEHAVIORAL DIAGRAMS (DYNAMIC)

The world around us is dynamic in the sense that it is continuously evolving. After nightlong sleep, whether we wake up or not, the sun rises, the birds chirp, people go to their offices and so on. While driving, the vehicles around us move with different speeds. In a classroom, lots of interactions take place between the teacher and the students. All these examples show that the world is characterized by action and interaction between the world actors. This behavior of the world or a part of the world can be represented by behavioral diagrams.

Interactions between various actors of a system are represented using interaction diagrams. The following steps are carried out before drawing the interaction diagrams:

1.  Identify participating objects.
2.  Find out the object organization.
3.  Identify messages that take place between the objects.
4.  Determine the sequence of messages.

A brief discussion on interaction diagrams is given in the following section.

#### 12.4.1 Interaction Diagrams

An interaction diagram helps us in capturing the behavior of a ‘use case’ scenario. There are two types of interaction diagrams: sequence diagrams and collaborations diagram.

*Sequence diagram*: this diagram shows the interaction between various objects in terms of a time sequence. Each object has a lifeline and the messages it exchanges with other objects are arranged in the order of their occurrence.

In a sequence diagram, objects are placed in horizontal dimension. The lifeline of each object is depicted by a vertical line. Messages or interactions are represented as horizontal arrows as shown in [Fig. 12.14](#chapter_12.xhtml_ch12fig14).

![Figure 12.14](Images/ch12-fig14.png)

**Figure 12.14** *A sequence diagram*

Consider the classroom scenario wherein we have four major objects: teacher, black board, student and notebook. The possible interactions among these objects are shown in the sequence diagram given in [Fig. 12.15](#chapter_12.xhtml_ch12fig15).

![Figure 12.15](Images/ch12-fig15.png)

**Figure 12.15** *Sequence diagram of a classroom scenario*

It may be noted that the vertical line is called the object lifeline. It represents the object’s existence during the interaction. However, this diagram does not represent associations among the participating objects.

*Collaboration diagram*: this diagram shows as to how various objects work together in a particular context to achieve desired outcome. It is a collection of vertices and arcs representing objects and messages respectively. The objects are laid out in an organized manner and the arcs are labeled with the messages they send to each other.

The collaboration diagram for classroom scenario is shown in [Fig. 12.16](#chapter_12.xhtml_ch12fig16).

![Figure 12.16](Images/ch12-fig16.png)

**Figure 12.16** *A classroom scenario*

It may be noted that the arrows indicate the message sent within the given use case. This diagram does not primarily indicate the sequence of messages or events. However, sequence can be depicted by appropriately numbering the messages as shown in [Fig. 12.16](#chapter_12.xhtml_ch12fig16). For instance, ‘Ask question’ is the third message in sequence from a student to a teacher.

Similarly, a collaboration diagram of a sub-section of examination system is given in [Fig. 12.17](#chapter_12.xhtml_ch12fig17).

![Figure 12.17](Images/ch12-fig17.png)

**Figure 12.17** *Collaboration diagram of a sub-section of examination system*

The usage of interaction diagrams can be summarized as given below:

1.  Model the dynamic behaviour of the system.
2.  Represent the message flow of the system.
3.  Represent the interactions among the objects.
4.  Show the object organization of the system.
5.  Show the control flow by structural organization (collaboration diagram).
6.  Show the control flow by time sequence (sequence diagram).

#### 12.4.2 State Chart Diagrams

In a dynamic environment, an object moves from one state to another after the occurrence of an event. The event could be a message, timeout or a signal sent by another object. For example, when the object on the front of a queue gets served and leaves the serving window, the server gives a signal to the object next in the queue to come to the front. This type of dynamic behavior of objects is represented by a state chart diagram. It depicts the sequence of states that an object passes through during its lifetime in response to messages it receives from other objects. A state chart diagram is a directed graph of nodes and edges. The nodes represent states of the objects and the arrows depict transitions among states as shown in [Fig. 12.18](#chapter_12.xhtml_ch12fig18).

![Figure 12.18](Images/ch12-fig18.png)

**Figure 12.18** *State chart diagram*

Therefore, the following needs to be identified before drawing the state chart diagram:

1.  Identify the objects.
2.  Identify the states.
3.  Identify the transitions and the related events.

Consider the state chart diagram shown in [Fig. 12.19](#chapter_12.xhtml_ch12fig19). It illustrates that initially the teacher object is in ‘wait’ state. It polls the status of the students. If the students are present then the teacher goes to ‘teach’ state else the teacher goes back to the ‘wait’ state. The teacher goes to ‘stop’ state from ‘teach’ state as soon as the bell rings.

![Figure 12.19](Images/ch12-fig19.png)

**Figure 12.19** *State chart showing states and transitions*

It may be noted that the conditions that govern the transitions have been placed between the square brackets. The start state is represented by a solid ball whereas the stop state is shown by a solid ball within a circle. It may further be noted that a state chart represents a reactive system wherein the participating objects react to external or internal events. Therefore the objects are also called as *reactive objects*.

If it is needed to branch to many states depending upon different values of conditions then we can use a *choice point* (a circle) as a junction from where the bifurcation begins. A condition is also called a *guard*.

Let us now modify the state chart of [Fig. 12.19](#chapter_12.xhtml_ch12fig19) to include the guard that the teacher goes to the stop state after waiting for 10 minutes for the students. The modified state chart is given in [Fig. 12.20](#chapter_12.xhtml_ch12fig20).

![Figure 12.20](Images/ch12-fig20.png)

**Figure 12.20** *Modified state chart diagram*

The usage of state chart diagrams can be summarized as given below:

1.  To represent the states of objects.
2.  To represent a reactive system.
3.  To represent the events responsible for transitions of objects from one state to another.

#### 12.4.3 Activity Diagrams

An internal action of an object at a particular state is called an activity. Therefore, the activity diagram represents a flow of work inside a use case, an algorithm, a protocol or between objects. The workflow itself is represented as a series of actions. The workflow can be sequential, branched or parallel.

The following needs are to be identified before drawing the activity diagram:

1.  Activities
2.  Association
3.  Conditions
4.  Constraints

An activity diagram is an extension of a flow chart. It is a graph consisting of activities and transitions. An activity is represented as rectangle with round corners and is labeled with the action it performs. As soon as the action is complete, the work flows to the next activity along the transition as shown in [Fig. 12.21](#chapter_12.xhtml_ch12fig21). For instance, as soon as a student is admitted, he/she is assigned a course.

![Figure 12.21](Images/ch12-fig21.png)

**Figure 12.21** *An activity diagram*

An activity can have more than one out going transition. When the workflow follows a transition the internal action of the activity is stopped. The outgoing transitions are resolved through suitable conditions. Let us extend the activity diagram of 12.21 so that the course is only assigned after the fee is deposited by the student. The modified activity diagram is shown in [Fig. 12.22](#chapter_12.xhtml_ch12fig22).

![Figure 12.22](Images/ch12-fig22.png)

**Figure 12.22** *Modified activity diagram*

Let us carry on further to extend the activity diagram by including the activity of calling candidates from the list of candidates till the number of admitted students is equal to 30\. The further modified activity diagram is given in [Fig. 12.23](#chapter_12.xhtml_ch12fig23).

![Figure 12.23](Images/ch12-fig23.png)

**Figure 12.23** *Activity diagram of admitting 30 students for a course*

Concurrent activities can also be depicted by using fork-join construct of UML as shown in [Fig. 12.24](#chapter_12.xhtml_ch12fig24). At ‘Fork’ the workflow splits into more than one workflow and at ‘Join’ all the threads of workflows join to form a single workflow.

![Figure 12.24](Images/ch12-fig24.png)

**Figure 12.24** *Fork- and join-construct for concurrent activities*

For example, after a student has been admitted, the course and hostel can be assigned concurrently as shown in [Fig. 12.25](#chapter_12.xhtml_ch12fig25).

![Figure 12.25](Images/ch12-fig25.png)

**Figure 12.25** *Activity diagram depicting concurrent activities*

The usage of activity diagrams can be summarized as given below:

1.  Represent the workflow of the system.
2.  Represent the sequence of the workflow from one activity to another.
3.  Show the type of workflow: sequential, branched and concurrent.

##### 12.5 IMPLEMENTATION DIAGRAMS

From the name itself, it is obvious that the implementation diagrams represent the implementation aspects of a system. These are of two types: component diagrams and deployment diagrams.

#### 12.5.1 Component Diagram

We know that a system is composed of reusable sub-systems called components. Each component implements a particular service offered by an interface. In the component diagram, the components are connected with each other either by the dependency relationship or the composition relationship.

For instance, a student gets registered with a university through an interface. The interface communicates with the registration module. The registration module stores the registration information in a student database as shown in [Fig. 12.26](#chapter_12.xhtml_ch12fig26).

![Figure 12.26](Images/ch12-fig26.png)

**Figure 12.26** *Component diagram*

Thus, it can be said that “a component diagram represents the components of a system and the relationship among them at an instance of time”. In fact the main purposes of drawing a component diagram are:

1.  Plan and name the components that are going to be the executable parts of the system.
2.  Represent the organization of components in the system visually.

#### 12.5.2 Deployment Diagram

As the name suggests, a deployment diagram *represents the topology of components in terms of their deployment on different nodes.* The nodes in general are computational hardware components like client and server machines, modems, monitors, etc. Therefore, in addition to software components, we need to identify nodes and their relationships. A software component runs on a particular node. Therefore, a node necessarily contains the instance of that component as shown in [Fig. 12.27](#chapter_12.xhtml_ch12fig27).

It may be noted that the node is named as a ‘client m/c’, i.e. client machine. An instance of ‘interface’ component is deployed on this node for execution.

![Figure 12.27](Images/ch12-fig27.png)

**Figure 12.27** *A node containing the instance of ‘interface’ component*

Let us now deploy the various components of [Fig. 12.26](#chapter_12.xhtml_ch12fig26) as per the following choice:

| Component | Node |
| Interface | client m/c |
| Registration | web server |
| Database | Database server |

The corresponding deployment diagram is given in [Fig. 12.28](#chapter_12.xhtml_ch12fig28).

![Figure 12.28](Images/ch12-fig28.png)

**Figure 12.28** *A deployment diagram*

The usage of deployment diagrams can be summarized as given below:

1.  To illustrate the distribution of hardware components called nodes.
2.  To specify the topology of the nodes.
3.  To identify the software components that will reside on the these nodes.

##### 12.6 SUMMARY

A model is a simplified representation of a system, created for the purpose of understanding the system. For software modeling, UML (unified modeling language) is used. A model can be static or dynamic. A class represents a specific feature of a system. An object is also represented by a rectangle but its name is qualified by its class name. A composition represents a ‘has-a’ relationship. Association is modeled as a pointer from one class to another. Aggregation is modeled as containership. Top down approach identifies specialization in classes. Bottom up approach creates super classes. Inheritance models ‘ako’ relationship. Dependency is the relationship of usage of one class by another. An actor is a class that initiates some action. A use case diagram represents the context of a system. An object moves from one state to another after the occurrence of an event. A state chart represents a reactive system. An activity can have more than one outgoing transition. Implementation diagrams are of two types: component and deployment.

##### ![question](Images/question.png)MULTIPLE CHOICE QUESTIONS

1.  A static model represents a system at:
    1.  motion
    2.  rest
2.  A class is represented as a ________ in UML.
    1.  circle
    2.  ellipse
    3.  rectangle
    4.  triangle
3.  An attribute defines a range of values for a:
    1.  state
    2.  object
    3.  class
    4.  function
4.  An object diagram is ______ of a class diagram.
    1.  a copy
    2.  opposite
    3.  instance
5.  An association is _________ relationship.
    1.  loose
    2.  tight
    3.  secured
6.  In containership only the _______ is visible.
    1.  relationship
    2.  link
    3.  contained object
    4.  container
7.  The aggregation is represented by a link with an open ______ at the container class end.
    1.  circle
    2.  ellipse
    3.  arrow
    4.  diamond
8.  Orthogonal classes do not ________ each other.
    1.  depend on
    2.  touch
    3.  inherit
    4.  associate with
9.  A use case is a class or a function that provides a ______ to the system.
    1.  link
    2.  state
    3.  service
    4.  name
10.  Messages in a sequence diagram are arranged in the order of their:
    1.  placement
    2.  occurrence
11.  Interaction diagrams model the ______ behaviour of the system.
    1.  primary
    2.  static
    3.  dynamic
    4.  optimal
12.  In a state chart diagram, an arrow represents a:
    1.  transition
    2.  state
    3.  event
    4.  object
13.  An internal action of an object at a particular state is called:
    1.  impulse
    2.  provocation
    3.  activity
    4.  reaction
14.  An activity diagram is an extension of a:
    1.  class diagram
    2.  object diagram
    3.  sequence diagram
    4.  flowchart
15.  A deployment diagram represents the __________ of components.
    1.  interaction
    2.  ordering
    3.  topology
    4.  relationship

##### ANSWERS

1.  b
2.  c
3.  a
4.  c
5.  a
6.  d
7.  d
8.  a
9.  c
10.  b
11.  c
12.  a
13.  c
14.  d
15.  d

##### ![Exercise](Images/exe.png)EXERCISES

1.  What is a model? Differentiate between static and dynamic models.
2.  What is UML? Explain in brief.
3.  How a class is represented in UML?
4.  How member access specifiers are represented in a UML class diagram?
5.  What is an object diagram?
6.  How aggregation, association and inheritance are represented in a UML class diagram?
7.  Draw the use case diagram of a Super Bazaar billing window scenario wherein the customers get the bill for the items purchased by them and making the payment in cash.
8.  Draw the use case diagram of an examination room scenario?
9.  Give the equivalent sequence diagram of the use case developed for examination room scenario.
10.  Draw the use case for an ATM machine wherein a customer withdraws cash by presenting the ATM card to the machine.
11.  Give the state chart diagram for the use case diagram developed for ATM machine.
12.  Differentiate between a sequence and collaboration diagrams.
13.  Give the activity diagram for use case developed for Super Bazaar billing window in Question 7.
14.  Explain component diagrams with the help of examples.
15.  Explain deployment diagrams with the help of examples.

## 13

## POLYMORPHISM: A REVIEW

##### 13.1 POLYMORPHISM

We have already introduced ourselves with ‘polymorphism’ in [Section 5.1](#chapter_05.xhtml_ch1) wherein it was defined as an entity or object having two or more forms. In object-oriented programming (OOP), functions and operators can be overloaded to achieve polymorphic behaviour.

Polymorphic functions have one name with different implementations. If the functions belong to different classes then a message (say ‘close’) can be interpreted differently by different objects resulting in different responses as shown in [Fig. 13.1](#chapter_13.xhtml_ch13fig1).

![Figure 13.1](Images/ch13-fig01.png)

**Figure 13.1** *Polymorphic behaviour of objects*

##### 13.2 TAXONOMY OF POLYMORPHISM

Cardelli and Wegner gave ...

## APPENDIX
TURBO C++ KEYWORDS

The turbo C++ keywords are listed below:

asm

auto

break

case

catch

_cdecl

cdecl

char

class

const

continue

_cs

default

do

double

_ds

else

enum

_es

_export

extern

_far

far

fl oat

for

friend

goto

huge

if

inline

int

interrupt

_loadds

long

_near

near

new

opeator

_pascal

pascal

private

protected

public

register

return

_saveregs

_seg

short

signed

sizeof

_ss

static

struct

switch

template

this

typedef

union

unsigned

virtual

void

volatile

while

## **Index**

& Operator, [59](#chapter_02.xhtml_page_59)

* Operator, [60](#chapter_02.xhtml_page_60)

‘\a’ (Alert), [11](#chapter_01.xhtml_page_11)

‘\b’ (Backspace), [11](#chapter_01.xhtml_page_11)

‘\n’ (new line), [11](#chapter_01.xhtml_page_11)

‘\t’ (Tab), [10](#chapter_01.xhtml_page_10)

##### A

Abstract class, [221](#chapter_07.xhtml_page_221)

Abstraction, [112](#chapter_04.xhtml_page_112)

Activity diagrams, [322](#chapter_12.xhtml_page_322)

Actor, [316](#chapter_12.xhtml_page_316)

Ad Hocpolymorphism, [330](#chapter_13.xhtml_page_330)

a kind of (AKO) relationship, [206](#chapter_07.xhtml_page_206)

Arithmetic assignment operators, [255](#chapter_09.xhtml_page_255)

Arithmetic operators, [12](#chapter_01.xhtml_page_12)

Arrays, [31](#chapter_01.xhtml_page_31)

initialization, [35](#chapter_01.xhtml_page_35), [38](#chapter_01.xhtml_page_38)

One-dimensional, [31](#chapter_01.xhtml_page_31), [32](#chapter_01.xhtml_page_32)

Multi-dimensional, [33](#chapter_01.xhtml_page_33)

parameters, [45](#chapter_01.xhtml_page_45)

Arrays of structures, [38](#chapter_01.xhtml_page_38)

Array of objects, [119](#chapter_04.xhtml_page_119)

arrow operator, [74](#chapter_02.xhtml_page_74)

Assignment operator, [18](#chapter_01.xhtml_page_18)

atexit(), [294](#chapter_11.xhtml_page_294)

##### B

Backslash character constants, [9](#chapter_01.xhtml_page_9)

base class, [206](#chapter_07.xhtml_page_206)

Basic data types, [2](#chapter_01.xhtml_page_2)

Behavioral diagrams, [318](#chapter_12.xhtml_page_318)

Binary file, [264](#chapter_10.xhtml_page_264)

Binary operators, [250](#chapter_09.xhtml_page_250)

break, [23](#chapter_01.xhtml_page_23)

break’ and ‘continue’ statements, [29](#chapter_01.xhtml_page_29)

##### C

Call by Reference, [44](#chapter_01.xhtml_page_44)

Call by Value, [42](#chapter_01.xhtml_page_42)–[44](#chapter_01.xhtml_page_44)

catch block, [296](#chapter_11.xhtml_page_296)

Character ...