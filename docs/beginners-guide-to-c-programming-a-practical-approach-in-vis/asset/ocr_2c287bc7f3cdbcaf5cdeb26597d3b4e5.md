7. Similarly, double-click on the NumericUpDown control so that its default event handler evenNumericUpDown_ValueChanged(...) will be created. This method will be called when the value of the NumericUpDown is changed:

```
private void evenNumericUpDown_ValueChanged(object sender,
EventArgs e)
{
    numbersListBox.Items.Add(evenNumericUpDown.Value.ToString());
}
```

Code 5.20

In this code line, the Value of the evenNumericUpDown control is read and converted to string. This string representation is then passed to the Add() method of the numbersListBox.Items so that the value displayed in the evenNumericUpDown is added to the numbersListBox each time the value of the evenNumericUpDown is changed.

8. We can now build and run the project. The program will appear as follows:

![](bbox=[0.4, 0.68, 0.7, 0.88])

Figure 5.74. The program when it first starts

As we increase/decrease the value of the NumericUpDown control, its value will be added to the ListBox as shown in Figure 5.75.