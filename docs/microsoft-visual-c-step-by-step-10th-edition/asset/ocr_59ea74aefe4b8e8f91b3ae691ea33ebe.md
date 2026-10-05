Click here to view code image

```
private void calculateClick(object sender, RoutedEventArgs e)
{
    try {
        if ((bool)addition.IsChecked)
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
    } catch (FormatException fEx)
    {
        result.Text = fEx.Message;
    }
}
```

+   4. On the **Debug** menu, select **Start Debugging**.
5. When the form appears, in the **Left Operand** box, type **John**, and in the **Right Operand** box, type **2**.
6. Select the **+ Addition** button, and then select **Calculate**.

As before, the `catch` handler successfully catches the `FormatException`, and the message “Input string was not in a correct format” is written to the Result box. However, although the exception was thrown in the `addValues` method, the handler caught it in the `calculateClick` method.

+   7. Select the – **Subtraction** button, and then select **Calculate.**.