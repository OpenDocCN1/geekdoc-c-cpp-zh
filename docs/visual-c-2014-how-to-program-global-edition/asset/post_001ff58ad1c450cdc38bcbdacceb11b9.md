
## 14.7 CheckBoxes and RadioButtons

| | | |
|---|---|---|
| 11 | Bold and Italic |
| 01 | Bold |
| 10 | Italic |

This is a simple example. The advantages of using bitwise operators to combine FontStyle values become more evident when we consider that there are five FontStyle values (Bold, Italic, Regular, Strikethout and Underline), resulting in 16 FontStyle combinations. Using bitwise operators to combine font styles greatly reduces the amount of code required to check all possible font combinations.

In 14.26, we need to set the FontStyle so that the text appears in bold if it was not originally, and vice versa. Line 23 uses the bitwise logical OR operator to do this. If label.Font.FontStyle is bold, then the resulting style is not bold. If the text is originally italic, the resulting style is bold and italic, rather than just bold. The same applies for FontStyle.Italic in line 32.

If we didn't use operators to compute FontStyle elements, we'd have to test for the current style and change it accordingly. In boCheckBox_CheckedChanged, we would test for the regular style and make bold, test for the bold style and make regular, test for the italic style and make it bold and test for the italic bold and make it italic. This is cumbersome, for every new style we add, we double the number of combinations. Adding a Checkbox for underline would require testing eight additional styles. Adding a Checkbox for strikethout would require sixteen additional styles.

### 14.7.3 RadioButtons

Radio buttons (defined with class radioButton) are similar to CheckBoxes in that they also have two states—selected and not selected (also deselected). However, RadioButtons appear as a group, in which only one RadioButton can be selected at a time. Selecting one RadioButton in the group forces all the others to be deselected. Therefore, RadioButtons are used to represent a set of mutually exclusive options (i.e., a set in which multiple options cannot be selected at the same time).

> Look-and-Feel Observation 14.4
> Use RadioButtons when the user should choose only one option in a group. Use CheckBoxes when the user should be able to choose multiple options in a group.

All RadioButtons added in a container are in the same group. To divide RadioButtons into several groups, they must be added to separate containers, such as GroupBoxes or Panels. Radio's common properties and a common event are listed in 14.27.

![](img/57baed2319be0bb1b5f98674846f2711_609_0.png)

| Common Properties Description |
|---|---|
| Checked | Indicates whether the RadioButton is checked. |
| Text | Specifies the RadioButton's text. |

Fig. 14.27 | RadioButton properties and an event. (Part I of 2.)

## RadioButton properties and an event

| Event | Description |
| --- | --- |
| Common Event CheckedChanged | Generated every time the RadioButton is checked or unchecked. When you double click a RadioButton control in design view, an empty event handler for this event is generated. |

Fig. 14.27 | RadioButton properties and an event. (Part 2 of 2.)

> Software Engineering Observation 14.I
> Form, GroupBoxes, and Panels can act as logical groups for RadioButtons. The RadioButtons within each group are mutually exclusive to each other, but not to RadioButtons in different logical groups.

The program in Fig. 14.28 uses RadioButtons to enable users to select options for a MessageBox. After selecting the desired attributes, the user presses the Display Button to display the MessageBox. A Label in the lower-left corner shows the result of the MessageBox (which, the user clicked—Yes, No, Cancel, etc.).

```c
// Fig. 14.28: RadioButtonTestForm.cs
// Using RadioButtons to set message window options.
using System;
using System.Windows.Forms;

namespace RadioButtonsTest
{
    // Form contains several RadioButtons--user chooses one
    // from each group to create a custom MessageBox
    public partial class RadioButtonsTestForm : Form
    {
        // create variables that store the user's choice of options
        private MessageBoxIconType { get; set; }
        private MessageBoxButtonType { get; set; }

        // default constructor
        public RadioButtonsTestForm()
        {
            InitializeComponent();
        }

        // change Buttons based on option chosen by sender
        private void buttonType_CheckedChanged(object sender, EventArgs e)
        {
            if (sender == okRadioButton) // display OK Button
            27 ButtonType = MessageBoxButtons.OK;
            28 }
            // display OK and Cancel Buttons
            30 else if (sender == okCancelRadioButton)
            {
            32 ButtonType = MessageBoxButtons.OKCancel;
            33 }
            // display Abort, Retry and Ignore Buttons
            35 else if (sender == abortIgnoreRadioButton)
            {
            37 ButtonType = MessageBoxButtons.AbortRetryIgnore;
            38 }
            // display Yes, No and Cancel Buttons
            40 else if (sender == yesNoCancelRadioButton)
            {
            42 ButtonType = MessageBoxButtons.YesNoCancel;
            43 }
            // display Yes and No Buttons
            45 else if (sender == yesNoRadioButton)
            {
            47 ButtonType = MessageBoxButtons.YesNo;
            48 }
            // only one option left--display Retry and Cancel Buttons
            50 else
            {
            52 ButtonType = MessageBoxButtons.RetryCancel;
            53 }

            // change Icon based on option chosen by sender
            57 private void iconType_CheckedChanged(object sender, EventArgs args)
            {
            if (sender == asteriskRadioButton) // display asterisk Icon
            {
            61 IconType = MessageBoxIcon.Asterisk;
            62 }
            // display error Icon
            64 else if (sender == errorRadioButton)
            {
            66 IconType = MessageBoxIcon.Error;
            67 }
            // display exclamation point Icon
            69 else if (sender == exclamationRadioButton)
            {
            71 IconType = MessageBoxIcon.Exclamation;
            72 }
            // display hand Icon
            74 else if (sender == handRadioButton)
            {
            76 IconType = MessageBoxIcon.Hand;
            77 }
```

Fig. 14.28 | Using RadioButtons to set message-window options. (Part 1 of 4.)

## 14.7 CheckBoxes and RadioButtons

```csharp
// 612 14.7 CheckBoxes and RadioButtons
// 612 Graphical Interfaces: Part I
// 612 display information
else if (sender == informationRadioButton)
{
    IconType = MessageBoxIcon.Information;
}
// 612 display question mark
else if (sender == questionRadioButton)
{
    IconType = MessageBoxIcon.Question;
}
// 612 display stop
else if (sender == stopRadioButton)
{
    IconType = MessageBoxIcon.Stop;
}
// 612 display warning
else if (sender == warningRadioButton)
{
    IconType = MessageBoxIcon.Warning;
}

// 612 store the value of the Button was pressed
// 612 change text accordingly
DialogResult result = MessageBox.Show("This is your MessageBox", "Custom", ButtonType, IconType);
switch (result)
{
    case DialogResult.OK:
        displayLabel.Text = "OK was pressed.";
        break;
    case DialogResult.Cancel:
        displayLabel.Text = "Cancel was pressed.";
        break;
    case DialogResult.Abort:
        displayLabel.Text = "Abort was pressed.";
        break;
    case DialogResult.Retry:
        displayLabel.Text = "Retry was pressed.";
        break;
    case DialogResult.Ignore:
        displayLabel.Text = "Ignore was pressed.";
        break;
    case DialogResult.Yes:
        displayLabel.Text = "Yes was pressed.";
        break;
    case DialogResult.No:
        displayLabel.Text = "No was pressed.";
        break;
}
```

Fig. 14.28 | Using RadioButtons to set message-window options. (Part 2 of 4.)
