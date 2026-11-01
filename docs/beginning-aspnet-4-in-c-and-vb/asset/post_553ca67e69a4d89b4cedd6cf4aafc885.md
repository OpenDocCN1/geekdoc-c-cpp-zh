
## PART I

## The C# Language

- CHAPTER 1: .NET Architecture
- CHAPTER 2: Core C#
- CHAPTER 3: Objects and Types
- CHAPTER 4: Inheritance
- CHAPTER 5: Generics
- CHAPTER 6: Arrays and Tuples
- CHAPTER 7: Operators and Casts
- CHAPTER 8: Delegates, Lambdas, and Events
- CHAPTER 9: Strings and Regular Expressions
- CHAPTER 10: Collections
- CHAPTER 11: Language Integrated Query
- CHAPTER 12: Dynamic Language Extensions
- CHAPTER 13: Memory Management and Pointers
- CHAPTER 14: Reflection
- CHAPTER 15: Errors and Exceptions

## .NET Architecture

### WHAT'S IN THIS CHAPTER?

- Compiling and running code that targets .NET
- Advantages of Microsoft Intermediate Language (MSIL)
- Value and reference types
- Data typing
- Understanding error handling and attributes
- Assemblies, .NET base classes, and namespaces

Throughout this book, we emphasize that the C# language must be considered in parallel with the .NET Framework, rather than viewed in isolation. The C# compiler specifically targets .NET, which means that all code written in C# will always run within the .NET Framework. This has two important consequences for the C# language:

- 1. The architecture and methodologies of C# reflect the underlying methodologies of .NET.
- 2. In many cases, specific language features of C# actually depend on features of .NET, or of the .NET base classes.

Because of this dependence, it is important to gain some understanding of the architecture and methodology of .NET before you begin C# programming. That is the purpose of this chapter.

### THE RELATIONSHIP OF C# TO .NET

C# is a relatively new programming language and is significant in two respects:

- It is specifically designed and targeted for use with Microsoft's .NET Framework (a feature-rich platform for the development, deployment, and execution of distributed applications).
- It is a language based on the modern object-oriented design methodology, and, when designing it, Microsoft learned from the experience of all the other similar languages that have been around since object-oriented principles came to prominence some 20 years ago.

One important thing to make clear is that C# is a language in its own right. Although it is designed to generate code that targets the .NET environment, it is not itself part of .NET. Some features are supported by .NET but not by C#, and you might be surprised to learn that some features of the C# language are not supported by .NET (for example, some instances of operator overloading)!

However, because the C# language is intended for use with .NET, it is important for you to have an understanding of this Framework if you want to develop applications in C# effectively. Therefore, this chapter takes some time to peek underneath the surface of .NET. Let's get started.

### THE COMMON LANGUAGE RUNTIME

Central to the .NET Framework is its runtime execution environment, known as the Common Language Runtime (CLR) or the .NET runtime. Code running under the control of the CLR is often termed managed code.

However, before it can be executed by the CLR, any source code that you develop (in C# or some other language) needs to be compiled. Compilation occurs in two steps in .NET:

- 1. Compilation of source code to Microsoft Intermediate Language (IL).
- 2. Compilation of IL to platform-specific code by the CLR.

This two-stage compilation process is very important, because the existence of the Microsoft Intermediate Language is the key to providing many of the benefits of .NET.

IL shares with Java byte code the idea that it is a low-level language with a simple syntax (based on numeric codes rather than text), which can be very quickly translated into native machine code. Having this well-defined universal syntax for code has significant advantages: platform independence, performance improvement, and language interoperability.

### Platform Independence

First, platform independence means that the same file containing byte code instructions can be placed on any platform; at runtime, the final stage of compilation can then be easily accomplished so that the code will run on that particular platform. In other words, by compiling to IL you obtain platform independence for .NET, in much the same way as compiling to Java byte code gives Java platform independence.

Note that the platform independence of .NET is only theoretical at present because, at the time of writing, a complete implementation of .NET is available only for Windows. However, a partial implementation is available (see, for example, the Mono project, an effort to create an open source implementation of .NET, at www.go-mono.com).

### Performance Improvement

Although we previously made comparisons with Java, IL is actually a bit more ambitious than Java byte code. IL is always Just-in-Time compiled (known as JIT compilation), whereas Java byte code was often interpreted. One of the disadvantages of Java was that, on execution, the process of translating from Java byte code to native executable resulted in a loss of performance (with the exception of more recent cases, where Java is JIT compiled on certain platforms).

Instead of compiling the entire application in one go (which could lead to a slow startup time), the JIT compiler simply compiles each portion of code as it is called (just in time). When code has been compiled once, the resultant native executable is stored until the application exits so that it does not need to be recompiled the next time that portion of code is run. Microsoft argues that this process is more efficient than compiling the entire application code at the start, because of the likelihood that large portions of any application code will not actually be executed in any given run. Using the JIT compiler, such code will never be compiled.

This explains why we can expect that execution of managed IL code will be almost as fast as executing native machine code. What it does not explain is why Microsoft expects that we will get a performance improvement. The reason given for this is that, because the final stage of compilation takes place at runtime, the JIT compiler will know exactly what processor type the program will run on. This means that it can optimize the final executable code to take advantage of any features or particular machine code instructions offered by that particular processor.

Traditional compilers will optimize the code, but they can only perform optimizations that are independent of the particular processor that the code will run on. This is because traditional compilers compile to native executable code before the software is shipped. This means that the compiler does not know what type of processor the code will run on beyond basic generalities, such as that it will be an x86-compatible processor or an Alpha processor.

### Language Interoperability

The use of IL not only enables platform independence, it also facilitates language interoperability. Simply put, you can compile to IL from one language, and this compiled code should then be interoperable with code that has been compiled to IL from another language.

You are probably now wondering which languages aside from C# are interoperable with .NET; the following sections briefly discuss how some of the other common languages fit into .NET.

### Visual Basic 2010

Visual Basic .NET 2002 underwent a complete revamp from Visual Basic 6 to bring it up to date with the first version of the .NET Framework. The Visual Basic language itself had dramatically evolved from VB6, and this meant that VB6 was not a suitable language for running .NET programs. For example, VB6 is heavily integrated into Component Object Model (COM) and works by exposing only event handlers as source code to the developer — most of the background code is not available as source code. Not only that, it does not support implementation inheritance, and the standard data types that Visual Basic 6 uses are incompatible with .NET.

Visual Basic 6 was upgraded to Visual Basic .NET in 2002, and the changes that were made to the language are so extensive you might as well regard Visual Basic as a new language. Existing Visual Basic 6 code does not compile to the present Visual Basic 2010 code (or to Visual Basic .NET 2002, 2003, 2005, and 2008 for that matter). Converting a Visual Basic 6 program to Visual Basic 2010 requires extensive changes to the code. However, Visual Studio 2010 (the upgrade of Visual Studio for use with .NET) can do most of the changes for you. If you attempt to read a Visual Basic 6 project into Visual Studio 2010, it will upgrade the project for you, which means that it will rewrite the Visual Basic 6 source code into Visual Basic 2010 source code. Although this means that the work involved for you is heavily cut down, you will need to check through the new Visual Basic 2010 code to make sure that the project still works as intended because the conversion might not be perfect.

One side effect of this language upgrade is that it is no longer possible to compile Visual Basic 2010 to native executable code. Visual Basic 2010 compiles only to IL, just as C# does. If you need to continue coding in Visual Basic 6, you can do so, but the executable code produced will completely ignore the .NET Framework, and you will need to keep Visual Studio 6 installed if you want to continue to work in this developer environment.

### Visual C++ 2010

Visual C++ 6 already had a large number of Microsoft-specific extensions on Windows. With Visual C++ .NET, extensions have been added to support the .NET Framework. This means that existing C++ source code will continue to compile to native executable code without modification. It also means, however,
