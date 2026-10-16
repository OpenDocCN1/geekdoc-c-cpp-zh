
## OBJECT ORIENTED PROGRAMMING WITH C++

FOURTH EDITION

E Balagurusamy  
Member  
Union Public Service Commission  
New Delhi

![](img/58ab8f034e2127e80560390a921c2523_1_0.png)

![](img/58ab8f034e2127e80560390a921c2523_5_0.png)

Tata McGraw-Hill Publishing Company Limited
NEW DELHI

McGraw-Hill Offices

New Delhi  New York  St Louis  San Francisco  Auckland  Bogotá  Caracas  
Kuala Lumpur  Lisbon  London  Madrid  Mexico City  Milan  Montreal  
San Juan  Santiago  Singapore  Sydney  Tokyo  Toronto

Tata McGraw-Hill

Published by Tata McGraw-Hill Publishing Company Limited,
7 West Patel Nagar, New Delhi 110 008.

Copyright © 2008, 2006, 2001, 1994, by Tata McGraw-Hill Publishing Company Limited.
No part of this publication may be reproduced or distributed in any form or by any means, electronic, mechanical, photocopying, recording, or otherwise or stored in a database or retrieval system without the prior written permission of the publishers. The program listings (if any) may be entered, stored and executed in a computer system, but they may not be reproduced for publication.

Fourth reprint 2008
DQLCRDRXRAZXB

This edition can be exported from India only by the publishers,
Tata McGraw-Hill Publishing Company Limited.

ISBN (13 digits): 978-0-07-066907-9
ISBN (10 digits): 0-07-066907-4

Managing Director: Ajay Shukla

General Manager: Publishing—SEM & Tech Ed: Vibha Mahajan
Sponsoring Editor: Shalini Jha
Jr. Sponsoring Editor: Nilanjan Chakravarty
Senior Copy Editor: Dipika Dey
Senior Production Manager: P L Pandita

General Manager: Marketing—Higher Education & School: Michael J. Cruz
Product Manager: SEM & Tech Ed: Biju Ganesan

Controller—Production: Rajender P Ghansela
Asst. General Manager—Production: B L Dogra

Information contained in this work has been obtained by Tata McGraw-Hill, from sources believed to be reliable. However, neither Tata McGraw-Hill nor its authors guarantee the accuracy or completeness of any information published herein, and neither Tata McGraw-Hill nor its authors shall be responsible for any errors, omissions, or damages arising out of use of this information. This work is published with the understanding that Tata McGraw-Hill and its authors are supplying information but are not attempting to render engineering or other professional services. If such services are required, the assistance of an appropriate professional should be sought.

Typeset at Script Makers, 19, A1-B, DDA Market, Paschim Vihar, New Delhi 110 063, and printed at Gopsons, A-2 & 3, Sector 64, Noida - 201 301

Cover: Gopsons

## Contents

- Preface xiii

### 1. Principles of Object-Oriented Programming 1

- 1.1 Software Crisis 1
- 1.2 Software Evolution 3
- 1.3 A Look at Procedure-Oriented Programming 4
- 1.4 Object-Oriented Programming Paradigm 6
- 1.5 Basic Concepts of Object-Oriented Programming 7
- 1.6 Benefits of OOP 12
- 1.7 Object-Oriented Languages 13
- 1.8 Applications of OOP 14
- Summary 15
- Review Questions 17

### 2. Beginning with C++ 19

- 2.1 What is C++? 19
- 2.2 Applications of C++ 20
- 2.3 A Simple C++ Program 20
- 2.4 More C++ Statements 25
- 2.5 An Example with Class 28
- 2.6 Structure of C++ Program 29
- 2.7 Creating the Source File 30
- 2.8 Compiling and Linking 30
- Summary 31
- Review Questions 32
- Debugging Exercises 33
- Programming Exercises 34

### 3. Tokens, Expressions and Control Structures 35

- 3.1 Introduction 35
- 3.2 Tokens 36
- 3.3 Keywords 36
- 3.4 Identifiers and Constants 36
- 3.5 Basic Data Types 38
- 3.6 User-Defined Data Types 40
- 3.7 Derived Data Types 42
- 3.8 Symbolic Constants 43
- 3.9 Type Compatibility 45
- 3.10 Declaration of Variables 45
- 3.11 Dynamic Initialization of Variables 46
- 3.12 Reference Variables 47
- 3.13 Operators in C++ 49
- 3.14 Scope Resolution Operator 50
- 3.15 Member Dereferencing Operators 52
- 3.16 Memory Management Operators 52
- 3.17 Manipulators 55
- 3.18 Type Cast Operator 57
- 3.19 Expressions and their Types 58
- 3.20 Special Assignment Expressions 60
- 3.21 Implicit Conversions 61
- 3.22 Operator Overloading 63
- 3.23 Operator Precedence 63
- 3.24 Control Structures 64
- Summary 69
- Review Questions 71
- Debugging Exercises 72
- Programming Exercises 75

### 4. Functions in C++ 77

- 4.1 Introduction 77
- 4.2 The Main Function 78
- 4.3 Function Prototyping 79
- 4.4 Call by Reference 81
- 4.5 Return by Reference 82
- 4.6 Inline Functions 82
- 4.7 Default Arguments 84
- 4.8 const Arguments 87
- 4.9 Function Overloading 87
- 4.10 Friend and Virtual Functions 89
- 4.11 Math Library Functions 90
- Summary 90
- Review Questions 92
- Debugging Exercises 93
- Programming Exercises 95

### 5. Classes and Objects 96

- 5.1 Introduction 96
- 5.2 C Structures Revisited 97
- 5.3 Specifying a Class 99

- 7.5 Overloading Binary Operators Using Friends 179
- 7.6 Manipulation of Strings Using Operators 183
- 7.7 Rules for Overloading Operators 186
- 7.8 Type Conversions 187
- Summary 195
- Review Questions 196
- Debugging Exercises 197
- Programming Exercises 200

### 8. Inheritance: Extending Classes 201

- 8.1 Introduction 201
- 8.2 Defining Derived Classes 202
- 8.3 Single Inheritance 204
- 8.4 Making a Private Member Inheritable 210
- 8.5 Multilevel Inheritance 213
- 8.6 Multiple Inheritance 218
- 8.7 Hierarchical Inheritance 224
- 8.8 Hybrid Inheritance 225
- 8.9 Virtual Base Classes 228
- 8.10 Abstract Classes 232
- 8.11 Constructors in Derived Classes 232
- 8.12 Member Classes: Nesting of Classes 240
- Summary 241
- Review Questions 243
- Debugging Exercises 243
- Programming Exercises 248

### 9. Pointers, Virtual Functions and Polymorphism 251

- 9.1 Introduction 251
- 9.2 Pointers 253
- 9.3 Pointers to Objects 265
- 9.4 this Pointer 270
- 9.5 Pointers to Derived Classes 273
- 9.6 Virtual Functions 275
- 9.7 Pure Virtual Functions 281
- Summary 282
- Review Questions 283
- Debugging Exercises 284
- Programming Exercises 289

### 10. Managing Console I/O Operations 290

- 10.1 Introduction 290
- 10.2 C++ Streams 291
- 10.3 C++ Stream Classes 292
- 10.4 Unformatted I/O Operations 292
- 10.5 Formatted Console I/O Operations 301
- 10.6 Managing Output with Manipulators 312
- Summary 317
- Review Questions 319
- Debugging Exercises 320
- Programming Exercises 321

### 11. Working with Files 323

- 11.1 Introduction 323
- 11.2 Classes for File Stream Operations 325
- 11.3 Opening and Closing a File 325
- 11.4 Detecting end-of-file 334
- 11.5 More about Open(): File Modes 334
- 11.6 File Pointers and Their Manipulations 335
- 11.7 Sequential Input and Output Operations 338
- 11.8 Updating a File: Random Access 343
- 11.9 Error Handling During File Operations 348
- 11.10 Command-line Arguments 350
- Summary 353
- Review Questions 355
- Debugging Exercises 356
- Programming Exercises 358

### 12. Templates 359

- 12.1 Introduction 359
- 12.2 Class Templates 360
- 12.3 Class Templates with Multiple Parameters 365
- 12.4 Function Templates 366
- 12.5 Function Templates with Multiple Parameters 371
- 12.6 Overloading of Template Functions 372
- 12.7 Member Function Templates 373
- 12.8 Non-Type Template Arguments 374
- Summary 375
- Review Questions 376
- Debugging Exercises 377
- Programming Exercises 379

### 13. Exception Handling 380

- 13.1 Introduction 380
- 13.2 Basics of Exception Handling 381
