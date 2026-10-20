
- 4.1.1 C# Hello World 167
- 4.1.2 Adding Controls to a Form 175
- 4.1.3 Group Box 175
- 4.1.4 Label Control 178
- 4.1.5 TextBox 181
- 4.1.6 ListBox 183
- 4.1.7 RadioButton 185
- 4.1.8 CheckBox 188
- 4.1.9 Button 190
- 4.2 C# Event Handling for Controls 192
- 4.3 Tree and PictureBox Control 197
- 4.3.1 PictureBox Control 201
- 4.4 Web Services 203
- 4.5 ADO.NET Architecture 204
- 4.5.1 C# Database Connection: How to connect SQL Server (Example:) 208
- 4.6 SQL Command in C# 210
- 4.7 Distributed Applications 250
- 4.7.1 Evolution of Distributed Applications 251
- 4.8 What is Globalization? 254
- 4.9 Authentication in ASP.NET 258

## PROGRAMS/PROJECTS

- PROGRAM 1 274
- PROGRAM 2 277
- PROGRAM 3 279
- PROGRAM 4 281
- PROGRAM 5 283
- PROGRAM 6 286
- PROGRAM 7 292
- PROGRAM 8 295
- PROGRAM 9 298
- PROGRAM 10 309
- PROGRAM 11 312
- PROGRAM 12 317
- PROGRAM 13 330

## CHAPTER 1

### INTRODUCTION TO .NET FRAMEWORK

.NET is a software framework which is designed and developed by Microsoft. The first version of the .NET Framework was 1.0 which came in the year 2002. In easy words, it is a virtual machine for compiling and executing programs written in different languages like C#, VB.NET etc. It is used to develop Form-based applications, Web-based applications, and Web services. There is a variety of programming languages available on the .NET platform, VB.NET and C# being the most common ones. It is used to build applications for Windows, phone, web, etc. It provides a lot of functionalities and also supports industry standards. .NET Framework supports more than 60 programming languages in which 11 programming languages are designed and developed by Microsoft. The remaining Non-Microsoft Languages which are supported by .NET Framework but not designed and developed by Microsoft.

### 1.1 Common Language Runtime (CLR):

CLR is the basic and Virtual Machine component of the .NET Framework. It is the run-time environment in the .NET Framework that runs the codes and helps in making the development process easier by providing the various services such as remoting, thread management, type-safety, memory management, robustness, etc. Basically, it is responsible for managing the execution of .NET programs regardless of any .NET programming language. It also helps in the management of code, as code that targets the runtime is known as the Managed Code and code doesn’t target to runtime is known as Unmanaged code.

Framework Class Library (FCL): It is the collection of reusable, object-oriented class libraries and methods, etc that can be integrated with CLR. Also called the Assemblies. It is just like the header files in C/C++ and packages in Java. Installing .NET Framework basically is the installation of CLR and FCL into the system. Below is the overview of .NET Framework.

Is .NET application platform dependent or platform independent?

![](img/e7ca4af023a4148a909dd82c11f81893_15_0.png)
Figure 1.1 Framework

The combination of Operating System Architecture and CPU Architecture is known as the platform. Platform dependent means the programming language code will run only on particular Operating System. A .NET application is platform dependent because of the .NET Framework which is only able to run on the Windows-based operating system. The .NET application is platform independent also because of Mono framework.

Using Mono framework the .NET application can run on any Operating System including Windows. Mono framework is a third party software developed by Novell Company which is now a part of Micro Focus Company. It is a paid framework.

Event-driven programming focuses on events. Eventually, the flow of program depends upon events. Until now, we were dealing with either sequential or parallel execution model but the model having the concept of event-driven programming is called asynchronous model. Event-driven programming depends upon an event loop that is always listening for the new incoming events. The working of event-driven programming is dependent upon events. Once an event loops, then events decide what to execute and in what order. Following flowchart will help you understand how this works:

![](img/e7ca4af023a4148a909dd82c11f81893_17_0.png)
Figure 1.2. .NET Architecture

The basic architecture of the .NET Framework is as shown below:

![](img/e7ca4af023a4148a909dd82c11f81893_17_1.png)

- The database connection is no longer required. If the application has finished all operations on a database, then the database connection may no longer be required.

### Working with Various programming languages –

As noted in an earlier section, a developer can develop an application in a variety of .NET programming languages.

- **Language -** The first level is the programming language itself, the most common ones are VB.NET and C#.
- **Compiler –** There is a compiler which will be separate for each programming language. So underlying the VB.NET language, there will be a separate VB.NET compiler. Similarly, for C#, you will have another compiler.
- **Common Language Interpreter –** This is the final layer in .NET which would be used to run a .NET program developed in any programming language. So the subsequent compiler will send the program to the CLI layer to run the .NET application.

![](img/e7ca4af023a4148a909dd82c11f81893_20_0.png)

### 1. Class Library

The .NET Framework includes a set of standard class libraries. A class library is a collection of methods and functions that can be used for the core purpose. For example, there is a class library with methods to handle all file-level operations. So there is a method which can be used to read the text from a file. Similarly, there is a method to write text to a file.

Most of the methods are split into either the System.\* or Microsoft.\* namespaces. (The asterisk \* just means a reference to all of the methods that fall under the System or Microsoft namespace). A namespace is a logical separation of methods. We will learn these namespaces more in detail in the subsequent chapters.
