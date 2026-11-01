With the PerformClick method, you can simulate the Click event on a button without the user actually clicking the button, which could be useful when testing your UI. A window also has the notion of a default button, which is automatically clicked if the user presses the Enter key in that window. To identify the button as default, you set the AcceptButton property on the form that contains the button to the button object. Then, when the user presses the Enter key, the button Click event for the default button is raised. Figure 39-1 shows that the button with the caption Default is the default button (notice the dark border). You can also define a button as the CancelButton which indicates that this button will receive a click event if the user presses the Escape key.

![](bbox=[0.6, 0.28, 0.9, 0.34])

Buttons can have images as well as text. Images are supplied by way of an ImageList object or the Image property. ImageList objects are exactly what they sound like: a list of images managed by a component placed on a form. They are explained in detail later in this chapter.

Both Text and Image have an Align property to align the text or image on the Button. The Align property takes a ContentAlignment enumeration value. The text or image can be aligned in combinations of left and right and top and bottom.

# CheckBox

The CheckBox control is also derived from ButtonBase and is used to accept a two-state or three-state response from the user. If you set the ThreeState property to true, the CheckBox's CheckState property can be one of the three CheckState enum values in the following table.

| VALUE | DESCRIPTION |
|---|---|
| Checked | The check box has a check mark. |
| Unchecked | The check box does not have a check mark. |
| Indeterminate | In this state the check box becomes gray. |

```
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
```

The Indeterminate state is useful if you want to convey to the user that an option has not been set. You can also check the Checked property if you want a Boolean value. The CheckedChanged and CheckStateChanged events occur when the CheckState or Checked properties change. For a three-state check box, you need to attach to the CheckStateChanged event. Catching these events can be useful for setting other values based on the new state of the CheckBox. The example includes the following code to show the state of the three-state check box. As the state of the check box changes, a label is updated with the new state.

# RadioButton

The last control derived from ButtonBase is the radio button. Radio buttons are generally used as a group. Sometimes referred to as option buttons, radio buttons allow the user to choose one of several options. When you have multiple RadioButton controls in the same container, only one at a time may be selected. So, if you have three options — for example, Red, Green, and Blue — if the Red option is selected and the user clicks the Blue option, Red is automatically deselected.