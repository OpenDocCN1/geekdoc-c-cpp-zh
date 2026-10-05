8. On the Debug menu, select Start Debugging.

9. In the Left Operand box, type 9876543. In the Right Operand box, type 9876543.

10. Select the * Multiplication button, and then Calculate.

This time, Visual Studio drops into the debugger and reports that the multiplication resulted in an OverflowException exception. You must add a handler to catch this exception and handle it more gracefully than just failing with an error.

11. On the Debug menu, select Stop Debugging.

12. In the Code and Text Editor displaying the MainPage.xaml.cs file, locate the calculateClick method.

13. Add the following catch handler (shown in bold) immediately after the existing FormatException catch handler in this method:

Click here to view code image

```
private void calculateClick(object sender, RoutedEventArgs e)
{
    try
    {
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

The logic of this catch handler is the same as that for the FormatException catch handler. However, it's still worth keeping these handlers separate instead of simply writing a generic Exception catch handler; in the future, you might decide to handle these exceptions differently.

14. On the Debug menu, select Start Debugging to build and run the application.

15. In the Left Operand box, type 9876543. In the Right Operand box, type 9876543.