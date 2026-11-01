
will be centred on the form both horizontally and vertically meaning that the Label will be aligned in the middle of the form.

![](img/41d82527c4e41cdb7e56259564306ddc_36_0.png)

Figure 3.19. Centring the Label on the form

After these steps, the Form looks like below:

![](img/41d82527c4e41cdb7e56259564306ddc_36_1.png)

Figure 3.20. Centred Label on the Form

Our GUI design is complete now. Since we don't want our Hello World application to do something interactive, we don't need to write a single line of code in this project. However, I want to show you the file on which we'll do actual coding in the following chapters. As I stated earlier, the Form1.cs file in fact consists of a Design mode and a Code mode. We dealt with the Design mode here. In order to view it in the

![](img/41d82527c4e41cdb7e56259564306ddc_41_0.png)

Figure 3.29. Opening the solution file Hello World.sln

That's all for this chapter. We have learned how to create a new project. to place a Label control on the form, setting basic properties of the Label visually and aligning it in the middle. And then we built the project and created the executable file.

As you may have noticed from the Toolbox, there are a lot of controls that can be used on Windows forms. Since our aim is to learn both GUI design and C# coding, it is required to know how we can use other control types like a Button or a TextBox. In the next two chapters, we'll learn working with commonly used form controls together with the associated basic C# coding before moving on to actual coding lectures in the following chapters.

| Reference number | Name | Image | Information |
|---|---|---|---|
| 10 | MaskedTextBox | MaskedTextBox | text box that forces to enter text in a specified format |
| 11 | MonthCalendar | MonthCalendar | A calendar control from which a date can be selected |
| 12 | NotifyIcon | NotifyIcon | An icon element in the notification area |
| 13 | NumericUpDown | NumericUpDown | Provides a numeric value which can be changed by arrow clicks |
| 14 | PictureBox | PictureBox | Used for displaying an image |
| 15 | ProgressBar | ProgressBar | Shows the progress of an operation |
| 16 | RadioButton | RadioButton | Enables to select only one of several options |
| 17 | RichTextBox | RichTextBox | Advanced text box with paragraph formatting, etc. |
| 18 | TextBox | TextBox | Enables the user to input text |
| 19 | ToolTip | ToolTip | Displays short info when mouse is over |
| 20 | TreeView | TreeView | Displays hierarchical items |
| 21 | WebBrowser | WebBrowser | Displays web pages on the form |

Table 4.1. Common controls (cont'd)

You can find these controls in the Common Controls section of the Toolbox as shown below:

![](img/41d82527c4e41cdb7e56259564306ddc_45_0.png)

Figure 4.2. Common controls in the Toolbox

### 4.2. Containers and Menus

Containers are the controls that are used to group other form elements. Container types provided in Visual Studio are as follows:

| Reference number | Name | Image | Information |
|---|---|---|---|
| 1 | FlowLayoutPanel | FlowLayoutPanel | Provides a liquid layout |
| 2 | GroupBox | GroupBox | Groups and draws a frame around its elements |
| 3 | Panel | Panel | Simply groups its elements |

| Reference number | Name | Image | Information |
|---|---|---|---|
| 4 | SplitContainer | SplitContainer | Provides a two vertical resizable areas for a container |
| 5 | TabControl | TabControl | Provides tabbed areas to place elements |
| 6 | TableLayoutPanel | TableLayoutPanel | Table shaped container |

Table 4.3. Containers used for grouping controls (cont'd)

Containers are listed in the Toolbox as shown below:

![](img/41d82527c4e41cdb7e56259564306ddc_46_0.png)

Figure 4.2. Containers in the Toolbox

On the other hand, menus and toolbars are special types of controls that provide easy access to commands on a form. Widely used examples include the File menu at the top of the form and the right-click menu for copy, paste, etc. commands. Visual Studio has the following menu and toolbar options:

| Reference number | Name | Image | Information |
|---|---|---|---|
| 1 | ContextMenuStrip | ContextMenuStrip | The right-click menu |
| 2 | MenuStrip | MenuStrip | Groups commands by functionality like the File menu |

![](img/41d82527c4e41cdb7e56259564306ddc_53_0.png)

Figure 4.9. Button stretches when its Anchor properties are updated as Top, Left, Right

17. Dock: Used for docking the control in one of five areas on the form. The docking options are shown in the figure below. Note that its options box is opened by clicking the arrow at the right as we did for other properties.

![](img/41d82527c4e41cdb7e56259564306ddc_53_1.png)

Figure 4.10. Docking options (None is selected by default)

18. Location: This property defines the location of the control on the form relative to the top left of the form.

19. MaximumSize: This property sets the maximum allowed size of the control. Used for forms rather than controls in practice.

20. MinimumSize: This sets the minimum allowed size of the control.

21. Size: Sets the dimensions of the control in pixels.

Short explanations of properties appear at the bottom space of the properties window once a property is selected as shown in Figure 4.11.

Properties of controls and other form elements can also be changed programmatically in real time during runtime.

![](img/41d82527c4e41cdb7e56259564306ddc_54_0.png)

Figure 4.11. Short explanation for the selected property appears at the bottom of the properties window

### 4.6. Events of Controls

Events take care of the things happening on the form. Clicking a button or selecting an option from a drop-down box are examples of events. The code that will be executed when an event happens are written in the .cs file of the project.

Each control type has a default event that can be created in the code just by double-clicking the control. For example, let's place a CheckBox on the form by drag&drop as in Figure 4.12. Form1 is in [Design] mode as it is shown inside the ellipse. When we double-click checkBox1 on this form, code view of Form1 opens in the editor as shown in Figure 4.13.

The default event for a CheckBox is the CheckChanged event which fires (executes) when the check of the CheckBox changes, i.e. when it is checked or unchecked. This default event handling method named checkBox1_CheckChanged(...) is created when checkBox1 is double clicked on the form as shown inside the rectangle in Figure 4.13.

![](img/41d82527c4e41cdb7e56259564306ddc_57_0.png)

Figure 4.14. All events of a CheckBox control listed in categories

| Reference number | Name | Triggered when... | Method format |
|---|---|---|---|
| 1 | BackColorChanged | the background color is changed | ControlName_BackColorChanged(...) |
| 2 | BackgroundImageChanged | the background image is changed | ControlName_BackgroundImageChanged(...) |
| 3 | CursorChanged | the cursor type is changed | ControlName_CursorChanged(...) |
| 4 | KeyPressed | a key on the keyboard is pressed when the control is active | ControlName_KeyPressed(...) |
| 5 | Load | the form is loaded (at the beginning of the execution of the program) | FormName_Load(...) |

![](img/41d82527c4e41cdb7e56259564306ddc_60_0.png)

## Chapter 5

### COMMON CONTROLS

In this chapter, we will study commonly used controls in detail because they are the backbones of GUI (form) design. We will use them in small projects where their properties and events will be programmed. This will be a gentle beginning of our C# coding journey.

### 5.1. Button

Buttons are used for triggering actions.

![](img/41d82527c4e41cdb7e56259564306ddc_60_1.png)

Figure 5.1. A button

Buttons have the following properties:

- **Image**: The foreground image of the button.
- **TextAlign**: The alignment of the text on the button.
- **FlatStyle**: Sets the appearance of the button.

> Please note that the properties discussed here are the ones additional to the common properties discussed in the previous chapter.

A simple Button example: Let's create a small project incorporating a Button step-by-step:

- 1. Create a new C# project in Visual Studio.
- 2. Place a Button on the form.
- 3. Set the Text property of the Button as Change.
- 4. Set the Name property of the Button as changeButton.
