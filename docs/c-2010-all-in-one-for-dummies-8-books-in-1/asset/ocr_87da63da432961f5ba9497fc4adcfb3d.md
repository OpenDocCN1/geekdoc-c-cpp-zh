# 380 Dividing a Single Program into Multiple Assemblies

+   - Class library (. DLL): A compiled library of functionality that can be used by other programs. All programs in this book also use libraries. For example, the System namespace (the home of classes such as String, Console, Exception, Math, and Object) exists in a set of library assemblies. Every program needs System classes. Libraries are housed in DLL assemblies.

Libraries are not executable — you can't make them directly. Instead, you must call their code from an executable or another library. The Common Language Runtime (CLR), which runs C# programs, loads library assemblies into memory as needed.

The important concept to know is that you can easily write your own class libraries. I show you in the later section "Putting Your Classes into Class Libraries."

![](bbox=[0.139, 0.245, 0.228, 0.313])

# Assemblies

Assemblies, which are the compiled versions of individual projects, contain the project's code in a special format, along with a bunch of metadata, or detailed information about classes in the assemblies.

I introduce assemblies in this section because they round out your understanding of the C# build process — and discussion of assemblies and access keywords such as protected and internal (it covers namespaces and these two access keywords later in this chapter). Assemblies also play a big part in understanding class libraries. It's covered in the later section "Putting Your Classes into Class Libraries."

The C# compiler converts the project's code to Common Intermediate Language (usually called IL) that's stored in the appropriate type of assembly. IL represents assembly assembly language (one step beyond the 1s and 0s used in machine language) that hardcore programmers have used for decades to get down "close to the metal" because their higher-level languages don't do what they needed or the compilers couldn't produce the most efficient code.

One major consequence of compiling from .NET to IL, regardless of language, is that a program can use assemblies written in different languages. For example, a C# program can call methods in an assembly originally written in Visual Basic or C++ or the C# program can subclass a VB class.

You can take a look at IL by running the Ildasm.exe tool in the .NET Software Development Kit (SDK) or the Reflector tool that I point you to at csharp102.info. Select a .EXE or .DLL assembly file to view its code as IL. A Visual Studio solution can contain any number of projects.

![](bbox=[0.139, 0.617, 0.228, 0.706])