
## Compiling and Running the Application

The C# compiler allows any file extension for files containing C# source code, but .cs is typically used. After saving the source code to a file, developers must compile it. (Appendix A provides instructions for installing the compiler.) Because the mechanics of the command are not part of the C# standard, the compilation command varies depending on the C# compiler implementation.

If you place Listing 1.1 into a file called HelloWorld.cs, the compilation command in Output 1.1 will work with the Microsoft .NET compiler (assuming appropriate paths to the compiler are up).4

### Output 1.1:

```
>csc.exe HelloWorld.cs
Microsoft (R) Visual C# 2008 Compiler version 4.0.20506.1
for Microsoft (R) .NET Framework version 4.0
Copyright (C) Microsoft Corporation. All rights reserved.
```

The exact output will vary depending on what version of the compiler you use.

Running the resultant program, HelloWorld.exe, displays the message shown in Output 1.2.

### Output 1.2:

```
>HelloWorld.exe
Hello. My name is Inigo Montoya.
```

The program created by the C# compiler, HelloWorld.exe, is an assembly. Instead of creating an entire program that can be executed independently, developers can create a library of code that can be referenced by another, larger program. Libraries (or class libraries) use the filename extension .dll, which stands for Dynamic Link Library (DLL). A library is also an assembly. In other words, the output from a successful C# compile is an assembly regardless of whether it is a program or a library.

4. Compilation using the Mono compiler, an open source compiler sponsored by Novell, is virtually identical, except that the compiler name is mcs.exe rather than csc.exe. Although I would very much have liked to place instructions for each platform here, doing so detracts from the topic of introducing C#. See Appendix A for details on Mono.

### Language Contrast: Java—Filename Must Match Class Name

In Java, the filename must follow the name of the class. In C#, this convention is frequently followed but is not required. In C#, it is possible to have two classes in one file, and starting with C# 2.0, it’s possible to have a single class span multiple files.

## C# Syntax Fundamentals

Once you successfully compile and run the HelloWorld program, you are ready to start dissecting the code to learn its individual parts. First, consider the C# keywords along with the identifiers that the developer chooses.

### BEGINNER TOPIC

### Keywords

In order for the compiler to interpret the code, certain words within C# have special status and meaning. Known as **keywords** or **reserved words**, they provide the concrete syntax that the compiler uses to interpret the expressions the programmer writes. In the HelloWorld program, class, static, and void are examples of keywords.

The compiler uses the keywords to identify the structure and organization of the code. Because the compiler interprets these words with elevated significance, you can use keywords only under the specific rules identified by the language. In other words, programming languages require that developers place keywords only in certain locations. When programmers violate these rules, the compiler will issue errors.

### C# Keywords

Table 1.1 shows the C# keywords.

### TABLE 1.1: C# Keywords

| abstract | add* | alias* | as |
| :--- | :--- | :--- | :--- |
| ascending* | base | bool | break |
| by* | byte | case | catch |
| char | checked | class | const |
| continue | decimal | default | delegate |
| descending* | do | double | dynamic* |
| else | enum | equals* | event |
| explicit | extern | false | finally |
| fixed | float | for | foreach |
| from* | get* | global* | goto |
| group* | if | implicit | in |
| int | interface | internal | into* |
| is | join* | let* | lock |
| long | namespace | new | null |
| object | on* | operator | orderby* |
| out | override | params | partial* |
| private | protected | public | readonly |
| ref | remove* | return | sbyte |
| sealed | select* | set* | short |
| sizeof | stackalloc | static | string |
| struct | switch | this | throw |
| true | try | typeof | uint |
| ulong | unchecked | unsafe | ushort |
| using | value* | var* | virtual |
| void | volatile | where* | while |
| yield* | | | |

* Contextual keyword

After C# 1.0, no new keywords were introduced to C#. However, some constructs in these later versions use contextual keywords, which are significant only in specific locations. Outside these designated locations, contextual keywords have no special significance.5 By this method, all C# 1.0 code is fully compatible with the later standards.6 (Table 1.1 designates contextual keywords with a *.)

- 5. For example, early in the design of C# 2.0, the language designers designated yield as a keyword, and Microsoft released alpha versions of the C# 2.0 compiler, with yield as a designated keyword, to thousands of developers. However, the language designers eventually determined that by using yield return rather than yield, they could ultimately avoid adding yield as a keyword because it would have no special significance outside its proximity to return.

- 6. There are rare and unfortunate incompatibilities, such as the following:
  - C# 2.0 requires implementation of IDisposable with the using statement, rather than simply a Dispose() method
  - Some rare generic expressions such as F(G<A, B>(7)); in C# 1.0, that means F((G<A, B>(7))); and in C# 2.0 that means to call generic method G<A, B> with argument 7 and pass the result to F

### BEGINNER TOPIC

### Identifiers

In addition to the keywords defined in C#, developers may provide their own names. Programming languages refer to these names as identifiers since they identify constructs that the programmer codes. In Listing 1.1, HelloWorld and Main are examples of identifiers. It is possible to assign a value to a variable and then refer to it later using its identifier. It is important, therefore, that the names the developer assigns are meaningful rather than arbitrary. A keen ability to select succinct and indicative names is an important characteristic of a strong programmer because the resultant code is easier to understand and reuse. In some rare cases, some identifiers, such as Main, can have a special meaning in the C# language.

### ADVANCED TOPIC

### Keywords

Although it is rare, keywords may be used as identifiers if they include “@” as a prefix. For example, you could name a local variable @return. Similarly (although it doesn’t conform to the casing standards of C# coding standards), it is possible to name a method @throw().

There are also four undocumented reserved keywords in the Microsoft implementation: __arglist, __makeref, __reftype, and __refvalue. These are required only in rare interop scenarios and you can ignore them for all practical purposes.

### Type Definition

All code in C# appears within a type definition, and the most common type definition begins with the keyword class. A class definition is the section of code that generally begins with class identifier { ... }, as shown in Listing 1.2.

```
LISTING 1.2: Basic Class Declaration

class HelloWorld
{
    ...
}
```

The name used for the type (in this case, HelloWorld) can vary, but by convention, it should begin with a capital letter and a noun. If the name contains multiple words appended together, then each additional word should also begin with a capital letter. For this particular example, therefore, other possible names are Greetings, HelloInigoMontoya, Hello, or simply Program. (Program works especially if it is the class that contains the Main() method described next.) The CLI creators called this type of casing Pascal casing because of its popularity in the Pascal programming
