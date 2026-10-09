Contained within the CLI standard are specifications for the following:

+   - The Virtual Execution System
- The Common Intermediate Language
- The Common Type System
- The Common Language Specification
- Metadata
- The framework

This chapter broadens your view of C# to include the CLI, which is critical to how C# programs operate and interact with programs and with the operating system.

# ## CLI Implementations

The primary implementations of the CLI today are .NET Core, which runs on Windows, as well as UNIX/Linux and Mac OS; the .NET Framework for Windows; and Xamarin, which is intended for iOS, Mac OS, and Android applications. Each implementation of the CLI includes a C# compiler and a set of framework class libraries; the version of C# supported by each, as well as the exact set of classes in the libraries, varies considerably, and many implementations are now only of historical interest. Table 22.1 describes these implementations.

**TABLE 22.1: Implementations of the CLI**

| Compiler | Description |
| :------- | :---------- |
| Microsoft .NET Framework | This traditional (and first) version of the CLR is for creating applications that run on Windows. It includes support for Windows Presentation Foundation, Windows Forms, and ASP.NET. It uses the .NET Framework Base Class Library (BCL). |
| .NET Core/CoreCLR | The .NET Core project, as the name implies, contains the core functionality common to all new implementations of .NET. It is an open source and platform-portable rewrite of the .NET Framework designed for high-performance applications. The CoreCLR is the implementation of the CLR for this project. At time of this book's writing, .NET Core 2.0 has been released for Windows, macOS, Linux, FreeBSD, and NetBSD. See https://github.com/dotnet/coreclr for more details. |