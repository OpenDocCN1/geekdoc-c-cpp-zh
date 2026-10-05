When the form runs, the Text property of each of these controls holds the values that the user enters.

+   4. Toward the bottom of the form, verify that the TextBlock control used to display the expression being evaluated is named expression and that the TextBlock control used to display the result of the calculation is named result.

+   5. Close the Document Outline window.

+   6. On the View menu, select Code to display the code for the MainPage.xaml.cs file in the Code and Text Editor window.

+   7. In the Code and Text Editor window, locate the addValues method. It looks like this:

Click here to view code image

```
private void addValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: Add rhs to lhs and store the result in outcome
    expression.Text = $"{lhsOperand.Text} + {rhsOperand.Text}";
    result.Text = outcome.ToString();
}
```

The body of this method contains six statements:

+   The first statement in this method declares an int variable called lhs and initializes it with the integer corresponding the value typed by the user in the lhsOperand box. Remember that the Text property of a TextBox contains a string, while lhs is an int, you must convert this string to an integer before you assign it to lhs. The int data type provides the int.Parse method, which does precisely this.

+   The second statement declares an int variable called rhs and initializes it to the value in the rhsOperand box after converting it to an int.

+   The third statement declares an int variable called outcome.

+   The fourth statement consists of a comment that states that you need to add rhs to lhs and store the result in outcome. This is the missing bit of code that you need to implement, which you'll do in the next step.