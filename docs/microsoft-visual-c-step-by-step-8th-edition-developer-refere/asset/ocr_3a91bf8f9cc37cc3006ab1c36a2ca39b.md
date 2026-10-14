```
{
    addValues();
}
else if ((bool)subtraction.IsChecked)
{
    subtractValues();
}
else if ((bool)multiplication.IsChecked)
{
    multiplyValues();
}
else if ((bool)division.IsChecked)
{
    divideValues();
}
else if ((bool)remainder.IsChecked)
{
    remainderValues();
}
}
catch (FormatException fEx)
{
    result.Text = fEx.Message;
}
catch (OverflowException oEx)
{
    result.Text = oEx.Message;
}
}
```

The *addition, subtraction, multiplication, division,* and *remainder* fields are the buttons that appear on the form. Each button has a property called *IsChecked* that indicates whether the user has selected it. The *IsChecked* property is a nullable Boolean that has the value *true* if the button is selected or *false* otherwise. (You learn more about nullable values in Chapter 8, “Understanding values and references.”) The cascading *if* statement examines each button in turn to find which one is selected. (The radio buttons are mutually exclusive, so the user can select only one radio button at most.) If none of the buttons is selected, none of the *if* statements will be true and none of the calculation methods is called.

You could try to solve the problem by adding one more *else* statement to the *if-else* cascade to write a message to the *result* text box on the form, but a better solution is to separate the detection and signaling of an error from the catching and handling of that error.

+   6. Add another *else* statement to the end of the list of *if-else* statements and throw an *InvalidOperationException* as shown in bold in the following:

Click here to view code image

```
if ((bool)addition.IsChecked)
{
    addValues();
```