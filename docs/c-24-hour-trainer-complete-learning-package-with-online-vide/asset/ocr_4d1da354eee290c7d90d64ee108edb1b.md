That means you can set the dialog's return result and close the dialog in a single line of code. Typing one line of code should be no real hardship, but believe it or not, there's an even easier way to close the dialog.

If you set a Button's DialogResult property, the Button automatically sets the form's DialogResult property when it is clicked. For example, suppose you set the cancelButton's DialogResult property to DialogResult.Cancel. When the user clicks the Button, it automatically sets the form's DialogResult property to DialogResult.Cancel so the form automatically closes. That lets you set the return value and close the form without typing any code at all.

If you think setting one Button property is still too much work, you can even avoid that, at least for the Cancel button. When you set a form's CancelButton property, C# automatically sets that Button's DialogResult property to DialogResult.Cancel.

Note that when you set the form's AcceptButton property, C# does not automatically set the Button's DialogResult property. The assumption is that the OK Button might need to validate the data the user entered on the form before it decides whether to close the dialog. For example, if the user doesn't fill in all required fields, the OK Button might display a message asking the user to fill in the remaining fields instead of closing the dialog.

> NOTE Actually these methods hide the dialog so control returns to the calling code, but they don't call its Close method. That means the dialog isn't destroyed so the calling code can look at values entered on the dialog by the user.

If you don't want to perform any validation, you can simply set the OK Button's DialogResult property to DialogResult.OK.

# USING CUSTOM DIALOGS

A program uses a custom dialog in exactly the same way that it uses a standard dialog. It creates, initializes, and displays the dialog. It checks the return result and takes whatever action is appropriate.

There's a slight difference in how the program creates the dialog because you can add standard dialogs to a form at run time and you can't do that with custom dialogs. To use a custom dialog, the code needs to create a new instance of the dialog's form as described in Lesson 9.

The following code shows how a program might display a new customer dialog:

```
// Let the user create a new customer.
private void newCustomerButton_Click(object sender, EventArgs e)
{
    // Create and display a NewCustomerDialog.
    NewCustomerDialog newCustomerDialog;
    newCustomerDialog = new NewCustomerDialog();
    if (newCustomerDialog.ShowDialog() == DialogResult.OK)
```