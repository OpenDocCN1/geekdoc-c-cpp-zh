8. The Text of the outputLabel will be updated when the Text of the inputTextBox is changed. The code line outputLabel.Text = inputTextBox.Text.ToUpper(); does the required job. It takes the Text of the inputTextBox, converts it to all-capitals by the method ToUpper() and then assigns the result to the Text of outputLabel. We'll write this code line inside the inputTextBox_TextChanged() method as follows:

```
private void inputTextBox_TextChanged(object sender,
EventArgs e)
{
    outputLabel.Text = inputTextBox.Text.ToUpper();
}
```

Code 6.18

9. Build and run the project. The following program window with tabs will appear:

![](bbox=[0.27, 0.56, 0.7, 0.83])

Figure 6.58. The program with TabControl

When we enter a text in the TextBox of the Input tab, this text will be converted to upper case and then written on the Label of the Output Tab as shown in Figures 6.59 and 6.60, respectively. Please note that we didn't need to place a Button to fire the conversion process because the inputTextBox_TextChanged() method automatically executes whenever we change the text of the inputTextBox.