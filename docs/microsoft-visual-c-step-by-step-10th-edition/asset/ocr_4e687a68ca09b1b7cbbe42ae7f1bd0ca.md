until you find an exception with the InnerException property set to null (as shown in the previous image). At this point, you have reached the initial exception, and this exception typically highlights the problem you need to address.

+   6. Select Close in the QuickWatch dialog.

+   7. In Visual Studio, on the Debug menu, select Stop Debugging

+   8. Display the code for the file MainPage.xml.cs in the Code and Text Editor window, and locate the addValues method.

+   9. Add a try block (including braces) around the statements inside this method, together with a catch handler for the FormatException exception, as shown in the form:

Click here to view code image

```
try
  int lhs = int.Parse(lhsOperand.Text);
  int rhs = int.Parse(rhsOperand.Text);
  int outcome = 0;

  outcome = lhs + rhs;
  expression.Text = $\$(lhs) + {rhs}";
  result.Text = outcome.ToString();

catch (FormatException fex)
{
  result.Text = fex.Message;
}
```

Now, if a FormatException exception occurs, the catch handler displays the text in the exception's Message property in the Result box at the bottom of the form.

+   10. On the Debug menu, select Start Debugging.

+   11. When the form appears, in the Left Operand box, type John, and in the Right Operand box type 2.

+   12. Select the + Addition button, and then select Calculate.

The catch handler successfully catches the FormatException, and the message “Input string was not in a correct format” is written to the Result box. The