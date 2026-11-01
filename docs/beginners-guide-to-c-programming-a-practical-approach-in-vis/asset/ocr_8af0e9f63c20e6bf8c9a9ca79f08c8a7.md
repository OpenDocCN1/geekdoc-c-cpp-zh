6. In order to show the selected date in a message box, we’ll take the Value property of the DateTimePicker inside the event handler of the button as follows:

```
private void showDateButton_Click(object sender, EventArgs e)
{
    MessageBox.Show(dateTimePicker1.Value.ToLongDateString());
}
```

Code 5.6

Since the Name property of the DateTimePicker control is dateTimePicker1 by default, we take its Value property and convert it to a string using the method toLongDateString() for being able to show in the message box.

7. Now, build and run the project:

![](bbox=[0.35, 0.62, 0.75, 0.85])

Figure 5.28. The DateTimePicker example

Current date is shown in the DateTimePicker by default. We can select another date from the list by clicking the arrowhead to the right of the DateTimePicker as in Figure 5.29.

We may now click the Show Selected Date button to shown the picked date in a message box as shown in Figure 5.30.