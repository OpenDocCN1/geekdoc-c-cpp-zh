
## Table 8.1: Noteworthy Public Properties of the Form Class

| Property | Description |
|---|---|
| DesktopBounds | Gets or sets the size and location of a form on desktop |
| DesktopLocation | Gets or sets the location of a form on desktop |
| DialogResult | Gets or sets the value of the dialog result property for a form when it is displayed as a modal dialog box. |
| FormBorderStyle | Gets or sets the border style of a form |
| HelpButton | Gets or sets the value indicating whether the Help button should appear in the caption box of a form |
| Icon | Gets or sets an icon (picture representing a form on the taskbar) for a form |
| IsMdiChild | Gets or sets a value that indicates if a form is an MDI child form |
| IsMdiContainer | Gets or sets a value that indicates if a form is a container for MDI child forms |
| IsRestrictedWindow | Gets a value that determines whether a form uses all the windows and user input events without any restrictions |
| KeyPreview | Gets or sets a value that determines whether a form receives all the key events before an event is passed to an active control |
| Location | Gets or sets the location of a form |
| MainMenuStrip | Gets or sets the menu container for a form |
| MaximizeBox | Gets or sets a value that determines if the Maximize button is displayed in the caption bar of a form |
| MaximumSize | Gets a value that indicates the maximum size of a form |
| MdiChildren | Gets an array of MDI child forms of a parent form |
| MdiParent | Gets or sets the current MDI parent form of a form |
| Menu | Gets or sets the Main menu that is displayed in a form |
| MergedMenu | Gets the merged menu for a form |
| MinimizeBox | Gets or sets the value that determines whether the Minimize button is displayed in the caption bar of a form |
| MinimumSize | Gets or sets the minimum size of a form |
| Modal | Gets a value that determines if a form is displayed in a modal dialog box |
| Opacity | Gets or sets the opacity level of a form |
| OwnedForms | Gets an array of Form objects of all forms owned by the parent form |
| Owner | Gets or sets the parent form that owns a form |
| RightToLeftLayout | Gets or sets the value that determines whether the right-to-left placement is turned on. |
| ShowIcon | Gets or sets a value that determines whether an icon (picture representing a form on the taskbar) is displayed in the caption bar of a form |
| ShowInTaskbar | Gets or sets a value that determines whether a form is displayed in the Windows Taskbar |
| Size | Gets or sets the size of a form |
| SizeGripStyle | Gets or sets the style of the size grip to be displayed in the lower-right corner of a form |
| StartPosition | Gets or sets the starting position of a form at runtime |
| TabIndex | Gets or sets the tab order for the controls in a form |
| TabStop | Gets or sets a value that determines whether a user can give focus to a form by using the Tab key |
| Text | Gets or sets the text associated with a form |
| TopLevel | Gets or sets a value that determines whether a form should be displayed as a top-level window |
| TopMost | Gets or sets a value that determines whether a form should be displayed as the topmost form of an application |
| TransparencyKey | Gets or sets the color representing the transparent areas of a form |
| WindowState | Gets or sets a value that indicates whether a window is restored, minimized, or maximized |

## Table 8.2: Noteworthy Public Methods of the Form Class

| Method | Associated function |
|--------|---------------------|
| Activate | Activates a form by giving it focus |
| AddOwnedForm | Adds an owned form to the parent form |
| Close | Closes a form |
| LayoutMdi | Arranges MDI child forms within the MDI parent form |
| RemoveOwnedForm | Removes the owned form from the parent form |
| SetDesktopBounds | Sets the bounds of a form with desktop coordinates |
| SetDesktopLocation | Sets the location of a form with desktop coordinates |
| ShowDialog | Displays a form as a modal dialog box |
| ToString | Gets a string representing the current instance of a form |
| ValidateChildren | Validates all selected child controls of a form |

## Table 8.3: Noteworthy Public Events of the Form Class

