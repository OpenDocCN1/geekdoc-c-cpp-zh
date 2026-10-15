# TABLE 21.1: Primary C# Compilers

| Compiler | Description |
|---|---|
| Windows Desktop CLR | This version of the CLR is for creating Windows client applications. |
| CoreCLR | The .NET Core project, as the name implies, contains the core functionality common to all upcoming flavors of .NET from Microsoft. It is intended to be a cross-platform, open source implementation designed for high-performance server applications. The CoreCLR is the implementation of the CLR for this project. At the time of this book’s writing, Microsoft had announced that it was in preview release for Windows, OS X, and Linux. See https://github.com/dotnet/coreclr for more details. |
| Microsoft Silverlight | This cross-platform implementation of the CLI was for creating browser-based web client applications. Microsoft stopped developing Silverlight in 2013. |
| .NET Compact Framework | This is a trimmed-down implementation of the .NET Framework designed to run on PDAs, phones, and the Xbox 360.

The XNA library and tools for developing Xbox 360 applications are based on the Compact Framework 2.0 release; Microsoft stopped development of XNA in 2013. |
| .NET Micro Framework | The Micro Framework is Microsoft’s open source implementation of the CLI for devices so resource constrained that they cannot run the compact framework. See http://www.netmf.com/ for details. |
| Mono | Mono is an open source, cross-platform implementation of the CLI for many UNIX-based operating systems, mobile operating systems such as Android, and game consoles such as PlayStation and Xbox. It is under active development by Xamarin, which has partnered with Microsoft to provide extensions integrating it into Visual Studio 2015. |
| DotGNU Portable.NET | This effort to create a cross-platform implementation of the CLI was “decommissioned” in 2012. |
| Shared Source CLI (Rotor) | Between 2001 and 2006, Microsoft released “shared source” reference implementations of the CLI licensed for noncommercial use. |