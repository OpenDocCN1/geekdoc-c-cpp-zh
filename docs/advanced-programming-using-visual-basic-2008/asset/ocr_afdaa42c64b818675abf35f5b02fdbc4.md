You can share data between forms by setting properties of the form. If you need to pass data between forms, create a property of the form, write Property Set / Get procedures, and set the properties as needed.

# Controls

The .NET intrinsic (built-in) controls appear in the toolbox, and you can add more controls to the toolbox by right-clicking on the toolbox and selecting Choose Items.

Create an instance of a control class on a form by clicking on the control's icon and drawing the control on the form or by double-clicking the control's icon, which creates a control of default size. You can create multiple controls of one class by Ctrl-clicking on the icon—the pointer remains a crossbar as long as you keep the Ctrl key pressed and you can create as many controls of that type as you wish. Release the Ctrl key when you are finished drawing that control type.

You can select multiple controls using Ctrl-click or Shift-click, or by drawing a selection box around the controls with the mouse pointer. The selected controls are treated as a group and you can move them, delete them, or change their common properties.

# Common .NET Controls

The majority of VB programming is performed using just a few controls: Label, TextBox, CheckBox, RadioButton, ListBox, ComboBox, and Button.

# The Label Control

Use a Label control for the words and instructions on the form as well as program output that you don't want the user to be able to modify. Set the Text property for the words that you want to appear. You also can set the font and size and change its style with the BorderStyle and BackColor properties. A Label cannot receive the focus.

# The TextBox Control

Use a TextBox for user input. The Text property holds the contents of the TextBox. You can enable/disable a TextBox by setting its Enabled property to true or false. You also can use a TextBox for program output. Set its ReadOnly property to true for output that you don't want the user to be able to change. This allows the user to still select the output and copy it to the clipboard for pasting in another location.

# The CheckBox Control

Use a CheckBox for options the user can select or deselect. Each CheckBox operates independently, so any number of check boxes may be selected.

The Checked property of a CheckBox holds its current state and may be true or false. You can test and set the Checked property in code.

```
If TheCheckBox.Checked Then
' Take some action.
TheCheckBox.Checked = False
End If
```