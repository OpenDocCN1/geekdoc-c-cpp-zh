# The syntax for the Show() method of the MessageBox class

```
MessageBox.Show(text[, caption[, buttons[, icon[, defaultButton]]]]);
```

# The enumerations that work with the MessageBox class

| Enumeration | Members |
|---|---|
| MessageBoxButtons | OK, OKCancel, YesNo, YesNoCancel, AbortRetryIgnore |
| MessageBoxIcon | None, Information, Error, Warning, Exclamation, Question, Asterisk, Hand, Stop |
| MessageBoxDefaultButton | Button1, Button2, Button3 |
| DialogResult | OK, Cancel, Yes, No, Abort, Retry, Ignore |

# A statement that displays a dialog box and gets the user response

```
DialogResult button = MessageBox.Show(
"Are you sure you want to save this data?",
"Payment",
MessageBoxButtons.YesNo,
MessageBoxIcon.Question,
MessageBoxDefaultButton.Button2);
```

# The dialog box that’s displayed

![](bbox=[0.155, 0.444, 0.444, 0.558])

# A statement that checks the user response

```
if (button == DialogResult.Yes)
{
    SaveData();
    isDataSaved = true;
}
```

# Description

+   - You can use the Show() method of the MessageBox class to display a message to a user and accept a response from the user.
+   - You use the first three enumerations listed above to specify the buttons and icon that will appear in the dialog box and the button that’s treated as the default.
+   - If you omit the buttons argument, the OK button is displayed by default. If you omit the icon argument, no icon is displayed by default. If you omit the default button argument, the first button is the default.
+   - The Show() method returns a DialogResult value that corresponds to one of the members of the DialogResult enumeration. You can use this value to determine which button the user clicked.