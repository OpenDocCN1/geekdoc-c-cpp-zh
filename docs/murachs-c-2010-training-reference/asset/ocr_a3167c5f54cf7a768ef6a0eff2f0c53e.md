# The Payment form displayed as a dialog box

![](bbox=[0.065, 0.101, 0.843, 0.443])

# Properties for creating custom dialog boxes

| Property | Description |
| --- | --- |
| BorderStyle | Typically set to FixedDialog to prevent the user from resizing the form by dragging its border. |
| ControlBox | Typically set to false the control box and the Maximize, Minimize, and Close buttons don't appear in the title bar of the form. |
| MaximizeBox | Typically set to false so the user can't maximize the form by double-clicking the title bar. |
| MinimizeBox | Can be set to false to prevent the Minimize button from being displayed if the ControlProperty is set to true. |

# Code that creates and displays a dialog box

```
Form paymentForm = new frmPayment();
paymentForm.ShowDialog();
// execution continues here after the user responds to the dialog box
```

# Description

+   * If you display a form as a dialog box, the user must respond to the form before continuing to any other forms. A form like this is sometimes referred to as a custom dialog box or a modal form.
* You use the ShowDialog method of a form object to display the form as a dialog box. After the user responds to the dialog box, execution continues with the statement that follows the ShowDialog method.

Figure 10-11 How to display a form as a dialog box