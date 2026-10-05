
# The code for the Future Value application

private void btnFutureValue.Click(object sender, System.EventArgs e)
{
```csharp
try {
    if (IsValidData()) {
        decimal monthlyInvestment =
            Convert.ToDecimal(txtMonthlyInvestment.Text);
        decimal yearlyInterestRate =
            Convert.ToDecimal(txtInterestRate.Text);
        int years = Convert.ToInt32(txtYears.Text);

        int months = years * 12;
        decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;
        decimal futureValue = CalculateFutureValue(
            monthlyInvestment, monthlyInterestRate, months);

        txtFutureValue.Text = futureValue.ToString("c");
        txtMonthlyInvestment.Focus();
    }
} catch (Exception ex) {
    MessageBox.Show(ex.Message + "\n\n" +
        ex.GetType().ToString() + "\n" + 
        ex.StackTrace, "Exception");
}
```

public bool IsValidData()
{
```csharp
return
    IsPresent(txtMonthlyInvestment, "Monthly Investment") &&
    IsDecimal(txtMonthlyInvestment, "Monthly Investment") &&
    IsWithinRange(txtMonthlyInvestment, "Monthly Investment", 1, 1000) &&

    IsPresent(txtInterestRate, "Yearly Interest Rate") &&
    IsDecimal(txtInterestRate, "Yearly Interest Rate") &&
    IsWithinRange(txtInterestRate, "Yearly Interest Rate", 1, 20) &&

    IsPresent(txtYears, "Number of Years") &&
    IsInt32(txtYears, "Number of Years") &&
    IsWithinRange(txtYears, "Number of Years", 1, 40);
```

public bool IsPresent(TextBox textbox, string name)
{
```csharp
if (textbox.Text == "") {
    MessageBox.Show(name + " is a required field.", "Entry Error");
    textbox.Focus();
    return false;
}
return true;
```

7-12 The code for the Future Value application (part 1 of 2)

# The code for the Future Value application

public bool IsDecimal(TextBox textBox, string name)
{
```csharp
  try {
    Convert.ToDecimal(textBox.Text);
    return true;
  }
  catch (FormatException ex) {
    MessageBox.Show(name + " must be a decimal value.", "Entry Error");
    textBox.Focus();
    return false;
  }
}
```

public bool IsInt32(TextBox textBox, string name)
{
```csharp
  try {
    Convert.ToInt32(textBox.Text);
    return true;
  }
  catch (FormatException ex) {
    MessageBox.Show(name + " must be an integer.", "Entry Error");
    textBox.Focus();
    return false;
  }
}
```

public bool IsWithinRange(TextBox textBox, string name, decimal min, decimal max)
{
```csharp
  decimal number = Convert.ToDecimal(textBox.Text);
  if (number < min || number > max) {
    MessageBox.Show(name + " must be between " + min + " and " + max + ".", "Entry Error");
    textBox.Focus();
    return false;
  }
  return true;
}
```

private decimal CalculateFutureValue(decimal monthlyInvestment, decimal monthlyInterestRate, int months)
{
```csharp
  decimal futureValue = 0;
  for (int i = 0; i < months; i++) {
    futureValue = (futureValue + monthlyInvestment) * (1 + monthlyInterestRate);
  }
  return futureValue;
}
```

Figure 7-12 The code for the Future Value application (part 2 of 2)

# Perspective

In this chapter, you learned how to handle exceptions and validate data so you can code applications that are “bulletproof.” This means your applications won't throw unhandled exceptions no matter what data the user enters or how the user works with the user interface. This is an essential feature of any professional application.

But there's a lot more for you to learn about the C# language. So in chapter 8, you'll learn how to work with arrays and collections. In chapter 9, you'll learn how to work with dates, and you'll learn more about working with strings. And in chapter 10, you'll learn how to develop forms that use other types of controls. When you finish these chapters, you'll be able to develop applications of considerable complexity.

# Terms

- exception
- throw an exception
- catch an exception
- exception handling
- subclass
- structured exception handling
- try-catch statement
- exception handler
- try block
- catch block
- stack trace
- finally block
- throw statement
- data validation
- range checking

# Exercise 7-1 Enhance the Invoice Total application

This exercise guides you through the process of enhancing the Invoice application so it catches any runtime errors and validates the Subtotal entry.

- 1. Open the application that's in the C:\C# 2010\Chapter 07\InvoiceTotal directory. This is the version that you worked on in chapter 4.

- 2. Add a try-catch statement to the btnCalculate_Click method so it catches any exception that the ToDecimal method of the Convert class might throw. The catch block should display a dialog box like the one in figure 7-12.

- 3. Add a try-catch statement to the btnCalculate_Click method so it catches any exception that the ToDecimal method of the Convert class might throw. The catch block should display a dialog box like the one in figure 7-12.

- 4. Add a try-catch statement to the btnCalculate_Click method so it catches any exception that the ToDecimal method of the Convert class might throw. The catch block should display a dialog box like the one in figure 7-12.

# Exercise 7-2 Enhance the Invoice application

This exercise guides you through the process of enhancing the Invoice application so it catches any runtime errors and validates the Subtotal entry.

- 1. Open the application that's in the C:\C# 2010\Chapter 07\InvoiceTotal directory. This is the version that you worked on in chapter 4.

- 2. Add a try-catch statement to the btnCalculate_Click method so it catches any exception that the ToDecimal method of the Convert class might throw. The catch block should display a dialog box like the one in figure 7-12.

- 3. Add a try-catch statement to the btnCalculate_Click method so it catches any exception that the ToDecimal method of the Convert class might throw. The catch block should display a dialog box like the one in figure 7-12.
