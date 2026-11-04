
![](img/d5be6ade75773ca6cec5c78f96a98bb1_55_0.png)

FIGURE 1-8

The drop area just to the left of the mouse represents a tabbed area. If you drop on this kind of target, the window becomes a tab in that area.

> **CUSTOMIZATION MODERATION**
>
> Visual Studio lets you move, dock, float, hide, auto-hide, and tabify windows. If you have multiple monitors, you can float a window and move it to another monitor, giving you a larger editing area. It's so flexible that it can present as many different faces as a politician during an election year.
>
> Feel free to customize the IDE to suit your needs, but if you do, keep in mind that your version of Visual Studio may look nothing like the pictures in this book. To minimize confusion, you may want to keep the IDE looking more or less like Figure 1-7, at least until you get a better sense of which tools will be most useful to you.

## Try It

In this Try It, you prepare for later work throughout the book. You locate web resources that you can use when you have questions or run into trouble. You create and run a program, explore the project's folder hierarchy, and make a copy of the project. You also get a chance to experiment a bit with the IDE, displaying new toolbars, moving windows around, and generally taking the IDE for a test drive and kicking the tires.

- 2. If the Toolbox is auto-hiding (it should be after you first install Visual Studio), hover the mouse over it until it expands. Click the thumbtack to pin it.
- 3. To display the Output window, open the View menu and select Output. Grab the Output window's title bar and drag it around. Move it over some drop targets to see where it lands. When you're finished, drop it at the bottom of the IDE as shown in Figure 1-7.

### Run the program.

- 1. Press F5 or open the Debug menu and select Start Debugging.
- 2. Try out the form's minimize, maximize, and close buttons and the commands in the form's system menu. Move the form around and resize it. Marvel at the fact that you didn't need to write any code!

### Find the program's executable, copy it to the desktop, and run it there.

- 1. Start File Explorer and navigate to the location that you specified when you created the new program.
- 2. There you should find a folder named after the program. Open that folder and examine the files inside. Notice the .sln file that you can double-click to reopen the solution in Visual Studio. Notice also the bin, obj, and .vs directories.
- 3. Enter the bin directory and move into its Debug subdirectory. It contains several files including the executable, named after the program but with the .exe extension. Right-click the executable and select Copy.
- 4. Right-click the desktop and select Paste to copy the executable to the desktop.
- 5. Double-click the copy of the executable on the desktop.

### Copy the project folder to a new location and make changes to the copy.

- 1. In File Explorer, go to the directory that contains the project folder.
- 2. Right-click the project's folder and select Copy.
- 3. Right-click the desktop and select Paste to copy the project folder.
- 4. Open the copied project folder and double-click the .sln file to open the copied project in Visual Studio. If the form doesn't open in the Form Designer (#4 in Figure 1-7), look in Solution Explorer and double-click the file Form1.cs.
- 5. In the Form Designer, grab the handle on the form's lower-right corner and resize the form to make it tall and skinny.
- 6. Run the modified program. Then go back to the original project (which should still be running in another instance of Visual Studio) and run it. Notice that the two versions display forms of different sizes.

### Compress the project folder to make a backup.

- 1. In Visual Studio, close the project. (Or close Visual Studio.)
- 2. In File Explorer, return to the project's folder and delete the bin, obj, and .vs directories. (Note that you can't delete the bin directory if Visual Studio has the project open.)
- 3. Move up one level to the directory that contains the project folder. Right-click the folder, expand the Send To submenu, and select Compressed (Zipped) Folder.
- 4. E-mail copies of your first project to all of your friends and relatives. I'm sure they'll thank you!

## Exercises

- 1. Build a solution that contains two projects. (Create a project named Project1. Check the Create Directory for Solution box and name the solution TwoProjects. Then open the File menu, expand the Add submenu, and select New Project to add a new project named Project2.)
- 2. This lesson explains only a tiny fraction of the ways you can customize Visual Studio. Try another one by making your own toolbar. Select the Tools menu's Customize command. On the Toolbars tab, click the New button, and name the new toolbar MyTools. On the Commands tab, select the Toolbar radio button and then select the new toolbar from the dropdown list. Now use the Add Commands button to add some commands to the toolbar.
- 3. This lesson also describes only a few of the windows Visual Studio offers. Use the menus to find and display the Output, Immediate, Error List, and Task List windows. Put them all in tabs at the bottom of Visual Studio (#8 in Figure 1-7).
- 4. Some tools are available only when Visual Studio is in a certain state. Look in the Debug menu's Windows submenu. Then start the program and look there again. Most of those windows are useful only when the program is running and you are debugging it. (I talk about some of them in later lessons.)
- 5. [WPF] Create a new WPF application. Run it side by side with a Windows Forms application. What are the differences? (Hint: There shouldn't be many and they should be cosmetic. You learn about more important but less obvious differences in later lessons.)

> NOTE Please select the videos for Lesson 1 online at www.wrox.com/go/csharp24hourtrainer2evideos.

## 2 Creating Controls

Way back in the computer stone ages, when programmers worked by candlelight on treadle-powered computers and hand-carved wooden monitors, input and output were very simple. The computer wrote text in toxic green on the bottom of a monitor and the text scrolled up as the monitor became full. The user typed on a keyboard to enter text at a single input prompt, and that was about it. Multiple windows performing useful work simultaneously, mice, and forms displaying many labels and textboxes, buttons, scrollbars, and full-color images existed only in the fevered dreams of science-fiction writers.

Today these things are so commonplace that we take them completely for granted. They appear in desktop software, web pages, laptops, handheld computers, and even cell phones.

Building these sorts of objects in the old days would have been extremely difficult, but today it's practically trivial to add them to your application.

You already saw in Lesson 1 how easy it is to make an application (albeit a trivial one) that displays a form that runs independently of the others on the computer. It's almost as easy to use labels, textboxes, buttons, scrollbars, images, menus, popups, and everything else that makes up a modern application.

C# makes all of these objects and more available as controls.

In this lesson, you learn how to add controls to a form. You learn how to size, position, and arrange controls. You also learn how to use a control's properties to change its appearance and behavior at design time and at run time. When you're done with this lesson, you'll be able to build a professional-looking form.

### Understanding Controls

A control is a programming entity that combines a visible appearance on the screen and code to manage it. The code defines the control's appearance and behavior.

For example, a TextBox control displays a blank area on the screen where the user can type information. The code inside the control determines how the control draws itself and provides normal textbox features such as multiline or single-line behavior; scrolling and scrollbars displayed as needed; copy, cut, and paste; a context menu displayed when you right-click the control; the ability to navigate when the user presses the Tab key; and much more.

### What's in a Name?

By convention, in C# the names of control types (and other types) use Pascal casing where multiple words are strung together with the first letter of each word capitalized; for example, TextBox, ProgressBar, Button, and PictureBox.

In addition to controls, C# provides components. A component is similar to a control except it has no visible piece on the form. For example, the Timer component acts as a clock to let the program do something at regular intervals. The Timer interacts with the program but doesn't display anything visible to the user. (Some components such as ErrorProvider and ToolTip may display visible effects on the screen, but the components themselves are not visible on the form.)

The features of controls (and components) fall into three categories: properties, methods, and events.

### Properties

A property determines the appearance and state of a control. If a Car were a control, its properties would be things like Color, TransmissionType, CurrentSpeed, and NumberOfCupHolders. Your program could set a Car's Color to HotPink (to attract the attention of other drivers) or set its CurrentSpeed to 110 (to attract the attention of the police).

For a programming example, the TextBox control has a Font property that determines the font it uses and a ForeColor property that determines the color of its text.

### Methods

A method is a feature of a control that makes the control perform some action. Your code can call a method to make the control do something. For example, the Car control might have methods such as Start, Stop, EjectPassenger, and OilSlick. Your program could call the OilSlick method to make the car spray oil out the back so you can escape from spies.

### Events

An event occurs when something interesting happens to the control. The control raises or fires the event to tell the program that something happened. For example, a Car might have RanOutOfGas and Crashed events. The Car control would raise the Crashed event to tell the program that the
