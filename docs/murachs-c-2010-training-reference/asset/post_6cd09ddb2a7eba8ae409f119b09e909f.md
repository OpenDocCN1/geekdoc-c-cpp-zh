
# The code for the methods for the Future Value application

```csharp
private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal monthlyInvestment = Convert.ToDecimal(txtMonthlyInvestment.Text);
    decimal yearlyInterestRate = Convert.ToDecimal(txtInterestRate.Text);
    int years = Convert.ToInt32(txtYears.Text);

    int months = years * 12;
    decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;

    decimal futureValue = this.CalculateFutureValue(
        monthlyInvestment, monthlyInterestRate, months);
    txtFutureValue.Text = futureValue.ToString("c");
    txtMonthlyInvestment.Focus();
}
```

```csharp
private decimal CalculateFutureValue(decimal monthlyInterestRate, int months)
{
    decimal futureValue = 0m;
    for (int i = 0; i < months; i++)
    {
        futureValue = (futureValue + monthlyInvestment)
        * (1 + monthlyInterestRate);
    }
    return futureValue;
}
```

```csharp
private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}
```

```csharp
private void ClearFutureValue(object sender, EventArgs e)
{
    txtFutureValue.Text = "";
}
```

# Description

- The CalculateFutureValue method separates the calculation from the rest of the code for the event handler for the Click event of the Calculate button
- The TextChanged event of the Monthly Investment, Yearly Interest Rate, and Number of Years text boxes is wired to the ClearFutureValue event handler. As a result, the Future Value text box will be cleared every time the user changes the data in one of those boxes.

![](img/3148667e42d4db35b3d08576aaa1fa01_198_0.png)

# Some of the generated code

Figure 6-10 shows a partial listing of the generated code for the Future Value application. This code is stored in the Designer.cs file for the form within the Windows Form Designer generated code region. In this figure, you can see the code that's generated for three controls: one button and two text boxes.

To start, the InitializeComponent method creates objects from the appropriate classes and assigns those objects to the appropriate variables, which have already been declared. Next, the InitializeComponent method includes a group of statements for each control. Most of these statements set the starting properties for these controls.

However, the last statement in each group wires an event to an event handler. Here, the TextChanged events of the two text boxes are wired to an event handler named ClearFutureValue, and the Click of the Calculate button is wired to an event handler named btnCalculate_Click. (Although it isn't shown in this listing, the TextChanged event of the third text box on this form is also wired to the ClearFutureValue event handler.)

As the warning at the top of this listing suggests, you should avoid modifying this code with a code editor. However, you should be aware that this generated code exists and that it is essential to the proper operation of your application. In addition, there are times when using the Code Editor to directly modify this code may be easier than using the Form Designer to indirectly modify this code. If, for example, you start an event handler and decide to delete it, you may want to use the Code Editor to delete the wiring statement. Fortunately, this doesn't cause any problems for the Form Designer.

# Some of the generated code in the Designer.cs file for the form

```csharp
#region Windows Form Designer generated code
/// <summary>
/// Required method for Designer support - do not modify
/// the contents of this method with the code editor.
/// </summary>
private void InitializeComponent()
{
    this.btnCalculate = new System.Windows.Forms.Button();
    this.txtInterestRate = new System.Windows.Forms.TextBox();
    this.txtMonthlyInvestment = new System.Windows.Forms.TextBox();
    // ...
    // btnCalculate
    this.btnCalculate.Location = new System.Drawing.Point(54, 126);
    this.btnCalculate.Name = "btnCalculate";
    this.btnCalculate.Size = new System.Drawing.Size(75, 23);
    this.btnCalculate.TabIndex = 18;
    this.btnCalculate.Text = "&Calculate";
    this.btnCalculate.EventHandler += (this.btnCalculate.Click);
    // ... txtInterestRate
    this.txtInterestRate.Location = new System.Drawing.Point(132, 37);
    this.txtInterestRate.Name = "txtInterestRate";
    this.txtInterestRate.Size = new System.Drawing.Size(84, 20);
    this.txtInterestRate.TabIndex = 16;
    this.txtInterestRate.TextChanged += (this.ClearFutureValue);
    // ... txtMonthlyInvestment
    this.txtMonthlyInvestment.Location = new System.Drawing.Point(132, 92);
    this.txtMonthlyInvestment.Name = "txtMonthlyInvestment";
    this.txtMonthlyInvestment.Size = new System.Drawing.Size(84, 20);
    this.txtMonthlyInvestment.TabIndex = 15;
    this.txtMonthlyInvestment.TextChanged += (this.ClearFutureValue);

...
}
#endregion

private System.Windows.Forms.Button btnCalculate;
private System.Windows.Forms.TextBox txtInterestRate;
private System.Windows.Forms.TextBox txtMonthlyInvestment;
```

# Description

- The InitializeComponent method creates objects from the appropriate classes and assigns those objects to the appropriate variables, which have already been declared. Next, the InitializeComponent method includes a group of statements for each control. Most of these statements set the starting properties for these controls.
- However, the last statement in each group wires an event to an event handler. Here, the TextChanged events of the two text boxes are wired to an event handler named ClearFutureValue, and the Click of the Calculate button is wired to an event handler named btnCalculate_Click. (Although it isn't shown in this listing, the TextChanged event of the third text box on this form is also wired to the ClearFutureValue event handler.)

![](img/3148667e42d4db35b3d08576aaa1fa01_200_0.png)

# Perspective

Now that you have finished this chapter, you should be able to code and call methods. With those skills, you are well on your way toward developing programs at professional level.

# Terms

- method
- access modifier
- return statement
- parameter
- parameter list
- signature
- overloading a method
- argument
- argument list
- optional parameter
- pass by position
- pass by name
- pass by value
- pass by reference
- event wiring
- delegate

# Exercise 6-1

# Enhance the Future Value application

In this exercise, you'll enhance the Future Value application that you created in chapter 5 so it works like figure 6-9.

Use refactoring to create theFutureValue method

1. Open the application that's in C:\C# 2010\Chapter 6\FutureValue directory.
2. Use refactoring as shown in figure 6-4 to refactor the event handler and create a new method named FutureValue.
3. Test the application to make sure the new method works.

Add the FutureValue method without refactoring

4. Press Ctrl-Z several times to return the code to the way before you refactored.
5. Add a method named FutureValue that works like figure 6-9. To do that, start the type of the new method including its starting and ending braces. Then, move the related code from the btnCalculate_Click method to the block within the new method and modify it where necessary.
6. Modify the code in the btnCalculate_Click method so it calls the FutureValue method. As you enter the call to the method, note how the IntelliSense feature helps you understand the arguments.
7. Test the application to make sure this new method works.

Add an event handler for the Text event

8. In the Properties Designer, select the first text box. Then, click the Events button to display the Events list for your text box. Review the events that are generated.
9. Enter "ClearFutureValue" to the right of the TextChanged event and press Enter. When you do, the Code Editor will open and an event handler ClearFutureValue will be created. Enter a statement that clears the Future Value text box as shown in figure 6-9.
10. Open the Form1.Designer.cs file for, expand the Forms generated region, and locate the statements that set the properties of the Monthly investment text box. At the end of those statements, you'll find a statement that wires the TextChanged event of this control to the ClearFutureValue event handler.
11. Return to the Form Designer and select the Yearly Interest Rate text box. Drop down the list for the TextChanged event of this control, and notice that the ClearFutureValue event handler is included in this list. Select this event handler to wire the event to it. Repeat this for the Number of Years text box.
