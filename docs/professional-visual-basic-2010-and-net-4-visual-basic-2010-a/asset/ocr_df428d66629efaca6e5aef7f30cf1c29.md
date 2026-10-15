The DialogResult property of a dialog box can be set in two ways. The most common way is to associate a DialogResult value with a button. Then, when the button is pressed, the associated value is automatically placed in the DialogResult property of the form.

To set the DialogResult value associated with a button, use the DialogResult property of the button. If this property is set for the button, then it is unnecessary to set the DialogResult in code when the button is pressed.

The following example uses this technique. In Visual Studio 2010, start a new VB Windows application. On the automatic blank form that appears (named Form1), place a single button and set its Text property to Dialog.

Now add a new Windows form by selecting Project ➔ Add Windows Form and name it DialogForm.vb. Place two buttons on DialogForm and set the properties for the buttons as shown in the following table.

| PROPERTY | VALUE FOR FIRST BUTTON | VALUE FOR SECOND BUTTON |
|---|---|---|
| Name | OKButton | CancelButton |
| Text | OK | Cancel |
| DialogResult | OK | Cancel |

Do not put any code in DialogForm at all. The form should look like the one shown in Figure 14-4.

On the first form, Form1, place the following code in the Click event for Button1:

```
Dim frmDialogForm As New DialogForm()
frmDialogForm.ShowDialog()
' You're back from the dialog - check user action.
Select Case frmDialogForm.DialogResult
Case DialogResult.OK
MsgBox("The user pressed OK")
Case DialogResult.Cancel
MsgBox("The user pressed cancel")
End Select
frmDialogForm = Nothing
```

![](bbox=[0.71, 0.405, 0.88, 0.495])

Run and test the code. When a button is pressed on the dialog form, a message box should be displayed (by the calling form) indicating the button that was pressed.

The second way to set the DialogResult property of the form is in code. In a Button_Click event, or anywhere else in the dialog form, a line like the following can be used to set the DialogResult property for the form and simultaneously hide the dialog form, returning control to the calling form:

```
Me.DialogResult = DialogResult.Ignore
```

This particular line sets the dialog result to DialogResult.Ignore, but setting the dialog result to any of the permitted values also hides the dialog form.

# Forms at Runtime

The life cycle of a form is like that of all objects: It is created and later destroyed. Forms have a visual component, so they use system resources, such as handles. These are created and destroyed at interim stages within the lifetime of the form. Forms can be created and will hold state as a class, but will not appear until they are activated.

Table 14-2 summarizes the typical states of a form's existence. For each state, it includes how you get the form to that state, the events that occur when the form enters a state, and a brief description of each.