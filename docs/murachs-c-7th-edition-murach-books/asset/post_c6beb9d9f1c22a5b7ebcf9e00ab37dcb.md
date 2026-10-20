
![](img/844f608d10a44654833ea5efc8a2e7a7_180_0.png)

## The Future Value form

## The property settings for the form

| Default name | Property | Setting |
|---|---|---|
| Form1 | Text | Future Value |
|  | AcceptButton | btnCalculate |
|  | CancelButton | btnExit |
|  | StartPosition | CenterScreen |

## The property settings for the controls

| Default name | Property | Setting |
|---|---|---|
| label1 | Text | Monthly Investment: |
| label2 | Text | Yearly Interest Rate: |
| label3 | Text | Number of Years: |
| label4 | Text | Future Value: |
| textBox1 | Name | txtMonthlyInvestment |
| textBox2 | Name | txtInterestRate |
| textBox3 | Name | txtYears |
| textBox4 | Name | txtFutureValue |
|  | ReadOnly | True |
|  | TabStop | False |
| button1 | Name | btnCalculate |
|  | Text | &Calculate |
| button2 | Name | btnExit |
|  | Text | E&xit |

## Additional property settings

- The TextAlign property of each of the labels is set to MiddleLeft.
- The TabIndex properties of the controls are set so the focus moves from top to bottom and left to right.

## The code for the form

Figure 5-13 presents the code for the Future Value form. Like the code for the Invoice Total form, this code consists of two event handlers: one for the Click event of the Calculate button and one for the Click event of the Exit button. Here, most of the processing occurs in the event handler for the Click event of the Calculate button.

The first three statements in this event handler declare and initialize the variables that will be used to store the values that the user enters into the three text boxes. Here, the ToDecimal() and ToInt32() methods of the Convert class are used to convert the string values that are returned from the Text property of the text boxes to the appropriate numeric data types.

The next two statements perform calculations that convert the yearly values entered by the user to monthly values. That way, all of the variables used in the future value calculation will be in terms of months. The first statement converts the number of years to months by multiplying the years by 12. The second statement divides the yearly interest rate by 12 to get a monthly interest rate, and then divides that result by 100 to convert the number to a percentage.

The next group of statements uses a for loop to calculate a new future value for each month of the investment. Here, the variable that stores the future value is declared before the loop so it can be used after the loop finishes its processing. Then, within the loop, the single assignment statement that calculates the future value is executed once for each month. Since this loop contains a single statement, it doesn’t require braces. However, to clearly identify the start and end of the loop, I included these braces anyway.

Within the loop, the arithmetic expression adds the monthly investment amount to the future value, which has an initial value of zero. Then, the expression multiplies that sum by 1 plus the monthly interest rate. If, for example, the monthly investment amount is $100 and the monthly interest rate is 1% (or .01), the future value is $101 after the expression is executed the first time through the loop:

```
(0 + 100) * (1 +.01) = 100 * 1.01 = 101
```

And the future value is $203.01 after the expression is executed the second time:

```
(101 + 100) * (1 + .01) = 201 * 1.01 = 203.01
```

Continue this process for as many months as the user indicates, and the future value will contain the correct result for a series of equal monthly investments.

After the loop ends, the next statement formats the future value and displays it on the form. To do that, the ToString() method converts a decimal value to a string that uses the currency format. Then, this string value is assigned to the Text property of the Future Value text box. Finally, the last statement moves the focus to the Monthly Investment text box to prepare for the next calculation.

To keep this program simple, it doesn’t validate the data that’s entered by the user. As a result, an exception will occur if the user enters nonnumeric data in one of the text boxes. In chapter 7, you’ll learn how to add data validation to this program to prevent exceptions like this.

## The code for the event handlers in the Future Value application

```
private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal monthlyInvestment =
        Convert.ToDecimal(txtMonthlyInvestment.Text);
    decimal yearlyInterestRate = Convert.ToDecimal(txtInterestRate.Text);
    int years = Convert.ToInt32(txtYears.Text);

    int months = years * 12;
    decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;

    decimal futureValue = 0m;
    for (int i = 0; i < months; i++)
    {
        futureValue = (futureValue + monthlyInvestment)
            * (1 + monthlyInterestRate);
    }

    txtFutureValue.Text = futureValue.ToString("c");
    txtMonthlyInvestment.Focus();
}

private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}
```

## Description

- This application uses a for loop to calculate the future value of a monthly investment amount. For this calculation to work correctly, all of the variables that it uses must be converted to the same time period. In this case, that time period is months.
- Each time through the for loop, the assignment statement adds the monthly investment amount to the future value, which starts at zero. Then, this sum is multiplied by 1 plus the monthly interest rate. The result is stored in the futureValue variable so it can be used the next time through the loop.
- Since this application doesn’t provide data validation, the user will be able to enter invalid data, which will cause an exception to occur.

## Perspective

Now that you’ve finished this chapter, you should know how to code if statements, switch statements, switch expressions, conditional expressions, while statements, do-while statements, and for statements. These are the C# statements and expressions that implement the selection, case, and iteration structures, and they provide the logic of an application. Once you master them, you’ll be able to develop significant C# applications.

## Terms

|  |  |
|---|---|
| Boolean expression | discard |
| relational operator | conditional operator |
| logical operator | ternary operator |
| short-circuit operator | conditional expression |
| if-else statement | iteration structure |
| if statement | while statement |
| selection structure | while loop |
| block scope | do-while statement |
| nested if statement | do-while loop |
| switch statement | infinite loop |
| case structure | for statement |
| match expression | for loop |
| case label | jump statement |
| default label | continue statement |
| break statement | breakpoint |
| fall through | margin indicator bar |
| no fall through rule | execution point |
| switch expression | step through code |
| lamda operator |  |

## Exercise 5-1 Enhance the Invoice Total application

In this exercise, you’ll use if-else and switch statements to determine the discount percent for the Invoice Total application that’s in figure 5-7.

## Open the application and change the if-else statement

1. Open the application that’s in the C:\C#\Chapter 05\InvoiceTotal directory.
2. Change the if-else statement so customers of type R with a subtotal that is greater than or equal to $250 but less than $500 get a 25% discount and those with a subtotal of $500 or more get a 30% discount. Next, change the if-else statement so customers of type C always get a 20% discount. Then, test the application to make sure this works.
3. Use code snippets to add another customer type to the if-else statement so customers of type T get a 40% discount for subtotals of less than $500, and a 50% discount for subtotals of $500 or more. Also, make sure that customer types that aren’t R, C, or T get a 10% discount. Then, test the application.
4. Test the application again, but use lowercase letters for the customer types. Note that these letters aren’t evaluated as capital letters. Now, close the application and modify the code so the users can enter either capital or lowercase letters for the customer types. Then, test the application to make sure it works correctly.

## Use a switch statement with if-else statements to get the same results

5. Use a code snippet to enter the start of a switch statement right after the if-else statement. Next, enhance this code so the switch statement provides the structure for handling the three cases for customer types: R, C, and T (but not r, c, and t). Then, within each of these cases, you can copy the related code from the if-else statement above to provide for the discounts that are based on subtotal variations. In other words, the if-else statements will be nested within the switch cases.
6. Comment out the entire if-else statement above the switch statement. Then, test to make sure the switch statement works correctly. Is this code easier to read and understand?
7. When you’re through experimenting, close the project.
