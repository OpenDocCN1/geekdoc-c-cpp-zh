
This should give you some idea of how complicated the file structure for a project can be. For this relatively simple application, three form files and one class file were created by the developer. New namespaces and the Program.cs file were added to the project automatically. The Program.cs file contains the C# code that starts the application and runs the first form of the application.

## How to work with Visual Studio's windows

In Figure 1-11, the Toolbox isn't visible. Instead, it's hidden at the left side of the window. Then, when you need the Toolbox, you can move the mouse pointer over its tab to display it. This is one of the ways that you can adjust the windows in the IDE so it's easier to use. This figure also presents many of the other techniques you can use.

By default, the Toolbox is docked at the edge of the application window and so it appears as a tab. To display a hidden window, you place the mouse pointer over its tab. If you want the window to remain open when you move the mouse off the window, click the window's Auto Hide button. The Auto Hide button looks like a pushpin, as illustrated by the button near the upper right corner of the Properties window. To hide the window again, click its Auto Hide button.

You can also undo a window so it floats in the middle of the IDE, outside the IDE, or even on a separate monitor. That includes windows that are docked at the edge of the IDE, like the Toolbox and the Solution Explorer, as well as the tabbed windows in the middle of the IDE. To undo one of these windows, you drag it by its title bar or tab or double-click its title bar or tab. In this figure, for example, you can see that the Solution Explorer window that was docked at the right side of the IDE is now floating in the middle of the IDE. Although we don't recommend this arrangement of windows, it should give you an idea of the many ways that you can arrange them.

If you experiment with these techniques for a few minutes, you'll see that they're easy to master. Then, as you get more comfortable with Visual Studio, you can adjust the windows so they work best for you.

## Visual Studio with two floating windows and a hidden window

![](img/3148667e42d4db35b3d08576aaa1fa01_44_0.png)

- Active Files list
- Auto Hide button
- Close buttons
- Docked window
- Floating window
- Window tabs
- Hidden window

## How to rearrange windows

- To close a window, click its Close button. To reread, click its button in the Standard toolbar (if one is available) or select it from the Menu view.
- To undo a docked window so it floats on the screen, drag it by its title bar away from the edge of the application window or double-click it.
- To dock a floating window, drag it by its title bar onto one of the positioning areas that become available. Or, hold the Ctrl key and double-click its title bar to return it to its docked location.
- To hide a docked window, click its Auto Hide button. Then, the window is displayed as a tab at the edge of the screen, and you can display it by placing the mouse pointer over the tab. To change it back, click it and then click the Auto Hide button.
- To size a window, place the mouse pointer over an edge or a corner of the window, and drag it.
- If two or more windows are grouped into tabbed windows, you can display any window in the group by clicking on its tab. To close a tabbed window, you can click on its Close button or right-click on its tab and select the Close command.
- If you dock, undock, hide, or unhide a tabbed window, all the windows in the group are docked, undocked, hidden, or unhidden.

## Warning

- Be careful when modifying the window layout. It's easy to rearrange your windows, it can be hard to get them back the way they were.

Figure 1-11 How to work with Visual Studio's windows

## How to test a project

When you develop a project, you design the forms using the Forms Designer and you write the C# code for the project using the Code Editor. Then, when you're ready to test the project to see whether it works, you need to build and run the project.

## How to build a project

Figure 1-12 shows how to build a project. One way way to do that is to pull down the Build menu and select the Build Solution command. If the project doesn't contain any coding errors, the C# code is compiled into the Intermediate Language for the project and it is saved on disk in an assembly. This assembly can then be run by the Common Language Runtime.

Usually, though you don't need to build a project this way. Instead, you can simply run the project, as described in the next topic. Then, if the project hasn't been built before, or if it's changed since the last time it was built, Visual Studio builds it before running it.

## How to run a project

The easiest way to run a project is to click the Start Debugging button that's identified in figure 1-12. Then, the project is built if necessary, the Intermediate Language is executed by the Common Language Runtime, and the first (or only) form of the project is displayed. In this figure, for example, you can see the first form that's displayed when the Financial Calculations project is run. This form contains two buttons that you display the other forms of the project.

To test the project, you try everything that the application is intended to do. When data is entered, you test the application. When you're satisfied that the application works, you can exit it by clicking the button in the upper right corner of the form. If the application doesn't work, you need to fix it, you'll learn more about that in chapter 3.

## The form that's displayed when the Financial Calculations project is run

![](img/3148667e42d4db35b3d08576aaa1fa01_46_0.png)

## How to build a project

- Use Build->Build Solution. Or, right-click the project in Solution Explorer and select the Build command. This builds the Intermediate Language for the project and saves it in an assembly.

## How to run a project

- You can run a project by clicking the Start Debugging button in the Standard toolbar or by pressing F5. Then, the project is first built and run. As a result, it isn't necessary to use the Build command before you run it.

## Two ways to exit from a project that is running

- Click the Close button in the upper right of the startup form.
- Click the button control that's designed for exiting from the application.

Figure 1-12 How to build and run a project

## How to convert projects and change .NET Framework versions

If you've developed projects in earlier versions of C#, you may want to convert them to C# 2010 so that you can take advantage of the new features it provides. That's why Visual Studio 2010 provides a tool that helps you convert applications from a previous version of C#. Once you do that, you can change the version of the .NET Framework the converted applications use so you have access to the new features.

## How to convert projects created in earlier versions of C#

If you've developing applications in C# 2002 or 2003, you'll see that C# 2010 uses a different format for its projects. Because of that, projects created with C# 2002 or 2003 must be converted to C# 2010 if you want to work with them in that environment. Although C# 2005 and 2008 use the same project format as C# 2010, certain aspects of these projects need to be converted to C# 2010 to work with them in that environment.

Figure 1-13 presents a basic procedure for converting C# 2002, 2003, 2005, or 2008 projects. When you open one of these projects, Visual Studio automatically starts the Conversion Wizard. You can see the first page of this wizard in this figure. To convert the project, just click the Next button and follow the instructions. When the wizard is done, you can usually run the project without any further changes.
