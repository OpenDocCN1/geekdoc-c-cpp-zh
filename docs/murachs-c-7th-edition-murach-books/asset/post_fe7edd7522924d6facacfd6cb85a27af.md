
# How to handle multiple events with one event handler

In some cases, you’ll want to use the same event handler to handle two or more events. For example, it’s common to use one event handler for the TextChanged event of multiple text boxes on a form. To do that, you can use the procedure shown in figure 6-11.

To start, you must generate the event handler as described in figure 6-9. Typically, you will want to give this event handler a name that’s not specific to any one control. Suppose, for example, that at any time the user changes the value in one of the first three text boxes on the Future Value form, you want to clear the future value that’s currently displayed. Then, when you create the event handler for the first text box, you might give this event handler the name ClearFutureValue().

Once you’ve created this event handler, it will appear in the drop-down list of the event handlers that are available. In this figure, for example, you can see that the ClearFutureValue() event handler is included in the drop-down list for the TextChanged event of the Yearly Interest Rate text box. Then, you can select this event handler to generate a statement that wires the event to the event handler.

## How to select an existing event handler for an event

![](img/844f608d10a44654833ea5efc8a2e7a7_210_0.png)

## How to wire an event to an existing event handler

- 1. Select the control in the Form Designer.
- 2. If necessary, click the Events button in the Properties window to display a list of the events for the control.
- 3. Click to the right of the event you want to handle and display the drop-down list.
- 4. Select the event handler you want to use for that event.

## Description

- The drop-down list that’s available for each event includes all of the existing event handlers for the current form.
- When you select an event handler from the drop-down list, Visual Studio generates a statement that wires the event to the event handler.

# Another version of the Future Value application

Now that you know how to code methods and work with event handlers, you’re ready to see an enhanced version of the Future Value application. This version uses a private method to calculate the future value, and it uses a single event handler to clear the Future Value text box whenever the user changes the text in any of the other text boxes on the form.

Figure 6-12 shows the code for the event handlers and CalculateFutureValue() method of the Future Value application. This includes the event handlers for the Click events of the Calculate and Exit buttons, and it includes a custom event handler named ClearFutureValue() that handles the TextChanged event of the first three text boxes on the form.

The CalculateFutureValue() method contains the code that calculates the future value. It’s called by the shaded code in the event handler for the Click event of the Calculate button. This separates the calculation from the other code for the event. In a lengthy event handler, using methods like this can make it easier to code, test, and debug an application. You’ll see more of this in the next chapter.

The ClearFutureValue() event handler contains a single statement that sets the Text property of the Future Value text box on an empty string. In other words, it clears the future value that’s displayed on the form. Since this event handler is wired to the TextChanged event of the first three text boxes on this form, this code clears the Future Value text box every time the user changes a value in any of the other text boxes. Then, the future value isn’t displayed until the user clicks the Calculate button again. As a result, this code prevents the Future Value text box from displaying a value that isn’t accurate for the values that are displayed in the other text boxes.

# The code for the methods for the Future Value application

```
private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal monthlyInvestment = Convert.ToDecimal(txtMonthlyInvestment.Text);
    decimal yearlyInterestRate = Convert.ToDecimal(txtInterestRate.Text);
    int years = Convert.ToInt32(txtYears.Text);

    int months = years * 12;
    decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;

    decimal futureValue = this.CalculateFutureValue(monthlyInvestment, monthlyInterestRate, months);
    txtFutureValue.Text = futureValue.ToString("c");
    txtMonthlyInvestment.Focus();
}
```

```
private decimal CalculateFutureValue(decimal monthlyInvestment,
    decimal monthlyInterestRate, int months)
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

```
private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}
```

```
private void ClearFutureValue(object sender, EventArgs e)
{
    txtFutureValue.Text = "";
}
```

- The CalculateFutureValue() method separates the calculation from the rest of the code for the event handler for the Click event of the Calculate button.
- The TextChanged event of the Monthly Investment, Yearly Interest Rate, and Number of Years text boxes is wired to the ClearFutureValue() event handler. As a result, the Future Value text box will be cleared every time the user changes the data in one of those text boxes.

Figure 6-12 The event handlers and the other method of the Future Value application

# Some of the generated code

Figure 6-13 shows a partial listing of the generated code for the Future Value application. This code is stored in the Designer.cs file for the form within the Windows Form Designer generated code region. In this figure, you can see the code that’s generated for three controls: one button and two text boxes.

To start, the InitializeComponent() method creates objects from the appropriate control classes and assigns those objects to the appropriate variables, which have already been declared. Next, the InitializeComponent() method includes a group of statements for each control. Most of these statements set the starting properties for these controls.

However, the last statement in each group wires an event to an event handler. Here, the Click event of the Calculate button is wired to an event handler named btnCalculate_Click(), and the TextChanged events of the two text boxes are wired to an event handler named ClearFutureValue(). (Although it isn’t shown in this listing, the TextChanged event of the third text box on this form is also wired to the ClearFutureValue() event handler.)

As the warning at the top of this listing suggests, you should avoid modifying this code with a code editor. However, you should also be aware that this generated code exists and that it is essential to the proper operation of your application. In addition, there are times when using the Code Editor to directly modify this code may be easier than using the Form Designer to indirectly modify this code. If, for example, you start an event handler and decide to delete it, you may want to use the Code Editor to delete the wiring statement. Fortunately, this doesn’t cause any problems for the Form Designer.

# Some of the generated code in the Designer.cs file for the form

```
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
    ...
    //
    // btnCalculate
    //
    this.btnCalculate.Location = new System.Drawing.Point(54, 126);
    this.btnCalculate.Name = "btnCalculate";
    this.btnCalculate.Size = new System.Drawing.Size(75, 23);
    this.btnCalculate.TabIndex = 8;
    this.btnCalculate.Text = "&Calculate";
    this.btnCalculate.Click +=
        new System.EventHandler(this.btnCalculate_Click);
    //
    // txtInterestRate
    //
    this.txtInterestRate.Location = new System.Drawing.Point(132, 37);
    this.txtInterestRate.Name = "txtInterestRate";
    this.txtInterestRate.Size = new System.Drawing.Size(84, 20);
    this.txtInterestRate.TabIndex = 3;
    this.txtInterestRate.TextChanged +=
        new System.EventHandler(this.ClearFutureValue);
    //
    // txtMonthlyInvestment
    //
    this.txtMonthlyInvestment.Location = new System.Drawing.Point(132, 9);
    this.txtMonthlyInvestment.Name = "txtMonthlyInvestment";
    this.txtMonthlyInvestment.Size = new System.Drawing.Size(84, 20);
    this.txtMonthlyInvestment.TabIndex = 1;
    this.txtMonthlyInvestment.TextChanged +=
        new System.EventHandler(this.ClearFutureValue);
    ...
}

#endregion

private System.Windows.Forms.Button btnCalculate;
private System.Windows.Forms.TextBox txtInterestRate;
private System.Windows.Forms.TextBox txtMonthlyInvestment;
...
```

## Description

- The InitializeComponent() method creates an instance of each control on the form, assigns each control to a variable, sets the properties of each control, and wires control events to the appropriate event handlers.
