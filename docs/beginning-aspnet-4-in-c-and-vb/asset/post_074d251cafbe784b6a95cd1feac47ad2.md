
## User Interaction

User interaction is best described as the various events that a control creates and responds to. Some of the more common events are Click, DoubleClick, KeyDown, KeyPress, Validating, and Paint.

The Mouse events — Click, DoubleClick, MouseDown, MouseUp, MouseEnter, MouseLeave, and MouseHover — deal with the interaction of the mouse and the control. If you are handling both the Click and the DoubleClick events, every time you catch a DoubleClick event, the Click event is raised as well. This can result in undesired results if not handled properly. Also, Click and DoubleClick receive EventArgs as an argument, whereas the MouseDown and MouseUp events receive MouseEventArgs. The MouseEventArgs contain several pieces of useful information such as the button that was clicked, the number of times the button was clicked, the number of mouse wheel detents (notches in the mouse wheel), and the current X and Y coordinates of the mouse. If you have access to any of this information, you will have to handle either the MouseDown or MouseUp events, not the Click or DoubleClick events.

The keyboard events work in a similar fashion: The amount of information needed determines the event that is handled. For simple situations, the KeyPress event receives KeyPressEventArgs. This contains KeyChar, which is a char value that represents the key pressed. The Handled property is used to determine whether or not the event was handled. If you set the Handled property to true, the event is not passed on for default handling by the operating system. If you need more information about the key that was pressed, the KeyDown or KeyUp event is more appropriate to handle this. They both receive KeyEventArgs. Properties in KeyEventArgs include whether the Ctrl, Alt, or Shift key was pressed. The KeyCode property returns a Keys enumeration value that identifies the key that was pressed. Unlike the KeyPressEventArgs, KeyChar property, the KeyCode property tells you about every key on the keyboard, not just the alphanumeric keys. The KeyData property returns a Keys value and will also set the modifier. The modifiers are OR'd with the value. This tells you that the Shift key or the Ctrl key was pressed as well. The KeyValue property is the int value of the Keys enumeration. The Modifiers property contains a Keys value that represents the modifier keys that were pressed. If more than one has been selected, the values are OR'd together. The key events are raised in the following order:

- 1. KeyDown
- 2. KeyPress
- 3. KeyUp

The Validating, Validated, Enter, Leave, GotFocus, and LostFocus events all deal with a control gaining focus (or becoming active) or losing focus. This happens when the user tabs into a control or selects the control with the mouse. Enter, Leave, GotFocus, and LostFocus seem to be very similar in what they do. The GotFocus and LostFocus events are lower-level events that are tied to the WM_SETFOCUS and the WM_KILLFOCUS Windows messages. Generally, you should use the Enter and Leave events if possible. The Validating and Validated events are raised when the control is validating. These events receive CancelEventArgs. With this, you can cancel the following events by setting the Cancel property to true. If you have custom validation code, and validation fails, you can set Cancel to true and the control will not lose focus. Validating occurs during validation; Validated occurs after validation. The order in which these events are raised is:

- 1. Enter
- 2. GotFocus
- 3. Leave
- 4. Validating
- 5. Validated
- 6. LostFocus

Understanding the order of these events is important so that you don't inadvertently create a recursive situation. For example, trying to set the focus of a control from the control's LostFocus event creates a loop so the user would not be able to exit from your application.

With the PerformClick method, you can simulate the Click event on a button without the user actually clicking the button, which could be useful when testing your UI. A window also has the notion of a default button, which is automatically clicked if the user presses the Enter key in that window. To identify the button as default, you set the AcceptButton property on the form that contains the button to the button object. Then, when the user presses the Enter key, the button Click event for the default button is raised. Figure 39-1 shows that the button with the caption Default is the default button (notice the dark border). You can also define a button as the CancelButton which indicates that this button will receive a click event if the user presses the Escape key.

![](img/d7d2ffa0a76feaab821930e95daace93_1187_0.png)

Buttons can have images as well as text. Images are supplied by way of an ImageList object or the Image property. ImageList objects are exactly what they sound like: a list of images managed by a component placed on a form. They are explained in detail later in this chapter.

