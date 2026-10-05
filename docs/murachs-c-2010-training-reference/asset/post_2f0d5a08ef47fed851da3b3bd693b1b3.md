
# How a C# application is compiled and run

![](img/3148667e42d4db35b3d08576aaa1fa01_32_0.png)

##

1. The programmer uses Visual Studio to create a project, which includes C# source files. In some cases, a project will also contain other types of files, such as graphic image, sound, or text files.
2. The C# compiler builds (translates) the C# source code for a project into Microsoft Intermediate Language (MSIL), or just Intermediate Language (IL). This language is stored on disk in an assembly that also contains references to the required classes. An assembly is an executable file that has an .exe or .dll extension.
3. The assembly is run by the .NET Framework's Common Language Runtime. The CLR manages all aspects of how the assembly is run, including converting the Intermediate Language to native code that can be run by the operating system, managing memory for the assembly, and enforcing security.

## About projects and solutions

- A solution is a container that can hold one or more projects.

Figure 1-5 How a C# application is compiled and run.

# A tour of the Visual Studio IDE

With that as background, you're ready to take a tour of the Visual Studio IDE. Along the way, you'll learn some of the basic techniques for working in this environment. You'll also see how some of the terms that you just learned are applied within the IDE.

### How to start Visual Studio

Figure 1-6 shows how to start Visual Studio and what the opening view of the IDE looks like. In the main window within the IDE, a Start Page is displayed. This page lets you open projects, create new ones, and get news and information about Visual Studio. Often, though, this page just slows you down, I usually close this page, which you'll learn how to do in figure 1-11.

Note that the first time you start Visual Studio, you will be asked to select the default environment settings. Then, you can choose C# Development Settings so your menus will look like the ones in this book.

This figure demonstrates that there are some minor differences between the Visual Studio C# 2010 Express Edition and the other editions of Visual Studio. In this case, you access C# 2010 Express a little differently from the Windows Start menu, and the Start Page for C# 2010 Express is somewhat different from the Start Page for the other editions. Both of these differences are trivial, though, as are most of the differences between C# 2010 Express and the other editions.

Throughout this book, all of the screen illustrations are based on the Professional Edition of Visual Studio 2010. Whenever the Express Edition varies in any way that is likely to confuse someone who's using it, though, we will carefully detail the differences. As you would expect, the Professional Edition also has features that aren't available with the Express Edition, and will of course point out those limitations too.

In general, though, using the C# 2010 Express Edition is an excellent way to get started with Visual Studio 2010. As you will see, you can develop professional applications with that edition. And both the skills that you learn and the applications that you develop will work whenever you want to upgrade to one of the other editions.

# Chapter 1: How to get started with Visual Studio

## The Start Page that's displayed when you start Visual Studio

![](img/3148667e42d4db35b3d08576aaa1fa01_34_0.png)

### Description

- To start Visual Studio, open the Windows Start menu, then locate and select Microsoft Visual Studio 2010. Typically, this item is in the Visual Studio 2008 submenu of the All Programs menu.
- To make it easier to start Visual Studio, you may want to create a shortcut for Visual Studio 2010 or Microsoft Visual C# 2010 Express Edition and place it on the desktop.
- When Visual Studio starts, a Start Page is displayed in the Visual Studio IDE. You can use this page to open recent projects, create new ones, start tutorials, and so on.

### Variations between the Professional and Express Editions

- In this book, all of the screen illustrations are from the Professional Edition of Visual Studio 2010. In general, these illustrations are the same for both the Professional Edition and the Visual C# 2010 Express Edition.
- Whenever the Express Edition differs significantly from the Professional Edition, we'll point out the differences.

### Express Edition difference

- To start Visual Studio, open the Windows Start menu and select Microsoft Visual C# 2010 Express Edition. Typically, this item is in the All Programs menu.

Figure 1-6 How to start Visual Studio.

# How to open or close an existing project

To open a project, you can use the File→Open→Project/Solution command to display the dialog box shown in 1-7. From this dialog box, you can locate and open your C# projects. You can also open a recently used project using the File→Recent Projects command.

In case you're not familiar with this notation, File→Open→Project/Solution means to pull down the File menu from the menu bar, select the Open submenu, and select the Project/Solution command. Usually, you only need to pull down one menu and select a command. Sometimes, you need to go from a menu to one or more submenu and then to the command.

The Open Project dialog box in this figure shows both the solution file and the project file for a project. As this figure explains, a project can contain multiple files, including the for source code. A solution, on the other hand, is a container that holds one or more projects.

For the applications in this book, a solution contains just a simple project. In that case, there's not much distinction between a solution and a project. However, a solution can contain more than one project. This is often the case for large applications that are developed by teams of programmers.

With a multi-solution project, programmers can work independently on the projects that make up the solution. In fact, the projects don't even have to be written in the same language. For example, a solution can contain two projects, one in C#, the other in Visual Basic.

At this point, you might wonder whether you should open a project or a solution. In this figure, for example, FinancialCalculations.sln is a solution and FinancialCalculations.csproj is a C# project. In most cases, it doesn't matter whether you open the solution or the project. Either way, both the solution and the project will be de-ed.

# The Open Project dialog box

![](img/3148667e42d4db35b3d08576aaa1fa01_36_0.png)

## Project and solution concepts

- Every C# project has a project file with an extension of .csproj that keeps track of the files that make up the project and records various settings for the project. In this figure, the project file is just above the line.
- Every solution has a solution file with an extension of .sln that keeps track of the projects that make up the solution. In this figure, the solution file is highlighted.
- When you open a project file, Visual Studio opens the solution that contains the project. And when you open a solution file, Visual Studio automatically opens all the projects contained in the solution. So either way, both the project and the solution are opened.
- Sometimes the project and solution files are stored in the same directory. Sometimes the project file is stored in a subdirectory of the directory that contains the solution file.