| Event | Description |
|-------|-------------|
| Activated | Occurs when a form is activated through the code |
| Closed | Occurs when a form is closed |
| Closing | Occurs when a form is closing |
| Deactivate | Occurs when a form loses focus |
| FormClosed | Occurs after a form is closed |
| FormClosing | Occurs before a form is closed |
| HelpButtonClicked | Occurs when the Help button is clicked |
| InputLanguageChanged | Occurs after the input language of a form is changed |
| InputLanguageChanging | Occurs when a user tries to change the input language of a form |
| Load | Occurs before displaying a form for the first time |
| MaximizedBoundsChanged | Occurs when the value of the MaximizedBounds property has been changed |
| MaximumSizeChanged | Occurs when the value of the MaximumSize property has been changed |
| MdiChildActivate | Occurs when an MDI child form is activated or closed within an MDI application |
| MenuComplete | Occurs when the menu of a form loses focus |
| MenuStart | Occurs when the menu of a form receives focus |
| MinimumSizeChanged | Occurs when the value of the MaximumSize property is changed |
| ResizeBegin | Occurs when a user begins resizing a form |
| ResizeEnd | Occurs when a user finishes resizing a form |
| RightToLeftLayoutChanged | Occurs when the RightToLeftLayout property changes |
| Shown | Occurs when a form is displayed for the first time |
| TabIndexChanged | Occurs when the value of the TabIndex property changes |

Now that you are familiar with the noteworthy properties, methods and events of Windows Form, let's now learn how to create a Windows Forms application and set its various properties in the Immediate Solutions section.

## Immediate Solutions

## Creating Windows Forms Applications

In this section, you learn to create a Windows Forms application. Perform the following steps to create a Windows application, named FirstProject:

- 1. Click Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010. Visual Studio 2010 IDE opens.
- 2. Click the New Project link on Start Page or select File→New→Project. The New Project dialog box appears (Figure 8.2).
- 3. Select Visual C# option from the Installed Templates pane and then select Windows Forms Application option from the middle pane. Enter a name, for instance FirstProject, in the Name text box.
- 4. Enter a location for the application, for instance D:\Black Books\C# 2010\Chapter 8\, in the Location text box by using the Browse button. Ensure that the Create new solution option is selected in the Solution dropdown menu and the FirstProject text appears in the Solution name text box, as shown in Figure 8.2:

![](img/e073a4882197be4ab61103cbe0bcb394_302_0.png)

Figure 8.2: Displaying the New Project Dialog Box

- 5. Click the OK button. The FirstProject Windows Forms application opens in Visual Studio 2010 IDE, as shown in Figure 8.3:

![](img/e073a4882197be4ab61103cbe0bcb394_302_1.png)

Figure 8.3: Displaying the Windows Forms Designer

Whenever you create a new Windows Forms application or project, certain files and directories are created automatically. In our case, the following files and directories are created with the FirstProject application:

- FirstProject.csproj – Specifies a C# project
- AssemblyInfo.cs – Contains general information, such as the assembly and version of the application
- Form1.cs – Contains the code of a form
- Resources.resx – Specifies an eXtensible Markup Language (XML)-based resource template
- FirstProject.sln – Specifies a solution file of the application, storing the solution’s configuration
- Bin – Specifies the directory for binary executables
- Obj – Specifies the directory for debugging binaries

All these files and directories are created automatically by C# 2010. Now, let’s add some controls to the Form1.cs file.

## Adding Controls to Windows Forms

You can add many useful controls to a Windows Form, such as scroll bars, buttons, text boxes, and menus, which users generally use to interact with an application. In C# 2010, you can use the Toolbox window to add controls to a form.

Let’s add Button and TextBox controls by just dragging them from the Toolbox window to Form1 of the FirstProject application, as shown in Figure 8.4:

![](img/e073a4882197be4ab61103cbe0bcb394_303_0.png)

Figure 8.4: Adding Controls to a Form

You can also add controls to Form1 by just clicking the required control in the Toolbox window. The names for these controls, such as button1 and textBox1, are provided by C# automatically.

In this application, we want to display text in the text box when a user clicks the button1 button. Therefore, we change the Text property of this button to Click Me using the Properties window, as shown in Figure 8.5:
