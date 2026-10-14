3. Find the calculateClick method. Add to this method the try block and catch handler shown in bold in the following example:

Click here to view code image

```
private void calculateClick(object sender, RoutedEventArgs e)
{
    try

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
    }
    catch (FormatException fEx)
    {
        result.Text = fEx.Message;
    }
}
```

4. On the Debug menu, click Start Debugging.

5. When the form appears, in the Left Operand box, type John, and in the Right Operand box, type 2. Click the + Addition button, and then click Calculate.

As before, the catch handler successfully catches the FormatException, and the message “Input string was not in a correct format” is written to the Result text box. However, bear in mind that the exception was actually thrown in the addValues method, but it was caught by the handler in the calculateClick method.

6. Click the – Subtraction button, and then click Calculate.

This time, the subtractValues method causes the exception, but it is propagated back to the calculateClick method and handled in the same manner as before.

7. Test the * Multiplication, / Division, and % Remainder buttons, and verify