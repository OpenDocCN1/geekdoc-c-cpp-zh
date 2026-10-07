what application type to build (console, web, library, etc.), which .NET framework(s) to support, compiler settings, and which potential settings are needed to launch the application, along with other dependencies the code may rely on (called libraries). For example, the sample .NET console project file created in the previous section appears in Listing 1.2.

# Listing 1.2: Sample .NET Console Project File

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net7.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>
</Project>
```

In Listing 1.2, the application type is identified as a .NET 8.0 (net8.0) console application (Exe). The two other elements, Nullable (C# 8.0) and ImplicitUsings (C# 10.0), will be discussed in "Declaring Types That Allow Null" in Chapter 3 and "Using Directives" (https://essentialsharp.com/using-directives) in Chapter 5, respectively. All other settings (such as C# files to compile) are identified by convention. For example, by default, all *.cs files in the same directory (or subdirectory) as the project file are included in the compile.

# Compilation and Execution

When you execute dotnet run, it first implicitly runs dotnet build to compile the code. The compiled output created by the dotnet build command is an assembly called HelloWorld.dll Assemblies contain a set of instructions specifying how a program will behave. The extension stands for dynamic link library (DLL), and with .NET, assemblies have a .dll extension if they are console

+   * "*" in *.cs is called a wildcard character, and matches any number of characters including none. In this instance, identifies that any file ending in .cs will be included. If it was *.cs it would include files with just an ending in .cs.
* Note that if you use the Microsoft .NET Framework to create a console program, the compiled code is placed into a HelloWorld.exe file that you can execute assuming the Microsoft .NET Framework is installed on the computer.