Both Text and Image have an Align property to align the text or image on the Button. The Align property takes a ContentAlignment enumeration value. The text or image can be aligned in combinations of left and right and top and bottom.

## CheckBox

The CheckBox control is also derived from ButtonBase and is used to accept a two-state or three-state response from the user. If you set the ThreeState property to true, the CheckBox's CheckState property can be one of the three CheckState enum values in the following table.

| VALUE | DESCRIPTION |
|---|---|
| Checked | The check box has a check mark. |
| Unchecked | The check box does not have a check mark. |
| Indeterminate | In this state the check box becomes gray. |

```csharp
private void threeState_CheckStateChanged(object sender, EventArgs e)
{
    CheckBox cb = sender as CheckBox;

    if (null != cb)
        threeStateState.Text =
            string.Format("State is {0}", cb.CheckState);
}
```
*code snippet 03 MainExample/ButtonExample.cs*

The Indeterminate state is useful if you want to convey to the user that an option has not been set. You can also check the Checked property if you want a Boolean value. The CheckedChanged and CheckStateChanged events occur when the CheckState or Checked properties change. For a three-state check box, you need to attach to the CheckStateChanged event. Catching these events can be useful for setting other values based on the new state of the CheckBox. The example includes the following code to show the state of the three-state check box. As the state of the check box changes, a label is updated with the new state.

## RadioButton

The last control derived from ButtonBase is the radio button. Radio buttons are generally used as a group. Sometimes referred to as option buttons, radio buttons allow the user to choose one of several options. When you have multiple RadioButton controls in the same container, only one at a time may be selected. So, if you have three options — for example, Red, Green, and Blue — if the Red option is selected and the user clicks the Blue option, Red is automatically deselected.

If the values in the list are wide, you can change the width of the drop-down portion of the control with the DropDownWidth property. The MaxDropDownItems property sets the number of items to show when the drop-down portion of the list is displayed.

The FindString and FindStringExact methods are two other useful methods of the list controls. FindString finds the first string in the list that starts with the passed-in string. FindStringExact finds the first string that matches the passed-in string. Both return the index of the value that is found or -1 if the value is not found. They can also take an integer that is the starting index to search from.

Lastly, the CheckedListBox control is similar to the ListBox; however, the DisplayMember and ValueMember properties do not show up in IntelliSense, nor do they display in the property grid. They are available on the actual control, but an attribute has been added to them to indicate that they are not used. This is not the case — you can use DisplayMember to determine what will show up on the user interface, or as an alternative, you can simply override the ToString() method on the objects you are adding into this list to display whatever you like onscreen.

## The DataGridView Control

The DataGrid control that has been available from the initial release of .NET was functional, but it had many aspects that made it unsuitable for use in a commercial application — such as an inability to display images, drop-down controls, or lock columns, to name but a few. The control always felt half-completed, so many control vendors provided custom grid controls that overcame these deficiencies and also provided much more functionality.

.NET 2.0 introduced an additional Grid control — the DataGridView. This addressed many of the deficiencies of the original control, and added significant functionality that previously was available only with add-on products.

The DataGridView control has binding capabilities similar to the old DataGrid, so it can bind to an Array, DataTable, DataView, or DataSet class, or a component that implements either the IListSource or IList interface. It gives you a variety of views of the same data. In its simplest guise, data can be displayed (as in a DataSet class) by setting the DataSource and DataMember properties — note that this control is not a plugin replacement for the DataGrid, so the programmatic interface to it is entirely different from that of the DataGrid. This control also provides more complex capabilities, which are discussed in the course of this chapter.

In this section we use the Northwind sample database. If you don’t already have it installed, please download the installer from the Web and create a database called Northwind in your SQL Server or SQL Express instance. You can find the installation scripts for Northwind at http://msdn.microsoft.com/en-us/library/ms143221.aspx.

## Displaying Tabular Data

Chapter 20, “Threads, Tasks, and Synchronization,” introduced numerous ways of selecting data and reading it into a data table, although the data was displayed in a very basic fashion using Console.WriteLine().
