
## Exploring the New Project dialog box

I start with a breakdown of the New Project dialog box, shown in Figure 1-2. This screen is an important part of the usability of Visual Studio. You open it by clicking the New Project link on the setup page.

The section of the dialog box to the far left is a tree-view selector, similar to the one in Outlook. You have three options — Recent Templates, Installed Templates, and Online Templates. Installed Templates is selected. These templates, as Visual Studio calls them, are project types.

Within the selector is a WPF-style tree viewer. Instead of maples and oaks, this tree viewer has all the project categories described in upcoming sections of this chapter.

If you click, for example, the Visual C# option in the tree view, all the projects for Visual C# appear in the window just to the right. If you click one of the suboptions, just those project types — for Visual C# — appear.

To specify the version of the .NET Framework you would like to develop for, you can use the drop-down list just above the project list that currently says .NET Framework 4.5. To change the sorting options, use the Sort By: drop-down list directly to the right. One more step to the right, and you can change your view options (icon size in the dialog box).

![](img/80ff26f06fc9ab951e1cd4257b867366_534_0.png)

Figure 1-2: So many (project) options!

In the upper-right corner is a search box, which isn't as silly as it sounds given the large number of templates now in Visual Studio. Just below the search box is the description panel, where you can see a text description of the selected project type.

At the bottom are three important text boxes:

- **Name:** The name of this project.
- **Location:** The path to the project file.
- **Solution:** The name of the solution. Solutions are collections of projects.

For more about solutions and projects, see the next section.

## Understanding solutions and projects

Visual Studio project files, and the solutions that love them, are a constant topic of interest to Microsoft developers. You work on one solution at a time, with a number of projects within. How you organize your solutions and their projects will make or break you when it comes to finding something.

You can think of solutions as folders that hold projects. They're just folders with special properties. In fact, note the check box in the lower right corner of Figure 1-2. It's the one labeled Create Directory for Solution. That's what I mean — the solution is really an organizational "folder" for the projects.

Projects are where you put the code files for your programs. They store all kinds of things, like references to the .NET Framework, resources like graphics or files, and what file should be used to start the project.

Solutions do the same thing for projects that projects do for files. They keep the projects in a folder and store certain properties. For instance, they store which project should be started when debugging starts.

Neither the project nor the solutions have much to do with a finished program. They are just simple organizational structures for Visual Studio. The installation of the finished program is determined by the setup project.

In reality, the solution is more than a folder. It's a file in a folder that is used by Visual Studio to manage the developer experience. So, inside the folder for the solution is a file describing the projects within and then a bunch of folders with the projects themselves.

There are files for the projects, too — files that describe the resources and references for the project. They are all XML files that contain text references to the values that you set using Visual Studio.

When developing in Visual Studio, you shouldn't worry about that. In 14 years of working in various versions of Visual Studio, I have had to look at a solution or project file only a few times, and only in special situations. Knowing how they work, however, will help you design your project structure.

The way I work is to look at what I want to be a finished program and consider it a solution. Above that, I have a client folder. The result looks like Figure 1-3.

![](img/80ff26f06fc9ab951e1cd4257b867366_536_0.png)

Figure 1-3: My preferred project structure.

This strategy keeps me much more organized and works with the Visual Studio model. All I have to do is use the Browse button to change the location of the project and solution. It also helps to make the main project of a solution first (like the user interface) before the rest of the solution.

## A brief survey of the available project categories

The following list describes the project types listed in the New Project dialog box in Visual Studio. These kinds of finished programs are ones you can make using the installed templates.

- **Windows Store Projects:** These are full-screen, touch-first applications for Windows 8. They can be developed in C#, VB.NET, C++, or HTML5.
  - *Blank App*: Just what it sounds like, a barebones Windows Store app.
  - *Grid and Split App*: Two pre-templated sample apps for Windows Store that show off the list view.
  - *Class Library for Windows Store*: Helps you build a .NET DLL.
  - *Windows Runtime Component*: The templates to build WinMD components for Windows 8.
  - *Unit Test Library for Windows Store*: The add-on project for unit testing in Windows 8.
- **Windows Projects:** Windows projects in Visual C# are programs that compile into a running program, like Microsoft Word, or Visual Studio itself. The projects include
  - *Windows Forms Application*: The classic "program." Compiles into a program that runs with its own window and with a red close box (with the little X in it) to exit. This is the original Windows Program style, gradually being replaced by Windows Presentation Foundation.
  - *Class Library*: Makes a DLL when you're all done. This is the basis of the .NET Framework, and COM before that. It's used to make blocks of reusable code.
  - *WPF Application*: The new "program." Also compiles into an EXE, but uses a new user interface format called Windows Presentation Foundation. I cover this in depth in Book V.
  - *WPF Browser Application*: Just like a WPF application but runs in Internet Explorer. This is *not* a Silverlight application; it's an XBAP application, short for XAML Browser Application. It has a smaller set of available user interface toys but is still powerful.
  - *Console Application*: These EXEs are designed to be run from a command prompt (or Windows Explorer).
  - *WPF Custom Control Library*: This is a way to make actual custom controls that appear in the toolbox that you can use in your WPF applications.
  - *Empty Project*: Just what it sounds like — a project that's empty, poetic. It's used to build a program for which you don't have a template.
  - *Windows Services*: These programs appear in the Services control panel. Didn't know you could make those with .NET? You aren't alone. It's a powerful feature that few people know about. Windows Services are essentially terminate-and-stay-resident, or TSR, programs. (Remember those from your DOS days? They stay in memory.)
  - *WPF User Control Library*: The finished product of this looser control format doesn't appear in the toolbox but is much easier to build because it doesn't require coding the whole thing in C#.
  - *Windows Forms Control Library*: Like the WPF control library but for Windows Forms. It helps to build a control that you can use from the toolbox.
- **Web Projects:** Web projects are programs that require a server to run (well, usually) and are used from the browser. They render HTML to the browser, rather than fancy formats like Silverlight. Projects include
  - ASP.NET Web Application: This is the centerpiece of the web development space. It creates an application that can run on IIS, which presents a web page to the user.
  - ASP.NET Web Service Application: This is a class library for service-oriented applications. If you're going to distribute applications over several machines or provide broadly distributed applications, this project type will provide a standards-based implementation for your service offerings.
  - ASP.NET AJAX Server Control: Asynchronous JavaScript and XML (AJAX) is a development style that provides a significant quantity of user interactions within the web browser. This allows you to build controls that support this pattern.
  - WCF Service Application: This project belongs in the Communication Foundation section. It's like the ASP.NET Web Service Application, except it provides a number of different standards-based implementations for your service offerings. ASP.NET web services only provide one.
  - ASP.NET Server Control: This web control would appear in the toolbox, enabling you to drag the selected functionality right onto the web page in development.
  - ASP.NET AJAX Server Control Extender: This control extends the functionality of another AJAX control. It targets a control and adds a feature.
  - Dynamic Data LINQ to SQL Web Application: This is an ASP.NET web application that uses LINQ to make a data-active web page.
  - Dynamic Data Entities Web Application: This ASP.NET web application uses ADO.NET Data Entities to make a data-active web page.
- **Office Projects:** Office projects are part of the Visual Studio Tools for Office package and use Office as a platform instead of Windows or a web browser. To find out more, look at the book I coauthored with Peter Jaunovich, Office Development For Dummies. Office Projects include
  - Excel 2010 Workbook: Has a Microsoft Excel Workbook (a collection of Excel worksheets) as an output.
  - Word 2010 Template: Has a Microsoft Word 2007 template (a .dot file) as an output.
