
## SET THE APPLICATION ICON PROPERTY

If Hello, World isn't still open from the last exercise, open it from the Visual Studio Start screen (it will be listed on the left side under Recent Project or from the File menu). Display the Project Properties using any of the techniques you've learned, and then select the Application tab.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_85_0.png)

We'll set the icon here.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_85_1.png)

Click here to open the dialog.

After you select your icon, Visual Studio will display a thumbnail of it here.

Click the little box with an ellipsis in it, and Visual Studio will display a standard File Open dialog. The first time you open the dialog, Visual Studio will take you to the Microsoft Visual Studio\Common7\IDE folder, which can be a little scary, but just navigate to the folder for the application and choose Conversation.ico (or whichever icon file you chose to use).

After you select the icon and click the Open button, Visual Studio will show the icon on the tab.

## 2 BUILD THE APPLICATION

There are a lot of files involved in creating a Visual Studio application. In addition to the source files that you create, the resource files like icons that you create or reference, and the final executable created by the compiler, there are intermediate files that Visual Studio creates for you. When you set properties or resources, you need to tell Visual Studio to re-create some of these “behind-the-scenes” files so that they’re available to other components like the designers. You do that by BUILDING the application.

### THE BUILD MENU

Most of the time you can use Build Solution, which only rebuilds the files that have changed.

Rebuild Solution is a safer, but slower, choice. It rebuilds all the files, whether they’ve changed or not.

Clean Solution removes any intermediate files created by Visual Studio, but doesn’t build the solution. If Rebuild Solution seems to be acting strangely, try cleaning the solution first.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_86_0.png)

These options build and clean just the Project, not the whole Solution. Because our application only has a single project, there isn’t any real difference, but when you have a lot of Projects in a Solution, these alternatives can save a lot of time.

Press F5 or choose Build Solution from the Build menu so that the icon will be available to the WPF Designer.

## 3 SET THE WINDOW PROPERTY

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_87_0.png)

If necessary, double-click MainWindow.xaml in the Solution Explorer to open the WPF Designer. In the Properties window, find the Icon property, select it, and then click the ellipsis button.

After you click the ellipsis in the Properties window, Visual Studio will display the Choose Image dialog. Your new icon will be displayed, but there might not be a thumbnail. It's okay; Visual Studio just hasn't caught up with us.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_87_1.png)

Click on your icon, and then click OK to set the property.

After you click the OK button, Visual Studio will set the property to a long value that begins with pack://application.../. That's just WPF-Speak for “look in the application file”, and we’ll figure out how it all works later when we examine WPF Resources.

## DID IT WORK?

Don't take my word for it. Run the application and find out...

The icon shows up in the window where we set the property...

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_88_0.png)

But not in the window where we didn't.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_88_1.png)

The application executable also uses the icon, as you can see in the bin/debug folder in Windows Explorer.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_88_2.png)

## ONE MORE TIME...

Let's run through the steps to add an application icon one more time...

- 1. Add the icon file to the application in Project Properties.
- 2. Build the application to make the application available in the designers.
- 3. Set the Icon property of the windows where you want the icon displayed.

### TAKE A BREAK

You've finished the first task of this chapter, so take a short break to let it all settle before moving on. But before you go, stop for a minute to think about what you've achieved...

- You created an application that displayed a Window and a MessageBox.
- You changed the appearance of the Window.
- You added a second window to the project, and wrote the code to display it.
- You added an icon to the application and the Window.

That's a lot when you see it listed like that, isn't it? Go, you!

## REVIEW

Just a few exercises before we move on...

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_90_0.png)

Solutions and Projects, Projects and Solutions. One's like a file folder, one's like a filing cabinet. Which is which?

- Solution
- Project

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_90_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_90_2.png)

- List three ways to add a Project:
  - 1. 
  - 2. 
  - 3. 

- List two ways to show the Solution Properties dialog:
  - 1. 
  - 2. 

- List three ways to show Project Properties:
  - 1. 
  - 2. 
  - 3. 

Change the application icon to something else. What happens to the window?

In the walk-through, we only changed the icon of the main window. Add it to the other window in the application, as well.

## TAKE CONTROL

Visual Studio is a Windows application, and for the most part it behaves like any Windows application, with menus and toolbars and document windows where you do your work. But the work you do in Visual Studio is quite specialized, and the IDE adds some special capabilities to make it possible to work just the way you want to work.

This is a document window displayed as a tab, the default view.

You can display documents in tabs, or as separate windows. You can even drag them outside the main IDE window.

Tool windows can be docked to the edge of the IDE window or each other. When docked, they can be opened or closed.

This is a tool window that is docked and closed.

This is a tool window that is docked and open.

This is a document displayed in a floating window. It's not constrained by the Visual Studio IDE window.

Tool windows that are docked to each other are displayed as tabs.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_91_0.png)

## ARRANGING WINDOWS

Like any Windows application, you can control the individual windows in Visual Studio through the View and Window menus or by dragging the title bar of a window.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_92_0.png)

The View menu controls the display of tool windows. (Don't confuse “tool window” with “Toolbox.” The Toolbox is a tool window, but so are the Properties window and the Solution Explorer.)

Do you remember how to open a document window? Double-click on its name in the Solution Explorer.

The Window menu controls the display of open windows in the IDE. The most important item on this menu might be Reset Window Layout, which puts everything back in place when you get things messed up. (And you will, trust me.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_92_1.png)

## ON YOUR OWN

The best way to learn how to control the windows in Visual Studio is to play with them, so take a few minutes to move the Object Browser around. The Object Browser lets you look through a class hierarchy. You'll find out what that means in Chapter 7.

*Remember, you can always start over by choosing Reset Window Layout from the Window menu...*

- 1. Show the Object Browser by selecting its name on the View menu. It will probably display as a tab. If it doesn't, drag its title bar until it does.
- 2. Make it float by dragging its title bar, or selecting Float from the Window menu.
- 3. Dock it to the left side of the screen along with the Toolbox. It will be open when you first dock it, so click the [icon] to collapse it.
- 4. Drag it over so it displays as a tab in the same pane as the Solution Explorer.
- 5. Use Reset Window Layout to put everything back the way it was originally.
- 6. When you're dragging a window around, Visual Studio will display this odd docking widget. Can you work out what each bit does?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_93_0.png)
