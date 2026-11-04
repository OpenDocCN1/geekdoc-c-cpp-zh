
If the program takes arguments, such as filenames, from the command line, drag the files to the executable file in Windows Explorer. I show you this process in the article "Passing Arguments to a Program" at http://csharp102.info; click the Articles tab and look in the section "C# Techniques."

A solution in Visual Studio can contain multiple projects — some .DLL and some .EXE. If a solution contains more than one .EXE project, you must tell Visual Studio which project is the start-up project: That one runs from the Debug menu. To specify a start-up project, right-click that project in Solution Explorer and choose Set As Startup Project. The start-up project's name appears in boldface in Solution Explorer.

Think of a solution containing two .EXE assemblies as two separate programs that happen to use the same library assemblies. For example, you might have in a solution a console executable and a Windows Forms executable plus some libraries. If you make the console app the start-up project and compile the code, you produce a console app. If you make the Windows Forms app the start-up — well, you get the idea.

## Class libraries

A class library contains one or more classes, usually ones that work together in some way. Often, the classes in a library are in their own namespaces. (I explain namespaces later in this chapter in the section "Putting Classes into Namespaces.") You may build a library of math routines, a library of string handling routines, and a library of input/output routines, for example.

Sometimes, you even build a whole solution that is nothing but a class library, rather than a program that can be executed on its own. (Typically, while developing this type of library, you also build an accompanying .EXE project, or driver, with which to test your library during development. But when you release the library for programmers to use, you release just the .DLL [not the .EXE] — and documentation for it, which you can generate by writing XML comments in the code. XML comments are described in Book IV, which is all about Visual Studio.)

The next section shows you how to write your own class libraries (and drivers).

## Putting Your Classes into Class Libraries

The simplest definition of a class library project is one whose classes contain no Main() method. Can that definition be correct? It can and is. The existence of Main() distinguishes a class library from an executable. C# libraries are much easier to write and use than similar libraries were in C or C++.

The following sections explain the basic concepts involved in creating your own class libraries. Don't worry: C# does the heavy lifting. Your end of it is quite simple.

![](img/80ff26f06fc9ab951e1cd4257b867366_403_0.png)

Even the free Visual C# 2012 Express Edition can now create class libraries. It used to require a small hack to make it work.

## Creating the projects for a class library

You can create the files for a new class library project and its driver in either of two ways:

- **Create the class library project first and then add the driver project to its solution.** You might take this approach if you were writing a stand-alone class library assembly. I describe how to create the class library project in the next section.
- **Create a driver program first and then add one or more library projects to its solution.** Thus you might first create the driver program as a console application or a graphical Windows Forms (or Windows Presentation Foundation) application. Then you would add class library projects to that solution.

This approach is the one to take if you want to add a supporting library to an ongoing application. In that case, the “driver” could be either the ongoing program or a special driver project added to the solution just to test the library. For testing, you set the driver project as the start-up project as described in the earlier section “Executables.”

## Creating a stand-alone class library

If your whole purpose is to develop a stand-alone class library that can be used in various other programs, you can create a solution that contains a class library project from scratch — here’s how simple it is:

- 1. **Create a new project.**
- 2. **When you pick the template to base it on in the New Project dialog box, select Class Library (rather than, say, Console Application).**

Figure 10-1 shows what Solution Explorer looks like at this point.

After you have a class library project, you can add a driver project (or a unit test project or both) using the approach described in the next section.

![](img/80ff26f06fc9ab951e1cd4257b867366_404_0.png)

### Adding a second project to an existing solution

If you have an existing solution — whether it’s an ongoing application or a class library project such as the one described in the previous section — you can easily add a second project to your solution: either a class library project or an executable project, such as a driver. Follow these steps:

- 1. After your existing solution is open in Visual Studio, right-click the solution node (the top node) in Solution Explorer.
- 2. From the pop-up menu, choose Add→New Project.
- 3. In the New Project dialog box, select the type of project you want to add.

Select a class library, a console application, a Windows Forms application, or another available type on the right side of the dialog box.

- 4. Use the Location box to navigate to the folder where you want the project.

The location you navigate to depends on how you want to organize your solution. You can put the new project’s folder in either of two places:

### Can't Use Your Namespace in Class Library?

- *All-in-one-folder*: Navigate into the main project folder, making the added project a subfolder. (See Figure 10-2.)
- *Side-by-side*: Navigate to the folder that contains the main project folder so that the two projects are at the same level. (See Figure 10-3.)

- 5. Name your project and click OK.

If the new project is a library project, choose its name carefully — it will become the name of the library's .DLL file and the name of the namespace containing the project's classes.

If you need to give the library project the same name as another project or even the main project, you can distinguish it by appending the suffix Lib, as in `MyConversionLib`.

If the project you're adding is intended to stand on its own and be usable in other programs, use the side-by-side approach.

The `ClassLibrary` example in this section (like most examples in this book) takes the all-in-one-folder approach. The point is that although the folders don't have to be in the same place, putting them there can be convenient.

The task of selecting the location is independent of adding the new project directly to the `ClassLibrary` solution. The two project folders can be in the same solution while still being located in different places.

![](img/80ff26f06fc9ab951e1cd4257b867366_405_0.png)

Figure 10-2:
Organizing two projects in an all-in-one-folder.

![](img/80ff26f06fc9ab951e1cd4257b867366_405_1.png)

Figure 10-3:
Organizing two projects side by side.

![](img/80ff26f06fc9ab951e1cd4257b867366_405_2.png)

## Creating classes for the library

After you have a class library project, create the classes that make up the library. The following ClassLibrary example shows a simple class library — I show you some driver code for it after the example:

![](img/80ff26f06fc9ab951e1cd4257b867366_406_0.png)

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

Book II Chapter 10 Can I Use Your Namespace in the Library?

![](img/80ff26f06fc9ab951e1cd4257b867366_406_1.png)

Libraries can contain any C# type: class, structure, delegate, interface, and enumeration. I cover structures (structs) in bonus Chapter 4 on http://csharp102.info, delegates in Chapter 9 of this minibook, interfaces in Chapter 8 of this minibook, and enumerations (enums) in the article “Enumerating the Charms of the Enum” on the same site.

![](img/80ff26f06fc9ab951e1cd4257b867366_406_2.png)

In class library code, you normally shouldn’t catch exceptions. Let them bubble up from the library to the client code that’s calling into the library. Clients need to know about these exceptions and handle them in their own ways. I cover exceptions in Book I.

## Using a driver program to test a library

By itself, the class library doesn’t do anything, so you need a driver program, a small executable program that “drives” the library to test it during development by calling its methods.

In other words, write a program that uses classes and methods from the library. You see this behavior in the NamespaceUse program example later in this chapter (and other programs in this book) — for example, when you call the WriteLine() method of class Console from the .NET Framework class libraries. (Console is in the System namespace, in the library file mscorlib.dll.)
