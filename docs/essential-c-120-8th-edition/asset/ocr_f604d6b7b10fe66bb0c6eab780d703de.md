# TABLE 24.1: Implementations of the CLI (continued)

| Compiler | Description |
|---|---|
| Xamarin | A set of development tools and platform-portable .NET libraries as well as an implementation of the CLI that helps developers create applications that run on Microsoft Windows, iOS, macOS, and Android platforms with a very high degree of code reuse. Xamarin reached end of support in May of 2024. |
| Microsoft Silverlight | A legacy cross-platform implementation of the CLI intended for creating browser-based client applications. Microsoft stopped developing Silverlight in 2013. |
| .NET Compact Framework | A legacy trimmed-down implementation of the .NET Framework designed to run on PDAs, phones, and Xbox 360. The XNA library and tools for developing Xbox 360 applications are based on the Compact Framework 2.0 release; Microsoft stopped development of XNA in 2013. |
| .NET Micro Framework | Microsoft's open source implementation of the CLI for devices so resource constrained that they cannot run the compact framework. |
| Portable .NET | This effort to create a cross-platform implementation of the CLI was decommissioned in 2012. |
| Shared Source CLI (Rotor) | Between 2001 and 2006, Microsoft released shared-source reference implementations of the CLI licensed for noncommercial use. |

While the list is extensive considering the work required to implement the CLI, just three frameworks are the most relevant going forward.

# Microsoft .NET Framework

The Microsoft .NET Framework was the first .NET CLI implementation (released in February 2000). As such, it is the most mature framework and has the largest API set. It supports building web, console, and Microsoft Windows client applications. The biggest limitation of the .NET Framework is that it runs on Microsoft Windows only—in fact, it is bundled with Microsoft Windows. Numerous sub-frameworks are included with the Microsoft .NET Framework; the most prominent are described here: