As shown in Fig.C#–1.1, .NET Framework 2.0 consists of components, such as .NET Framework Base Class Library, Windows Forms, ASP.NET, Console, ActiveX Data Objects for .NET (ADO.NET), Common Language Specification (CLS), Common Type System (CTS), and .NET languages, such as C# and Visual Basic.NET. Similarly, .NET Framework 3.0 comprises WPF, Windows Communication Foundation (WCF), Windows Workflow Foundation (WF), and Windows CardSpace (WCS). .NET Framework 3.5 introduces a few enhancements, such as Language-Integrated Query (LINQ), ASP.NET AJAX, ADO.NET Entity Framework and Data Services, and new compilers for C#, Visual Basic.NET, and C++. Finally, .NET Framework 4.0 incorporates Parallel Extensions, Managed Extensibility Framework, Dynamic Language Runtime, and other additional enhancements.

Let’s now learn about some of the important components of .NET Framework 4.0.

# Explaining the Components of .NET Framework 4.0

As mentioned earlier, .NET Framework 4.0 is based on .NET Framework 2.0, 3.0, and 3.5 and therefore includes several components that are a part of these versions of the .NET Framework. Some of the basic components of .NET Framework 4.0 are as follows:

+   - CLR
+   - CTS and CLS
+   - Assemblies and metadata
+   - .NET Framework Base Class Library
+   - Windows Forms
+   - ADO.NET
+   - ASP.NET and ASP.NET AJAX
+   - WPF
+   - WCF
+   - WF
+   - WCS
+   - LINQ

Let’s now discuss these components one by one in detail in the following sections.

# Common Language Runtime (CLR)

One of the most important and central components of the .NET Framework is CLR. Also referred to as runtime, CLR essentially provides a runtime or execution environment within which all .NET applications run. The functionalities that CLR provides include memory management, exception handling, debugging, security, thread execution, code execution, type safety, verification, and compilation. In simple words, you can say that CLR manages the execution of .NET applications. The code that runs under CLR or targets CLR is known as managed code, while unmanaged code is the code that is compiled into native or machine code and is directly executed by an operating system. As managed code benefits from various features such as cross-language integration, enhanced security, type safety, and memory management, using the managed execution environment enables programmers to commit fewer mistakes, thereby create more secure and stable applications.

Interoperability between various .NET languages, such as Visual C#, Visual Basic, or Visual C++ is facilitated by CLR, as it provides a common environment for the execution of code written in any of these languages. All .NET applications, when run, are compiled into an intermediate code called the Microsoft Intermediate Language (MSIL) or IL code, by the language compiler. This MSIL code is then used by the Just-In-Time (JIT) compiler to compile the code into the native machine code, which is the final executable code. Fig.C#–1.2 illustrates the functioning of CLR: