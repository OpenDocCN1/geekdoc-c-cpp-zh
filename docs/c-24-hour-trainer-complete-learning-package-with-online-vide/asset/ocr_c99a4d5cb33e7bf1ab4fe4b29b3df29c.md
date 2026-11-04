```
```
// Calculate the factorial.
long result = 1;
for (long i = 2; i <= value; i++)
{
    result *= i;
}
return result;
```
```

The following code shows how the program might invoke the new version of the Factorial method. It uses a try-catch block to protect itself in case the Factorial method throws an exception. The block also protects against other errors such as the user entering garbage in the TextBox.

```
```
// Calculate the factorial.
private void calculateButton_Click(object sender, EventArgs e)
{
    try
    {
        // Get the input value.
        long number = long.Parse(numberTextBox.Text);

        // Calculate the factorial.
        long answer = Factorial(number);

        // Display the factorial.
        resultTextBox.Text = answer.ToString();
    }
    catch (Exception ex)
    {
        // Display an error message.
        MessageBox.Show(ex.Message);
        resultTextBox.Clear();
    }
}
```
```

> **TIP** Exceptions take additional overhead and disrupt the natural flow of the code, making it harder to read, so only throw exceptions to signal exceptional conditions.
> 
> If a method needs to tell the calling code whether it succeeded or failed, that isn't an exceptional condition so use a return value. If a method has an invalid input parameter (such as a 0 in a parameter that cannot be 0), that's an error, so throw an exception.