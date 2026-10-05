
# How to use refactoring to create a new method and its calling statement

In chapter 3, you were introduced to refactoring, which refers to the process of revising and restructuring existing code. This can be especially helpful when you want to create a new method from some code that's in an event handler. This process is illustrated in figure 6-4. To refactor the code, you just select the code you want to create a method from, right-click on the selected code, choose the Extract Method command from the Refactor submenu, and enter a name for the new method.

In this figure, you can see that refactoring creates both a statement and a new method CalculateFutureValue. The only significant difference between this method and the CalculateFutureValue method in figure 6-1 is that the refactored method includes the static keyword. Similarly, the only significant difference in the refactored statement in figure 6-2 is that the calling statement doesn't use this keyword. This is necessary because the keyword refers to the object created from the class for the form. As a result, you can't use this keyword to call a static method. For more information about working with static methods, please see chapter 12.

Incidentally, for the CalculateFutureValue method, the static keyword isn't necessary. As a result, if you want, you can use this keyword to call this method. Then, all of the code's generated when you use refactoring to create a new method works without any changes, so there's usually no need to edit it.

That's powerful stuff! With just a few mouse clicks and keystrokes, you can extract methods from event handlers. This in turn can make your code more manageable by keeping the event handlers shorter and easier to read.

# The btnCalculate_Click method with selected statements

```c
private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal monthlyInvestment = Convert.ToDecimal(txtMonthlyInvestment.Text);
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
```

# The method that replaces the selected code

decimal futureValue = CalculateFutureValue(monthlyInvestment, monthlyInterestRate);

# The method that's added to the class

```csharp
private static decimal CalculateFutureValue(decimal monthlyInvestment, int months, decimal monthlyInterestRate)
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

# How to use refactoring to create a new method from existing code

- 1. Select the code you want to create a new method from. Then, right-click on the selection, and choose Refactor→Extract Method from the shortcut menu.
- 2. In the Extract Method dialog box, enter the name that you want to use for the new method and click OK. This adds a new method to the class and replaces the selected code with a call statement that calls the method.

# Description

- If you want to extract a method from existing code, refactoring makes that easy with the Extract Method command.
- Note in the code above that the refactored code doesn't use this keyword in the method call and includes the static keyword in the method declaration. You'll learn more about the static keyword in chapter 12.

![](img/3148667e42d4db35b3d08576aaa1fa01_188_0.png)

# When and how to pass arguments by reference and by value

By default, the arguments passed to a method are *by value*. That means that the value of each passed variable is assigned to the corresponding parameter in the method. Because of that, the method can change the value of the parameter without affecting the value of the variable in the calling method.

In some cases, though, you'll want to be able to change the value of the variable in the calling method from the called method. To do that, you can pass the argument by *reference* as shown in figure 6-5. Here, the *ref* keyword is coded before the method, and before the parameter declaration. Then, when you call the method, a reference to the variable that you specify for the corresponding argument is passed to the method. As a result, if the method changes the value of the parameter, it also changes the value of the variable in the passed by reference. Then, when the method changes the fourth parameter, the method changes

In this figure, the first three arguments are passed by value, but the fourth is passed by reference. When the method changes the variable in the calling method it is also changed. As a result, there's no need for the method to return the value of the `futureValue` variable.

In general, though, it's better to pass arguments by value instead of by reference. That way, the data in the calling method can't be changed by the called method. What if you want the method to return two or more values instead of just one? The best way to do that is to return one object that contains those values, and you'll learn how to do that in section 3.

# The basic syntax of the parameters in a parameter list

[ref] type variableName

# A method named CalculateFutureValue requires four parameters

```csharp
private void CalculateFutureValue(decimal monthlyInvestment,
    decimal monthlyInterestRate, int months, ref decimal futureValue)
{
    for (int i = 0; i < months; i++)
    {
        futureValue = (futureValue + monthlyInvestment)
        *(1 + monthlyInterestRate);
    }
}
```

# Three statements that work with the CalculateFutureValue method

```csharp
decimal futureValue = 0;
this.CalculateFutureValue(monthlyInvestment,
    monthlyInterestRate, months, ref futureValue);
txtFutureValue.Text = futureValue.ToString("c");
```

# Description

- When you call a method, each argument can be passed to the method by value or reference.
- If you pass an argument by value, the value of the variable in the calling method can't be changed by the called method. That's because the value is a copy.
- If you pass an argument by reference, the value of the variable in the calling method can be changed by the called method.
- To pass an argument by reference, you use the ref keyword as shown above.

Figure 6-5 When and how to pass arguments by reference and by value

# How to work with events and delegates

In chapter 3, you learned how to generate the event handler for a control by double-clicking in the Form Designer. Now, you'll learn how to create an event handler for any event. In addition, you'll learn more about how wiring works, and you'll learn how to handle more than one event with the event handler.

# How to generate an event handler for any event

Figure 6-6 shows how to generate an event handler for any event. To do that, you select the form or control in the Form Designer and click the Events button in the Properties window. When you do, a list of events for that form or control is displayed. In this figure, you can see a list of events for the first text box. Below the list of events, you can see a short description of the highlighted event.

To generate a handler for any of these events, you can double-click on the event in this list. Then, Visual Studio will generate the method declaration for the event handler along with a statement that wires the event to the event handler (as you'll see in the next figure). When you use this technique, Visual Studio will generate the name of the control and the name of the event. For example, if you double-click the event for the Monthly Investment text box, Visual Studio will generate an event handler with this name:

```sharp
txtMonthlyInvestment_Validating
```

If you want to generate an event handler with a name other than the default, you can do that by entering the name next to the event in the Properties window. Then, when you press the Enter key, Visual Studio will create an event handler with that name. In most cases, you'll use this technique only when you generate an event handler that will be used to handle more than one event. You'll learn more about that in figure 6-8.
