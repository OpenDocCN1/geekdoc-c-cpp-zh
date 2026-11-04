
You must create text-only files, not formatted word-processor files, because the format information in a word processor file will confuse the C# compiler. When entering the program, call the file Example.cs.

## Compiling the Program

To compile the program, execute the C# compiler, csc.exe, specifying the name of the source file on the command line, as shown here:

```
C:\>csc Example.cs
```

The csc compiler creates a file called Example.exe that contains the MSIL version of the program. Although MSIL is not executable code, it is still contained in an exe file. The Common Language Runtime automatically invokes the JIT compiler when you attempt to execute Example.exe. Be aware, however, that if you try to execute Example.exe (or any other exe file that contains MSIL) on a computer for which the .NET Framework is not installed, the program will not execute because the CLR will be missing.

> Note Prior to running csc.exe you will need to open a Command Prompt window that is configured for Visual Studio. The easiest way to do this is to select Visual Studio 2008 Command Prompt under Visual Studio Tools in the Start menu. Alternatively, you can start an unconfigured Command Prompt window and then run the batch file vsvars32.bat, which is provided by Visual Studio. You may, however, encounter a problem with the command-line approach. At the time of this writing, Visual C# 2008 Express Edition does not provide the Visual Studio Tools menu or the vsvars32.bat file. Therefore, if you are using Visual C# 2008 Express, you may not be able to configure a command prompt window automatically. In this case, use the Visual Studio IDE instead. However, Visual C++ 2008 Express Edition does supply both vsvars32.bat and the Visual Studio 2008 Command Prompt menu selection. Therefore, if you also install Visual C++ 2008 Express Edition, you will be able to start a properly configured command prompt window that will also work for C#.

## Running the Program

To actually run the program, just type its name on the command line, as shown here:

```
C:\>Example
```

When the program is run, the following output is displayed:

```
A simple C# program.
```

## Using the Visual Studio IDE

Visual Studio is Microsoft's integrated programming environment. It lets you edit, compile, run, and debug a C# program, all without leaving its well-thought-out environment. Visual Studio offers convenience and helps manage your programs. It is most effective for larger projects, but it can be used to great success with smaller programs, such as those that constitute the examples in this book.

5. Next, add the file to the project by pressing Add. Your screen will now look like this:

![](img/7022d9b97326a713562c15aa43977d15_44_0.png)

6. Next, type the example program into the Example.cs window and then save the file. (You can download the source code to the programs in this book from www.mhprofessional.com so you won't have to type in each example manually.) When done, your screen will look like this:

![](img/7022d9b97326a713562c15aa43977d15_44_1.png)

By convention, C# programs use the .cs file extension, and this is a convention that you should follow. Also, many programmers call a file by the name of the principal class defined within the file. This is why the filename Example.cs was chosen. Since the names of C# programs are arbitrary, names won't be specified for most of the sample programs in this book. Just use names of your own choosing.

The program begins with the following lines:

```
/*
    This is a simple C# program.
    Call this program Example.cs.
*/
```

This is a comment. Like most other programming languages, C# lets you enter a remark into a program's source file. The contents of a comment are ignored by the compiler. Instead, a comment describes or explains the operation of the program to anyone who is reading its source code. In this case, the comment describes the program and reminds you to call the source file Example.cs. Of course, in real applications, comments generally explain how some part of the program works or what a specific feature does.

C# supports three styles of comments. The one shown at the top of the program is called a multiline comment. This type of comment must begin with /* and end with */. Anything between these two comment symbols is ignored by the compiler. As the name suggests, a multiline comment can be several lines long.

The next line in the program is

```
using System;
```

This line indicates that the program is using the System namespace. In C#, a namespace defines a declarative region. Although we will examine namespaces in detail later in this book, a brief description is useful now. Through the use of namespaces, it is possible to keep one set of names separate from another. In essence, names declared in one namespace will not conflict with names declared in a different namespace. The namespace used by the program is System, which is the namespace reserved for items associated with the .NET Framework class library, which is the library used by C#. The using keyword simply states that the program is using the names in the given namespace.

The next line of code in the program is shown here:

```
class Example {
```

This line uses the keyword class to declare that a new class is being defined. As mentioned, the class is C#'s basic unit of encapsulation. Example is the name of the class. The class definition begins with the opening curly brace ({) and ends with the closing curly brace (}). The elements between the two braces are members of the class. For the moment, don't worry too much about the details of a class except to note that in C#, most program activity occurs within one.

The next line in the program is the single-line comment, shown here:

```
// A C# program begins with a call to Main().
```

## Handling Syntax Errors

If you are new to programming, it is important to learn how to interpret and respond to errors that may occur when you try to compile a program. Most compilation errors are caused by typing mistakes. As all programmers soon find out, accidentally typing something incorrectly is quite easy. Fortunately, if you type something wrong, the compiler will report a syntax error message when it tries to compile your program. This message gives you the line number at which the error is found and a description of the error itself.

Although the syntax errors reported by the compiler are, obviously, helpful, they sometimes can also be misleading. The C# compiler attempts to make sense out of your source code no matter what you have written. For this reason, the error that is reported may not always reflect the actual cause of the problem. In the preceding program, for example, an accidental omission of the opening curly brace after the Main() method generates the following sequence of errors when compiled by the csc command-line compiler. (Similar errors are generated when compiling using the IDE.)

```
EX1.CS(12,21): error CS1002: ; expected
EX1.CS(13,22): error CS1519: Invalid token '(' in class, struct, or
interface member declaration
EX1.CS(15,1): error CS1022: Type or namespace definition, or
end-of-file expected
```

Clearly, the first error message is completely wrong, because what is missing is not a semicolon, but a curly brace. The second two messages are equally confusing.

The point of this discussion is that when your program contains a syntax error, don't necessarily take the compiler's messages at face value. They may be misleading. You may need to 'second guess' an error message in order to find the problem. Also, look at the last few lines of code immediately preceding the one in which the error was reported. Sometimes an error will not be reported until several lines after the point at which the error really occurred.

## A Small Variation

Although all of the programs in this book will use it, the line

```
using System;
```

at the start of the first example program is not technically needed. It is, however, a valuable convenience. The reason it's not necessary is that in C# you can always fully qualify a name with the namespace to which it belongs. For example, the line

```
Console.WriteLine("A simple C# program.");
```

can be rewritten as

```
System.Console.WriteLine("A simple C# program.");
```

Thus, the first example could be recoded as shown here:

```
// This version does not include "using System;";
```

```
class Example {
```
