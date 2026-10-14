
Of course, if you had to write the full name of a class every time you used it, the situation would be no better than prefixing qualifiers or even just naming the class with some globally unique name such as SystemConsole. Fortunately, you can solve this problem with a using directive in your programs. If you return to the TestHello program in Visual Studio 2015 and look at the file Program.cs in the Code and Text Editor window, you will notice the following lines at the top of the file:

Click here to view code image

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
```

These lines are using directives. A using directive brings a namespace into scope. In subsequent code in the same file, you no longer need to explicitly qualify objects with the namespace to which they belong. The five namespaces shown contain classes that are used so often that Visual Studio 2015 automatically adds these using directives every time you create a new project. You can add more using directives to the top of a source file if you need to reference other namespaces.

The following exercise demonstrates the concept of namespaces in more depth.

## Try longhand names

- 1. In the Code and Text Editor window displaying the Program.cs file, comment out the first using directive at the top of the file, like this:
  
- 2. On the Build menu, click Build Solution.
  The build fails, and the Error List window displays the following error message:
  
- 3. In the Error List window, double-click the error message.
  The identifier that caused the error is highlighted in the Program.cs source file with a red squiggle.
  
- 4. In the Code and Text Editor window, edit the Main method to use the fully qualified name System.Console.
  Main should look like this:

```
//using System;
```

Click here to view code image

```
The name 'Console' does not exist in the current context.
```

Click here to view code image

```
static void Main(string[] args)
```

```
{
    System.Console.WriteLine("Hello World!");
}
```

### Note

When you type the period after System, IntelliSense displays the names of all the items in the System namespace.

- 5. On the Build menu, click Build Solution.

The project should build successfully this time. If it doesn’t, ensure that Main is exactly as it appears in the preceding code, and then try building again.

- 6. Run the application to be sure that it still works by clicking Start Without Debugging on the Debug menu.

- 7. When the program runs and displays “Hello World!” in the console window, press Enter to return to Visual Studio 2015.

## Namespaces and assemblies

A using directive simply brings the items in a namespace into scope and frees you from having to fully qualify the names of classes in your code. Classes are compiled into assemblies.

An assembly is a file that usually has the .dll file name extension, although strictly speaking, executable programs with the .exe file name extension are also assemblies.

An assembly can contain many classes. The classes that the .NET Framework class library includes, such as System.Console, are provided in assemblies that are installed on your computer together with Visual Studio. You will find that the .NET Framework class library contains thousands of classes. If they were all held in the same assembly, the assembly would be huge and difficult to maintain. (If Microsoft were to update a single method in a single class, it would have to distribute the entire class library to all developers!)

For this reason, the .NET Framework class library is split into a number of assemblies, partitioned by the functional area to which the classes they contain relate. For example, a “core” assembly (actually called mscorlib.dll) contains all the common classes, such as System.Console, and other assemblies contain classes for manipulating databases, accessing web services, building GUIs, and so on. If you want to make use of a class in an assembly, you must add a reference to that assembly to your project.

You can then add *using* directives to your code that bring the items in namespaces in that assembly into scope.

You should note that there is not necessarily a 1:1 equivalence between an assembly and a namespace: A single assembly can contain classes defined in many namespaces, and a single namespace can span multiple assemblies. For example, the classes and items in the *System* namespace are actually implemented by several assemblies, including *mscorlib.dll*, *System.dll*, and *System.Core.dll*, among others. This all sounds very confusing at first, but you will soon get used to it.

When you use Visual Studio to create an application, the template you select automatically includes references to the appropriate assemblies. For example, in Solution Explorer for the TestHello project, expand the References folder. You will see that a console application automatically contains references to assemblies called *Microsoft.CSharp*, *System*, *System.Core*, *System.Data*, *System.Data.DataSetExtensions*, *System.Net.Http*, *System.Xml*, and *System.Xml.Linq*. You might be surprised to see that *mscorlib.dll* is not included in this list. The reason for this is that all .NET Framework applications must use this assembly because it contains fundamental runtime functionality. The References folder lists only the optional assemblies; you can add or remove assemblies from this folder as necessary.

To add references for additional assemblies to a project, right-click the References folder and then click Add Reference—you will perform this task in later exercises. You can remove an assembly by right-clicking the assembly in the References folder and then clicking Remove.

## Creating a graphical application

So far, you have used Visual Studio 2015 to create and run a basic console application. The Visual Studio 2015 programming environment also contains everything you need to create graphical applications for Windows 10. These templates are referred to as Universal Windows Platform (UWP) apps because they enable you to create apps that function on any device that runs Windows, such as desktop computers, tablets, and phones. You can design the user interface (UI) of a Windows application interactively. Visual Studio 2015 then generates the program statements to implement the user interface you’ve designed.

Visual Studio 2015 provides you with two views of a graphical application: the *design view* and the *code view*. You use the Code and Text Editor window to modify and maintain the code and program logic for a graphical application, and you use the Design View window to lay out your UI. You can switch between the two views whenever you want.

In the following set of exercises, you’ll learn how to create a graphical application by using Visual Studio 2015. This program displays a simple form containing a text box where you can enter your name and a button that when clicked displays a personalized greeting in a message box.

*If you want more information about the specifics of writing UWP apps, the final few chapters in Part IV of this book provide more detail and guidance.*

## Create a graphical application in Visual Studio 2015

- 1. Start Visual Studio 2015 if it is not already running.
- 2. On the File menu, point to New, and then click Project.
  The New Project dialog box opens.
- 3. In the left pane, expand the Installed node (if it is not already expanded), expand Templates, expand Visual C#, expand Windows, and then click Universal.
- 4. In the middle pane, click the Blank App (Windows Universal) icon.

### Note

XAML stands for Extensible Application Markup Language, which is the language that Universal Windows Platform applications use to define the layout for the GUI of an application. You will learn more about XAML as you progress through the exercises in this book.

- 5. Ensure that the Location field refers to the \Microsoft Press\VCSBS\Chapter 1 folder in your Documents folder.
- 6. In the Name box, type Hello.
- 7. Ensure that the Create Directory For Solution check box is selected, and then click OK.

If this is the first time that you have created a UWP application, you might be prompted to enable developer mode for Windows 10. Depending on your device and your version of Windows 10, you may or may not be able to enable developer mode through the user interface. For more guidance on enabling developer mode, see “Enable your device for development” at https://msdn.microsoft.com/library/windows/apps/xaml/dn706236.aspx.
