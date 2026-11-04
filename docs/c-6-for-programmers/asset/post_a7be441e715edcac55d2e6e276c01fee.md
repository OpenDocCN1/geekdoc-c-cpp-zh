
## Using Resources Programmatically

In this example, we added the images to the project as resources. This causes the IDE to copy the images into the app's executable file and enables the app to access the images through the project's Properties namespace. When you do this, you don't need to worry about wrapping the images with the app when you move it to another location or computer.

If you're creating a new project, use the following steps to add images to the project as resources:

- 1. After creating your project, right click the project's Properties node in the Solution Explorer and select Open to display the project's properties.
- 2. From the tabs on the left, click the Resources tab.
- 3. At the top of the Resources tab, click the down arrow next to Add Resource and select Add Existing File... to display the Add existing file to resources dialog.
- 4. Locate the image files you wish to add as resources and click the Open button. We provided three sample images in the Images folder with this chapter's examples.
- 5. Save your project.

The files now appear in a folder named Resources in the Solution Explorer. We'll use this technique in most examples that use images going forward.

A project's resources are accessible to the app via its Resources class (of the project's Properties namespace). The Resources class contains a ResourceManager object for interacting with the resources programmatically. To access an image, you can use the method GetObject, which takes as an argument the resource name as it appears in the Resources tab (e.g., "image0") and returns the resource as an Object. Lines 27-28 invoke GetObject with the result of the string-interpolation expression

```
$"image{ImageNumber}"
```

which builds the name of the resource by placing the index of the next picture (ImageNumber, which was obtained earlier in line 23) at the end of the word "image". You must convert this Object to type Image (namespace System.Drawing) to assign it to the PictureBox's Image property (lines 26-28).

The Resources class also provides direct access to the resources you define with expressions of the form Resources.resourceName, where resourceName is the name you provided to the resource when you created it. When using such an expression, the resource returned already has the appropriate type. For example, Properties.Resources.image0 is an Image object representing the first image.

## 14.9 ToolTips

In Chapter 2, we demonstrated tool tips—the helpful text that appears when the mouse hovers over an item in a GUI. Recall that the tool tips in Visual Studio (and most apps with GUIs) help you become familiar with the IDE's features and serve as useful reminders for each toolbar icon's functionality. This section demonstrates how to use the ToolTip component to add tool tips to your apps. Figure 14.31 describes common properties and a common event of class ToolTip.

| ToolTip properties and an event | Description |
|---|---|
| *Common Properties* | |
| AutoPopDelay | The amount of time (in milliseconds) that the tool tip appears while the mouse is over a control. |
| InitialDelay | The amount of time (in milliseconds) that a mouse must hover over a control before a tool tip appears. |
| ReshowDelay | The amount of time (in milliseconds) between which two different tool tips appear (when the mouse is moved from one control to another). |
| *Common Event* | |
| Draw | Raised when the tool tip is about to be displayed. This event allows programmers to modify the appearance of the tool tip. |

Fig. 14.31 | ToolTip properties and an event.

When you add a ToolTip component from the Toolbox, it appears in the component tray—at the bottom of the window when the Form is in Design mode. Once a ToolTip is added to a Form, a new property appears in the Properties window for the Form's other controls. This property appears in the Properties window as ToolTip on, followed by the name of the ToolTip component. For instance, if our Form's ToolTip were named helpfulToolTip, you would set a control's ToolTip on helpfulToolTip property value to specify the control's tool tip text. Figure 14.32 demonstrates the ToolTip component. For this example, we create a GUI containing two Labels, so we can demonstrate different tool tip text for each Label. Since there's no event-handling code in this example, we do not show you the code for the Form class.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_462_0.png)

![](img/3f5ef6be1748bb746e5f71a483bba4d0_462_1.png)

Fig. 14.32 | Demonstrating the ToolTip component.

In this example, the IDE named the ToolTip component toolTip1. Figure 14.33 shows the ToolTip in the component tray. We set the tool tip text for the first Label to "First Label" and the tool tip text for the second Label to "Second Label". Figure 14.34 demonstrates setting the tool tip text for the first Label.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_463_0.png)

ToolTip in component tray

Fig. 14.33 | Demonstrating the component tray.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_463_1.png)

Property to set tool tip text

Tool tip text

Fig. 14.34 | Setting a control's tool tip text.

## 14.10 NumericUpDown Control

At times, you'll want to restrict a user's input choices to a specific range of numeric values. This is the purpose of the NumericUpDown control. This control appears as a TextBox, with two small Buttons on the right side—one with an up arrow and one with a down arrow. By default, a user can type numeric values into this control as if it were a TextBox or click the up and down arrows to increase or decrease the value in the control, respectively. The largest and smallest values in the range are specified with the Maximum and Minimum properties, respectively (both of type decimal). The Increment property (also of type decimal) specifies by how much the current value changes when the user clicks the arrows. Property DecimalPlaces specifies the number of decimal places that the control should display. Figure 14.35 describes common NumericUpDown properties and an event.

| NumericUpDown properties and an event | Description |
|---|---|
| *Common Properties* | |
| DecimalPlaces | Specifies how many decimal places to display in the control. |
| Increment | Specifies by how much the current number in the control changes when the user clicks the control's up and down arrows. |
| Maximum | Largest value in the control's range. |
| Minimum | Smallest value in the control's range. |
| UpDownAlign | Modifies the alignment of the up and down Buttons on the NumericUpDown control. This property can be used to display these Buttons either to the left or to the right of the control. |
| Value | The numeric value currently displayed in the control. |
| *Common Event* | |
| ValueChanged | This event is raised when the value in the control is changed. This is the default event for the NumericUpDown control. |

Fig. 14.35 | NumericUpDown properties and an event.

Figure 14.36 demonstrates a NumericUpDown control in a GUI that calculates interest rate. The calculations performed in this app are similar to those in Fig. 6.6. TextBoxes are used to input the principal and interest rate amounts, and a NumericUpDown control is used to input the number of years for which we want to calculate interest.

```csharp
1 // Fig. 14.36: InterestCalculatorForm.cs
2 // Demonstrating the NumericUpDown control.
3 using System;
4 using System.Windows.Forms;
5 
6 namespace NumericUpDownTest
7 {
8     public partial class InterestCalculatorForm : Form
9     {
10        // default constructor
11        public InterestCalculatorForm()
12        {
13            InitializeComponent();
14        }
15 
16        private void calculateButton_Click(object sender, EventArgs e)
17        {
18            // retrieve user input
19            decimal principal = decimal.Parse(principalTextBox.Text);
20            double rate = double.Parse(interestTextBox.Text);
21            int year = (int) yearUpDown.Value;
22 
23            // set output header
24            string output = "Year\tAmount on Deposit\r\n";
```

Fig. 14.36 | Demonstrating the NumericUpDown control. (Part 1 of 2.)
