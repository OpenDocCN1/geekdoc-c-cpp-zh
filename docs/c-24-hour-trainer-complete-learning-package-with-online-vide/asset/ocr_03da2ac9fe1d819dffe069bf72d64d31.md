This makes the ListBox remove the currently selected item. Fortunately if there is no selected item, the ListBox does nothing instead of crashes.

When the user clicks the dialog's Cancel Button, hide the dialog and return DialogResult.Cancel.

+   1. You don't need to do anything else to make this work. When you set the dialog's CancelButton property to this Button, C# sets the Button's DialogResult property to DialogResult.Cancel so the button automatically sets the return result and closes the dialog.

When the user clicks the dialog's OK Button, check the entered name's length. If the length is 0, display a message asking the user to enter a name. If the length is greater than 0, hide the dialog and return DialogResult.OK.

1. Create an event handler for the dialog's OK Button. Use code similar to the following:

```
// Make sure the comedian's name isn't blank.
private void okButton_Click(object sender, EventArgs e)
{
    if (nameTextBox.Text.Length == 0)
    {
        MessageBox.Show("Please enter a comedian's name");
    }
    else
    {
        DialogResult = DialogResult.OK;
    }
}
```

# EXERCISES

+   1. [WPF] Repeat the Try It with a WPF application. Hints:

```
if (newComedianDialog.ShowDialog().Value)
{
    ...
}
```

+   - To see if the user clicked OK on the dialog, see if the ShowDialog method returns True as in this code:
+   - To define the Accept Button, set the Button's IsDefault property to True.
+   - To define the Cancel Button, set the Button's IsCancel property to True.
+   - To close the dialog, the OK Button's code should set DialogResult = true.
+   - To prevent the user from resizing the dialog, set ResizeMode to NoResize.
+   - To prevent the dialog from appearing in the taskbar, set ShowInTaskbar to False.

2. It's usually better to prevent the user from performing invalid actions than to allow the user to perform the action and then complain. In the Try It, the user can click the Delete Comedian Button even if no comedian is selected. To fix that, copy the program you built