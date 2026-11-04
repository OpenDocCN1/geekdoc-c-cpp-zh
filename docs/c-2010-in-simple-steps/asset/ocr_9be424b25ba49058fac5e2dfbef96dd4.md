# Using the StatusStrip Control

The StatusStrip control is an improved version of the StatusBar control. It allows you to display information about other controls in a form. For instance, you can use the StatusStrip control to display the name and description of a selected control, the progress of an ongoing operation, or instructions for the users.

The StatusStrip control is an instance of the StatusStrip class that exists in the System.Windows.Forms namespace.

Table 6.12 lists noteworthy properties of the StatusStrip class:

Table 6.12: Noteworthy Properties of the StatusStrip Class

| Property | Description |
|---|---|
| Dock | Retrieves or sets the border of the StatusStrip control that is docked to its parent control |
| GripStyle | Retrieves or sets the visibility of the grip of a StatusStrip control. The GripStyle property is used to reposition the StatusStrip control. For instance, if the GripStyle property of a StatusStrip control is set to Hidden, then there is no way for a user to drag the StatusStrip control from the position it has been originally placed. |
| LayoutStyle | Retrieves or sets a value that indicates the manner in which the status strip items are placed in the StatusStrip control |
| ShowItemToolTips | Retrieves or sets a value that indicates whether the ToolTips are displayed for the StatusStrip control |
| SizingGrip | Retrieves or sets a value that indicates whether a sizing handle, such as a grip appears in the lower-right corner of the control |
| Stretch | Retrieves or sets a value that indicates whether the StatusStrip control stretches from one end to another of its container |

As the StatusStrip class inherits the ToolStrip class, the StatusStrip control can contain several controls or items. The controls that a StatusStrip control can have are as follows:

+   - ToolStripStatusLabel: Refers to a label in the StatusStrip control
+   - ToolStripDropDownButton: Refers to a drop-down button which when clicked displays a drop-down list
+   - ToolStripSplitButton: Refers to a split button (combination of a standard button on the left and a drop-down button on the right)
+   - ToolStripProgressBar: Refers to a progress bar

> **Note**
> 
> By default, the StatusStrip control does not contain panels. You can add panels to a StatusStrip control by using the Items.AddRange() method.

Now, let's create a Windows Forms application named StatusStripDemo to see how a StatusStrip control works. Perform the following steps to create the StatusStripDemo application:

+   1. Repeat steps 1-4 under the Using the ToolStrip Control heading of this chapter.
+   2. Enter StatusStripDemo as the name of the application in the Name text box of the New Project dialog box and enter the path of the folder where you want to save the application in the Location combo box.
+   3. Click the OK button in the New Project dialog box. The StatusStripDemo application is created.
+   4. Select the Form1 form in the designer and press the F4 key to open its Properties window. In the Properties window, set the Text and Size properties of the Form1 form to StatusStripDemo and 450,300 respectively.
+   5. Drag Label and TextBox controls from Toolbox and drop them on the Form1 form. Set the properties of the Label (label1) and TextBox (textBox1) controls, as given in Table 6.13: