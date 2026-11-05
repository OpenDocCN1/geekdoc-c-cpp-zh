
## C#
PROGRAMMING
BEGINNERS

## LEARN IN 1 DAY

![](img/8115a2172ef67838d7fe1933fc517c4d_0_0.png)

## C# for Beginners: Learn in 1 Day

By Krishna Rungta

Copyright 2016 - All Rights Reserved – Krishna Rungta

**ALL RIGHTS RESERVED.** No part of this publication may be reproduced or transmitted in any form whatsoever, electronic, or mechanical, including photocopying, recording, or by any informational storage or retrieval system without express written, dated and signed permission from the author.

## Table of Contents

## Chapter 1: What is .NET Framework
- 1. What is the .NET Framework
- 2. Different versions of the .Net framework

## Chapter 2: Download and Install Visual Studio

## Chapter 3: Data Types
- 1. Building the first console application
- 2. Basic Data Types
- 3. Enumeration
- 4. Variables and Operators
- 5. Flow Control and conditional statements
- 6. Arrays

## Chapter 4: Class and Object
- 1. What are classes and objects
- 2. Fields and methods
- 3. Access Modifiers
- 4. Constructors
- 5. Inheritance
- 6. Polymorphism
- 7. Abstract classes
- 8. Interfaces

## Chapter 5: Collections
- 1. ArrayList
- 2. Stack
- 3. Queues
- 4. Hashtable

## Chapter 6: Windows Forms Application
- 1. Windows Forms Basics
- 2. Hello World in Windows Forms
- 3. Adding Controls to a form
- 4. Event Handling for Controls
- 5. Other Controls

## Chapter 7: Database Access
- 1. Fundamentals of Database connectivity
- 2. Connections in .Net
- 3. Accessing data
- 4. Inserting Records
- 5. Updating Records
- 6. Deleting Records
- 7. Connecting Controls to Data
- 8. Using DataGrids

## Chapter 8: File Operations
- 1. Basic File I/O Commands
- 2. Streams – Reading and Writing to files
- 3. Serialization

## Chapter 1: What is .NET Framework

The .Net framework is a software development platform developed by Microsoft. The framework was meant to create applications, which would run on the Windows Platform. The first version of the .Net framework was released in the year 2000.

The version was called .Net framework 1.0. The .Net framework has come a long way since then, and the current version is 4.6.1.

The .Net framework can be used to create both - **Form based** and **Web based** applications. Web services can also be developed using the .Net framework.

The framework also supports various programming languages such as Visual Basic and C#. So developers can choose and select the language to develop the required application. In this chapter, you will learn some basics of the .Net framework.

### .Net Framework Architecture

The basic architecture of the .Net framework is as shown below.

![](img/8115a2172ef67838d7fe1933fc517c4d_5_0.png)

The architecture of the .Net framework is based on the following key components;

- 1. **Common Language Runtime** - The “Common Language Infrastructure” or CLI is a platform on which the .Net programs are executed.

The CLI has the following key features:

- **Exception Handling** - Exceptions are errors which occur when the application is executed.

Examples of exceptions are:
- If an application tries to open a file on the local machine, but the file is not present.
- If the application tries to fetch some records from a database, but the connection to the database is not valid.

- **Garbage Collection** - Garbage collection is the process of removing unwanted resources when they are no longer required.

Examples of garbage collection are:
- A File handle which is no longer required. If the application has finished all operations on a file, then the file handle may no longer be required.
- The database connection is no longer required. If the application has finished all operations on a database, then the database connection may no longer be required.

### Working with Various programming languages

As noted in an earlier section, a developer can develop an application in a variety of .Net programming languages.

- 1. **Language** - The first level is the programming language itself, the most common ones are VB.Net and C#.
- 2. **Compiler** – There is a compiler which will be separate for each programming language. So underlying the VB.Net language, there will be a separate VB.Net compiler. Similarly for C#, you will have another compiler.
- 3. **Common Language Interpreter** – This is the final layer in .Net which would be used to run a .net program developed in any programming language. So the subsequent compiler will send the program to the CLI layer to run the .Net application.

![](img/8115a2172ef67838d7fe1933fc517c4d_6_0.png)

- 2. **Class Library** - The .NET Framework includes a set of standard class libraries. A class library is a collection of methods and functions that can be used for the core purpose.

For example, there is a class library with methods to handle all file level operations. So there is a method which can be used to read the text from a file. Similarly, there is a method to write text to a file.

Most of the methods are split into either the System.* or Microsoft.* namespaces. (The asterisk * just means a reference to all of the methods that fall under the System or Microsoft namespace)

A namespace is a logical separation of methods. We will learn these namespaces more in detail in the subsequent chapters.

- 3. **Languages** - The types of applications that can be built in the .Net framework are classified broadly into the following categories.

- **WinForms** – This is used for developing Forms-based applications, which would run on an end user machine. Notepad is an example of a client-based application.
- **ASP.Net** – This is used for developing web based applications, which are made to run on any browser such as Internet Explorer, Chrome or Firefox.
  - The Web application would be processed on a server, which would have Internet Information Services Installed.
  - Internet Information Services or IIS is a Microsoft component which is used to execute an ASP.net application.
  - The result of the execution is then sent to the client machines, and the output is shown in the browser.
- **ADO.Net** – This technology is used to develop applications to interact with Databases such as Oracle or Microsoft SQL Server.

### Different versions of the .Net framework

Below is the table of .Net framework versions, which have been released with their release dates. Every version has relevant changes to the framework.

For example, in framework 3.5 and onwards a key framework called the **Entity framework** was released. This framework is used to change the approach in which the applications are developed while working with databases.

| Version number | CLR version | Release date |
|---|---|---|
| 1.0 | 1.0 | 2002-02-13 |
| 1.1 | 1.1 | 2003-04-24 |
| 2.0 | 2.0 | 2005-11-07 |
| 3.0 | 2.0 | 2006-11-06 |
| 3.5 | 2.0 | 2007-11-19 |
| 4.0 | 4 | 2010-04-12 |
| 4.5 | 4 | 2012-08-15 |
| 4.5.1 | 4 | 2013-10-17 |
| 4.5.2 | 4 | 2014-05-05 |
| 4.6 | 4 | 2015-07-20 |
| 4.6.1 | 4 | 2015-11-17 |

The biggest advantage of the .Net framework is that it supports Windows platform. Almost everyone works with Windows machines.

Microsoft always ensures that .Net frameworks are in compliance with all the supported Windows operating systems.

The following design principles of the .Net framework is what makes it very relevant to create .Net based applications.

- 1. **Interoperability** - The .Net framework provides a lot of backward support. Suppose if you had an application built on an older version of the .Net framework, say 2.0. And if you tried to run the same application on a machine which had the higher version of the .Net framework, say 3.5. The application would still work. This is because with every release, Microsoft ensures that older framework versions gel well with the latest version.
- 2. **Portability** - Applications built on the .Net framework can be made to work on any Windows platform. And now in recent times, Microsoft is also envisioning to make Microsoft products work on other platforms, such as iOS and Linux.
