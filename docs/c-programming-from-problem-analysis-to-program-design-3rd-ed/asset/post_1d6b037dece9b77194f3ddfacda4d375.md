
If you do not see the constructed form, but instead see the program statements, your system may be set to show the Code Editor first. To see the graphical user interface form, select the **Designer** option from the **View** menu (or press **Shift+F7**). **F7** reveals the Code Editor.

Based on how you have Visual Studio configured, your screen might not look exactly like Figure 9-3. As a minimum, you will probably want to have the **Toolbox** and **Properties** windows accessible when you design your applications. Some developers prefer a larger screen to see their source code or find it distracting to have such a full screen of windows visible. You have many options for docking and hiding the windows shown in Figure 9-3. This figure has the **Toolbox**, **Solution Explorer**, **Properties**, and Form Designer windows visible. If you click the pushpin icon on the title bar of a specific window, the Auto Hide feature minimizes that window, but leaves a tab for it along the end of the IDE. Figure 9-4 calls attention to the pushpin icon. The **Toolbox** window is displayed in a dockable state snapped in place. The **Solution Explorer** and **Properties** windows are tab-docked in Auto Hide state. To put the window in Auto Hide state, click on its pushpin icon, and the pushpin is shown laying on its side. The **Error List** and **Output** windows, which are used when the application runs, are tab docked near the status bar.

![](img/e33ae760e23d89eac66541252ad65de8_507_0.png)

When a window is in Auto Hide state, if you move your mouse pointer over the tab, the window is redisplayed. At other times, only the tab is visible. To take a window out of Auto Hide, redisplay the window and click the pushpin icon so that it is standing up, as shown in Figure 9-4.

![](img/e33ae760e23d89eac66541252ad65de8_507_1.png)

**Figure 9-4**  Dockable windows

![](img/e33ae760e23d89eac66541252ad65de8_508_0.png)

Remember that to display the program statements, you can select **Code** from the **View** menu or press **F7**.

## Windows Forms

Windows Forms enable you to use a more modern object-oriented approach to developing Windows applications. The .NET model is based on an extensive collection of Control classes available, including a Form class, which is used as a container to hold other controls. The top-level window for an application is called a “form” in C#. If that top-level window opens another window, it is also considered a “form.” The large collection of properties and methods that make up a rich programmable interface to forms is available to classes inheriting from Form. The code written from Example 9-1 to change the title bar caption is:

```csharp
Text = "Simple Windows Application";  // Line 4
```

Using Visual Studio, all you have to do is find the appropriate property (Text) in the Properties window and type the value for the caption. You do not have to worry about whether the property’s name begins with an uppercase character or is spelled correctly. You can select it from an alphabetized list. In Figure 9-3, notice the Text property is selected. Changing that property is as easy as clicking in the box and typing a new title bar caption. As soon as you finish typing and click outside of the box, the Form Designer form is updated with this new caption in place of the default value, Form1. The section that follows explores some of the other properties you can change for the Form container class.

![](img/e33ae760e23d89eac66541252ad65de8_508_1.png)

If the Designer window is not visible, select **Designer** from the **View** menu or press **Shift+F7** to show the form.

### Windows Forms Properties

Figure 9-5 displays a list of some of the properties that can be set for the Form1 object. The Properties window is used to view and change the design time properties and events of an object.

If your Properties window is not visible, select Properties Window from the View menu or press F4.

![](img/e33ae760e23d89eac66541252ad65de8_509_0.png)

**Figure 9-5** Properties window

In Figure 9-5, some of the properties have an Expand arrow button to the left of the property name, indicating that the property can be expanded (only one is currently visible in the cropped image). Groups of properties are collapsed together for easier navigation through the property list. If you click the arrow the group expands. For example, clicking the arrow symbol to the left of the Location property reveals space where values can be typed for x and y. These values represent the x-coordinate and y-coordinate, respectively, for the location of the upper-left corner of the form.

In Figure 9-5, there are five buttons or icons immediately above the list of properties. The second button, the Alphabetical button, is selected. Properties appear listed in alphabetical order for this illustration. Many developers prefer to see the properties listed by category. As Figure 9-5 illustrates, the button to the left of the Alphabetical button rearranges the **Properties** window by category.

The lightning bolt, labeled **Events**, is used to display the list of events that can be programmed for a selected **object**. The third button from the left in Figure 9-5 is the **Property** button. This is selected, instead of the Events button, indicating that the list of properties are being displayed. Take a look at Figure 9-6, which contains a partial list of events that can be associated with a **Form1 object**.

![](img/e33ae760e23d89eac66541252ad65de8_510_0.png)

**Figure 9-6** Form events

To illustrate how Visual Studio automatically generates code when property values are changed, Table 9-1 lists changes made to the respective properties of **Form1**. These changes are applied to the project that was started in Figure 9-2. Changing the property is as simple as moving the cursor to the edit box to the right of the property identifier and typing or selecting a value. Many properties have a drop-down list of values available for selection. All changes to the property values can be made in the **Properties** window at design time. You do not have to enter any source code statements.

![](img/e33ae760e23d89eac66541252ad65de8_511_0.png)

You can, however, set the properties using program statements. As you review the code generated by Visual Studio, note how each property that you set by selecting or typing a value in the **Properties** window generates one or more lines of code.

**Table 9-1 Form1 property changes**

| Property name | Actions performed on the FirstWindows properties |
|---|---|
| AutoScroll | Selected `true` |
| BackColor | Selected a peach color from a drop-down color selection window on the Custom tab |
| Font | Selected Arial from a drop-down list of fonts; changed the size to 12 point; selected bold style |
| ForeColor | Selected a blue color from a drop-down color selection window on the Custom tab |
| Location | Changed the x-coordinate and y-coordinate from 0,0 to 30,30 |
| MaximizeBox | Selected `false` |
| Size | Changed the x-coordinate and y-coordinate from 300,300 to 400,400 |
| StartPosition | Using a drop-down menu option, changed the value from WindowsDefault to CenterScreen |
| Text | Typed "First Windows Application" |

As you can see from examining the property names in Table 9-1, the developers of Visual Studio did a good job selecting intuitive names for most of the properties. The names represent what the property would do to the form. Example 9-2 contains the source code listing generated by Visual Studio after the properties are set. The affected code is highlighted.

![](img/e33ae760e23d89eac66541252ad65de8_511_1.png)

Selecting **Code** on the **View** menu reveals the source code associated with the Form1.cs file. Double-clicking the form, while you are in design mode, takes you to the Code Editor, but with the undesired side effect that a Form1_Load() event-handler method heading and an empty body are added to your code. You will read more about events in Chapter 10. Each control has a default event. Double-clicking on the control adds its default event-handler method to your code. The form's default event is FormLoad.

Three files are illustrated. The IDE separates the source code into three files when you create a simple Windows application. Initially these files are Form1.cs, Form1.Designer.cs, and Program.cs. The first two files, Form1.cs and Form1.Designer.cs, both include partial class definitions for the Form1 class. It is recommended that you never edit the Form1.Designer.cs file. You will normally only be editing the Form1.cs file.
