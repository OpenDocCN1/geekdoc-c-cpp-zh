![](bbox=[0.177, 0.095, 0.792, 0.29])

**Figure 15-20** Wiring the same event to three RadioButton objects

Example 15-8 shows the event-handler method for the RadioButton CheckedChanged( ) event.

# Example 15-8

```
```csharp
private void radioButton_CheckedChanged(object sender,
                                       System.EventArgs e)
{
    if (this.radBtnFresSop.Checked)
    {
        this.lblClassif.Text =
            "Freshmen & Sophomores ";
    }
    else if (this.radBtnJrSr.Checked)
    {
        this.lblClassif.Text = "Junior & Seniors ";
    }
    else if (this.radBtnOther.Checked)
    {
        this.lblClassif.Text = "Special Students ";
    }
    this.lblClassif.Text += " Always Welcome!";
}
```
```

The event-handler method for the Submit button is used to retrieve the values entered into the TextBox fields and the selections made from the ListBox object by the user. These values are used to populate the Label controls that are to be displayed when the page is reloaded for the client. Example 15-9 shows the btnSubmit event-handler method.