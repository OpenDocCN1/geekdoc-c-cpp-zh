# Chapter 1: Introducing C#

Studio Code (https://code.visual.com). To optimize working with C# in Visual Studio Code, you will want to install the C# extension, as shown in Figure 1.1. However, if you are working on Windows or Mac, consider the corresponding version of Microsoft Visual Studio 2022 (or later)—see https://visualstudio.microsoft.com/. All are available free of charge.

![](bbox=[0.125, 0.237, 0.842, 0.483])

In the remainder of this section, we provide instructions for these editors. For Visual Studio Code, we rely on the command-line interface (CLI) tool dotnet CLI for creating the initial C# program in addition to compiling and running the program. For Windows and Mac, we focus on using the platform-specific version of Visual Studio 2022.

# With Dotnet CLI

The dotnet command, dotnet, is the dotnet command-line interface, or dotnet CLI, and it may be used to generate the initial code base for a C# program in addition to compiling and running the program.³ (To avoid ambiguity between CLI referring to the Common Language Infrastructure or the command-line interface, throughout the

+   This tool was released around the same time as C# 7.0, and it eclipsed compiling directly with the C# compiler, csc.exe.