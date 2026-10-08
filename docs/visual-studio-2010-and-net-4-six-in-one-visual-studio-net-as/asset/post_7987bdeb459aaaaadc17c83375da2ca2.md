
A great technology introduced in .NET 4, the Managed Extensibility Framework (MEF), is utilized to allow a straightforward and simple way of creating custom extensions. Writing editor components (such as classifiers, taggers, margins, adornments, IntelliSense presenters, and many more) is easy with the editor extensibility templates provided by the VS SDK.

Chapter 7 provides an overview about the .NET framework history. It includes the Windows development technologies used before .NET, and shows how the platform evolved until version 4 was released.

# PART II
## .NET 4

- CHAPTER 7: .NET Framework Version History
- CHAPTER 8: Modern UI Frameworks (WPF and Silverlight)
- CHAPTER 9: Windows Communication Framework (WCF)
- CHAPTER 10: Enhancements to the .NET Core Framework
- CHAPTER 11: Enhancements to the .NET Workflow Framework
- CHAPTER 12: Enhancements to the .NET Data Framework
- CHAPTER 13: Enhancements to the .NET Communications Framework
- CHAPTER 14: .NET Charting Components

# 7
## .NET Framework Version History

.NET Framework represents one of the most important innovations in the history of software development. This chapter introduces you to the history of the .NET Framework, and takes you from the very beginning to the newest version.

First, you'll learn about some antecedents, focusing on Win32 programming in C, programming in C++, Visual Basic and Delphi, and COM programming. After that, you'll learn about the main goals of the .NET Framework.

This chapter describes the evolution of the .NET Framework, step by step, from version 1.0 to the newest version. Also, you'll learn about the .NET Compact Framework, as well as .NET Micro Framework.

Finally, you'll learn about the .NET Framework architecture, including Common Language Runtime (CLR), Base Class Library (BCL), and the complete list of services of the architecture.

# BEFORE THE .NET FRAMEWORK

It is much easier to understand what led Microsoft professionals to the vision of the .NET Framework if you grab a bit about the run-times used around 2000. During this period, developers had to use a lot of tools to develop a complex system. Some of them were chosen by preference and experience (for example, Delphi, Visual Basic, and C++), but others were selected just because they were all that was available on the market.

Let's take a look at some of those tools.

# Win/Win/32 Programming in C

Before the age of the .NET Framework, the traditional programming language of Windows was C for a long time. The book Programming Windows, Fifth Edition, by Charles Petzold (Redmond, WA: Microsoft Press, 1998), which primarily covered Windows APIs, as a key reference for developers.

The C language and its developer environment itself didn't help the programmers with their work. They had to deal with difficult syntaxes, manual memory handling, pointers, and so on. Despite the fact that C is a structured language, everything was missing that could have given an object-oriented environment. The ancient Windows programs ran directly on the layer of the operating system, and used its services.

# C++ Programming

Upon first sight, C++ is an extension of the C language, providing a significant improvement over the C language — real object-oriented capabilities. The object-oriented programming is not only a new environment or set of new tools; it's also a very new approach. An effective use of the capabilities is impossible without understanding that deeply.

However, this new and effective object-oriented approach, C++ still didn't hide the Win32 API, and programmers still had to deal with memory handling, pointers, and syntax constructs.

The first steps to take advantage of C++ were the run-time engines (MFC, ATL, VCL, and so on). When an application was developed in one of these frameworks, the developers had to perform significant research before migrating an application to another framework.

The C++ frameworks offered static and dynamic translation:

- In the case of static translation, the run-time was physically bound to the EXE files.
- In the case of dynamic translation, the EXE file used an external DLL.

The DLLs of Microsoft's frameworks (for example, the DLL of MFC) were gradually added to the operating system.

The C++ frameworks were closer to the C language than to the object-oriented approach of C++.

# Programming in Basic

Since 1998, more programmers started to use Visual Basic (VB) because of its simplicity. Visual Basic 6.0 was popular because it hid the Win32 API from the developers, which was used for creating user interfaces. Despite the fact that C++ frameworks were greatly improved, VB was still far from what developers were used to. The biggest problem with VB was that it appeared to be an object-oriented language, but in reality, it was only "object-like." There is no inheritance.

# Programming in Delphi

Delphi is a very successful product from Borland. It has lots of users, similar to VB, and these users are still an active community. The programming language of this tool is Object Pascal, a real object-oriented language. Delphi provided components through an extensible IDE not only for developing thick and thin clients but also for distributed systems.

Delphi hid the Win32 API with its Visual Component Library (VCL) run-time. It doesn't require a run-time (in the VB sense) because its compiler-generated EXE files can be used independently. When using Win32API for Delphi, you could use most Win32 features immediately.

# COM Programming

Component Object Model (COM) programming was born as a solution for language-independent component reusability. COM cannot be referred to in past tense, because it's still around in Microsoft's products, with continually decreasing intensity.

COM provides an architecture for developers that promises, "If you comply with the rules for creating COM classes, your code will be binary reusable."

One of the most important advantages of binary reusability is that the components can be reusable independently from the language they were developed in. Unfortunately, this reusability was not complete, because of the limitations of the developer tools.

In contrast, one of the most frequently mentioned disadvantages of COM programming is that it is missing real inheritance. Although COM provides some technologies for, they are not easy to use.

However, COM provides a very important capability for developers — the transparency of the location of components. A component can even be in another process, or on another computer. If it's correctly installed (that is, marked into the registry), you don't have to deal the communication of processes and computers using the use of the component.

COM components can also be used as interfaces that are managed by the Microsoft Transaction Server (MTS), the ancestor of COM+ run-time that is still a part of the Windows operating systems.

The common reference of COM and the .NET Framework hides COM's pioneering role in the birth of the component-based approach and developer method. There is no question that COM is wrong, or that it is an already completely outdated technology, or that was condemned to death.
