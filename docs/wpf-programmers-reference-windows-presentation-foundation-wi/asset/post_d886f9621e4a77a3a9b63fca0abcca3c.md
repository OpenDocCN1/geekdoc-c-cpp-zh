
# SUMMARY

Visual Studio provides the basic tools that you need to build WPF applications. The Window Designer lets you build the XAML interface, and the Code Editors let you create the C# or Visual Basic code that sits behind the controls.

While you can get the job done with Visual Studio, it makes some tasks rather cumbersome. For example, it doesn't provide editors for complex objects such as visual brushes, and it doesn't provide any help for creating property animations. To build these things in Visual Studio, you need to write the XAML code yourself.

The Expression Blend tool described in the next chapter provides some useful tools that are missing from Visual Studio. For example, it lets you create complex visual brushes and property animations interactively rather than by writing XAML code. You'll still want to use Visual Studio to write the code behind the interface, but Expression Blend can make some chores a lot easier.

# 3 Expression Blend

Visual Studio provides an excellent environment for writing C# or Visual Basic but a mediocre environment for creating XAML interfaces. Expression Blend provides the opposite experience: It is a fine environment for creating XAML interfaces but a lackluster tool for creating C# and Visual Basic code-behind.

Fortunately, Expression Blend is nicely integrated with Visual Studio, so you can switch back and forth between the two tools as needed.

This chapter explains how you use Expression Blend Presentation Foundation (WPF) user interfaces (UI). It explains how to start a new project, add controls to a window, specify basic control properties, and create simple animations.

# INSTALLING EXPRESSION BLEND

To get the most out of this chapter, you'll need to install Expression Blend. Unfortunately Expression Blend is expensive and, unlike Visual Studio, has no Free edition. Fortunately you can download a 60-day trial. You can learn more about Expression Blend or download the trial version at expression.microsoft.com/cc13653.aspx.

Expression Blend is a huge and complicated application with lots of powerful features for building XAML user interfaces, and this book only covers the minimum necessary to build WPF applications. For more detailed information about the intricacies of Expression Blend, consult a book that focuses solely on Expression Blend such as Foundation Blend 3 with Silverlight (Victor Gaudioso, friends of ED, 2009) or Microsoft Expression Blend Unleashed (Brennan Williams, Sams, 2008).

> If you have lots of previous experience with Expression Blend, most of this will be familiar and easy to understand, so you might want to skip this chapter.

# NEW PROJECTS

Starting a WPF project in Expression Blend is easy. Open the File menu and select “New Project” to display the New Project dialog shown in Figure 3-1.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_75_0.png)

FIGURE 3-1

Select the type of project that you want to build. Enter a descriptive name for the project and the directory where you want to build it. Select the programming language that you want to use for code-behind (C# or Visual Basic) and click OK to create the project.

> If you only want to make loose XAML pages, select the WPF Application project and pick either programming language. Later you can copy the XAML file you build out of the project’s directory and discard the rest.

Figure 3-2 shows Expression Blend displaying a typical WPF application.

> ALL MAY NOT BE AS IT APPEARS
Expression Blend may not appear exactly as shown in the figures in this chapter. While it is not configurable as Visual Studio, there are still plenty of ways to resize, collapse, hide, or otherwise change the appearance of Expression Blend’s windows. If you can’t find a window, look for its title next to an arrow indicating that it has been collapsed. If you still can’t find it, look in the Window menu.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_76_0.png)

The following lists name the numbered parts that are highlighted in Figure 3-2.

- 1. Assets window
- 2. Projects window tab
- 3. Window Designer, Design view
- 4. Window Designer, XAML view
- 5. Properties window
- 6. Resources window tab
- 7. Objects and Timeline
- 8. Triggers window tab
- 9. Control Toolbox

The following sections describe each of the parts of Figure 3-2 in greater detail.

> TERMINOLOGY
The Window Designer’s Design view is also called the artboard.

# ASSETS WINDOW

The Assets window lists tools that you can use while building a project. Select a category on the left (Project, Controls, Styles, etc.) to see items that fit the category on the right. For example, in Figure 3-2 the Controls category is selected so the list on the right shows common controls. You can expand the Controls category to pick from the sub-categories All, Data Visualization, and Panels.

# PROJECTS WINDOW TAB

The Project window lists the files in the project. These include application files, resource files such as images and video, the XAML definition files, and the code-behind for those files.

The Project window gives several ways to edit different kinds of files. If you double-click on a XAML file, Expression Blend opens it in the Window Designer (described next).

If you double-click on a code-behind file, Expression Blend opens it in an internal code editor with IntelliSense.

> MISSING EDITORS

Unfortunately, Expression Blend doesn't have some of the extra editors that Visual Studio has to let edit bitmaps, icons, cursors, and so forth.
If you double-click on an image file in Expression Blend and you have a window open in the Window Designer, Expression Blend adds an control containing the image to the currently selected control. If you don't have a window open in the Window Designer, Expression Blend opens the file using its default application, usually Microsoft Paint.
Alternatively, you can right-click on the file and select "Edit Externally" to open it in an external editor like Microsoft Paint.

Best of all, you can right-click on a XAML or code-behind file and select "Edit in Visual Studio" to open the entire WPF project in Visual Studio. This lets you easily edit the code-behind and even the XAML with the full benefits of Visual Studio.

# WINDOW DESIGNER

The Window Designer lets you edit windows and define animations. The Storyboards section later in this chapter explains how you can use the Window Designer to build animations. This section explains how you can use it to build a window's basic user interface.

When you want to concentrate on the Window Designer, Expression Blend lets you hide the side panels that normally contain the Project window, Triggers, and other secondary windows. To hide or restore the panels, open the Window menu and select "Auto-Hide All Panels."

Figure 3-3 shows the Window Designer with the side panels hidden.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_78_0.png)

Figure 3-3

The upper part of this figure shows the design surface (artboard). Here you can add, select, resize, move, and delete controls. The Window Designer highlights the currently selected control with blue lines and displays the control name in its upper-left corner ("rectContent" in Figure 3-3).

Below the design surface is the XAML Editor. Here you can review and edit XAML code. In Figure 3-3 the Rectangle that is selected in the designer surface is highlighted in the XAML Editor.

The upper-right corner of the design surface holds three sideways buttons (circled in Figure 3-3) that let you view the design surface only, the XAML Editor, or a split view similar to the one shown in Figure 3-3.

Between the design surface and the XAML Editor is a zoom dropdown that says "100%" in Figure 3-3. Use the dropdown to select different scale levels while using the Designer.

The buttons to the right of the zoom dropdown let you turn off rendering effects (for performance), show or hide the snap grid (shown in Figure 3-3), turn snapping to gridlines on and off, turn snapping to snaplines on and off, and show and hide annotations.

The left edge of the screen shows the Control Toolbox. For more information on this area, see the section "Control Toolbox" later in this chapter.
