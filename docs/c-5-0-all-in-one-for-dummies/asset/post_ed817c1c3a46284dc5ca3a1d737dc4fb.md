
doing about any kind of programming you can imagine, from web-based databases to cryptography to the humble Windows dialog box.

Microsoft would claim that .NET is much superior to Sun's suite of web tools based on Java, but that's not the point. Unlike Java, .NET doesn't require you to rewrite existing programs. A Visual Basic programmer can add just a few lines to make an existing program web-knowledgeable (meaning that it knows how to get data off the Internet). .NET supports all the common Microsoft languages — and hundreds of other languages written by third-party vendors. However, C# is the flagship language of the .NET fleet. C# is always the first language to access every new feature of .NET.

## What is Visual Studio 2012? What about Visual C#?

(You sure ask lots of questions.) The first "Visual" language from Microsoft was Visual Basic. The first popular C-based language from Microsoft was Visual C++. Like Visual Basic, it had Visual in its name because it had a built-in graphical user interface (GUI — pronounced "GOO-ee"). This GUI included everything you needed to develop nifty-gifty C++ programs.

Eventually, Microsoft rolled all its languages into a single environment — Visual Studio. As Visual Studio 6.0 started getting a little long in the tooth, developers anxiously awaited version 7. Shortly before its release, however, Microsoft decided to rename it Visual Studio .NET to highlight this new environment's relationship to .NET.

That sounded like a marketing ploy to me — until I started delving into it. Visual Studio .NET differed quite a bit from its predecessors — enough to warrant a new name. Visual Studio 2012 is the sixth-generation successor to the original Visual Studio .NET. (Book IV is full of Visual Studio goodness, including instructions for customizing it.)

![](img/80ff26f06fc9ab951e1cd4257b867366_39_0.png)

Microsoft calls its implementation of the language Visual C#. In reality, Visual C# is nothing more than the C# component of Visual Studio. C# is C#, with or without Visual Studio.

Okay, that's it. No more questions. (For now, anyway.)

## Creating Your First Console Application

Visual Studio 2012 includes an Application Wizard that builds template programs and saves you a lot of the dirty work you'd have to do if you did everything from scratch. (I don't recommend the from-scratch approach.)

Typically, starter programs don't really do anything — at least, not anything useful. (Sounds like most of my programs.) However, they do get you beyond that initial hurdle of getting started. Some starter programs are reasonably sophisticated. In fact, you'll be amazed at how much capability the App Wizard can build on its own, especially for graphical programs.

This starter program isn't even a graphical program, though. A console application is one that runs in the "console" within Windows, usually referred to as the DOS prompt or command window. If you press Win+R and then type cmd, you see a command window. It's the console where the application will run.

The following instructions are for Visual Studio. If you use anything other than Visual Studio, you have to refer to the documentation that came with your environment. Alternatively, you can just type the source code directly into your C# environment. See the Introduction to this book for some alternatives to Visual Studio.

![](img/80ff26f06fc9ab951e1cd4257b867366_40_0.png)

## Creating the source program

To start Visual Studio, press the Windows button on your keyboard and type Visual Studio. Visual Studio 2012 appears as one of the available options.

Complete these steps to create your C# console app:

- 1. Open Visual Studio 2012 and click the New Project link, shown in Figure 1-1.

![](img/80ff26f06fc9ab951e1cd4257b867366_40_1.png)

Figure 1-1: Creating a new project starts you down the road to a better Windows application.

Visual Studio presents you with lots of icons representing the different types of applications you can create, as shown in Figure 1-2.

![](img/80ff26f06fc9ab951e1cd4257b867366_41_0.png)

Figure 1-2:
The Visual Studio App Wizard is eager to create a new program for you.

![](img/80ff26f06fc9ab951e1cd4257b867366_41_1.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_41_2.png)

- 2. In this New Project window, click the Console Application icon.

Make sure that you select Visual C# — and under it, Windows — in the Project Types pane; otherwise Visual Studio may create something awful like a Visual Basic or Visual C++ application. Then click the Console Application icon in the Templates pane.

Visual Studio requires you to create a project before you can start entering your C# program. A project is a folder in which you throw all the files that go into making your program. It has a set of configuration files that help the compiler do its work. When you tell your compiler to build (compile) the program, it sorts through the project to find the files it needs in order to re-create the executable program.

![](img/80ff26f06fc9ab951e1cd4257b867366_41_3.png)

- 3. The default name for your first application is ConsoleApplication1, but change it this time to Program1 by typing in the Name field.

The default place to store this file is somewhere deep in your Documents directory. Maybe because I'm difficult (or maybe because I'm writing a book), I like to put my programs where I want them to go, not necessarily where Visual Studio wants them. To simplify working with this book, you can change the default program location. Follow these steps to make that happen:

- a. Choose Tools→Options.

The Options dialog box opens. You may have to check the Show All Options box.

- b. Choose *Projects and Solutions→General.*
- c. Select the new location in the *Projects Location* field and click **OK**.

    ( I recommend C:\C# Programs for this book.)

You can create the new directory in the Projects Location dialog box at the same time. Click the folder icon with a small sunburst at the top of the dialog box. (The directory may already exist if you've installed the example programs from the website.)

You can see the Options dialog box in Figure 1-3. Leave the other fields in the project settings alone for now. Read more about customization of Visual Studio in Book IV.

![](img/80ff26f06fc9ab951e1cd4257b867366_42_0.png)

**Figure 1-3:** Changing the default project location.

- 4. Click the **OK** button.

After a bit of disk whirring and chattering, Visual Studio generates a file named *Program.cs*. (If you look in the window labeled *Solution Explorer*, you see some other files; ignore them for now. If Solution Explorer isn't visible, choose *View→Solution Explorer*.)

(C# source files carry the extension `.cs`. The name *Program* is the default name assigned for the program file.

The contents of your first console app appear this way:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
```

```csharp
namespace Program1
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

![](img/80ff26f06fc9ab951e1cd4257b867366_43_0.png)

Along the left edge of the code window, you see several small plus (+) and minus (−) signs in boxes. Click the + sign next to using ... This expands a code region, a handy Visual Studio feature that minimizes clutter. Here are the directives that appear when you expand the region in the default console app:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Regions help you focus on the code you're working on by hiding code that you aren't. Certain blocks of code — such as the namespace block, class block, methods, and other code items — get a +/- automatically without a #region directive. You can add your own collapsible regions, if you like, by typing #region above a code section and #endregion after it. It helps to supply a name for the region, such as Public methods. This code section looks like this:

```
#region Public methods
... your code
#endregion Public methods
```

![](img/80ff26f06fc9ab951e1cd4257b867366_43_1.png)

This name can include spaces. Also, you can nest one region inside another, but regions can't overlap.

For now, using System; is the only using directive you really need. You can delete the others; the compiler lets you know whether you're missing one.

## Taking it out for a test drive

To convert your C# program into an executable program, choose Build→ Build Program1. Visual Studio responds with the following message:

```
- Build started: Project: Program1, Configuration: Debug Any CPU -

Csc.exe /noconfig /nowarn ... (and much more)

Compile complete -- 0 errors, 0 warnings

Program1 -> C:\Program Files\... (and more)==Build: 1 succeeded or up-to-date, 0 failed, 0 skipped==
```

The key point here is the 1 succeeded part on the last line.
