![](bbox=[0.05, 0.15, 0.18, 0.28])

```
// ClassLibrary -- in a Class Library project
// File: Program.cs in ClassLibraryDriver project
// ClassLibrary -- A simple class library and its driver program
using System;
namespace ClassLibrary
{
public class MyLibrary
{
public void LibraryFunction1()
{
Console.WriteLine("This is LibraryFunction1()");
}
public static int LibraryFunction2(int input)
{
Console.WriteLine("This is LibraryFunction2(), returning {0}", input);
return input; // Just parrot the input.
}
}
}
```

Libraries can contain any C# type: class, structure, delegate, interface, and enumeration. I cover structures (structs) in Book I, delegates in Chapter 9 of this minibook, interfaces in Chapter 8 of this minibook, and enumerations (enums) in the article “Enumerating the Charms of the Enum” on csharp102.info.

![](bbox=[0.08, 0.6, 0.18, 0.7])

In class library code, you normally shouldn't catch exceptions. Let them bubble up from the library to the client code that's calling into the library. Clients need to know about these exceptions and handle them in their own ways. I cover exceptions in Book II.

# Using a driver program to test a library

By itself, the class library doesn't do anything, so you need a driver program, a small executable program that “drives” the library to test it during development by calling its methods.

In other words, write a program that uses classes and methods from the library. You see this behavior in the NamespaceUse program example later in this chapter (and other programs in this book) — for example, when you call the WriteLine() method of class Console from the .NET Framework class libraries. (Console is in the System namespace, in the library file mscorlib.dll.)

The following chunk of code continues the previous code listing. This one adds a new project with one class that contains a Main() method, and you can write code to exercise your library inside Main():

```
// ClassLibrary driver program
// In a separate Console Application project:
```