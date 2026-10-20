# The code for a dialog box that cancels the Closing event

```
private void frmCustomer_FormClosing(object sender, FormClosingEventArgs e)
{
    if (isDataSaved == false)
    {
        string message =
            "This form contains unsaved data.\n\n" +
            "Do you want to save it?";

        DialogResult button =
            MessageBox.Show(message, "Customer",
            MessageBoxButtons.YesNoCancel,
            MessageBoxIcon.Warning);

        if (button == DialogResult.Yes)
        {
            if (IsValidData())
                this.SaveData();
            else
                e.Cancel = true;
        }
        if (button == DialogResult.Cancel)
        {
            e.Cancel = true;
        }
    }
}
```

# The dialog box that’s displayed by the code shown above

![](bbox=[0.155, 0.51, 0.43, 0.63])

# Description

+   - The event handler for the FormClosing event of a form receives a parameter named e that’s created from the FormClosingEventArgs class. The Cancel property of this parameter lets you specify whether or not the event should be canceled. To cancel the event, set this property to true.