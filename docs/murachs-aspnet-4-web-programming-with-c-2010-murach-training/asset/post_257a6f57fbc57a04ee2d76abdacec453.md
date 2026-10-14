
## Common ASP.NET page events

| Event | Method name | Occurs when... |
| :--- | :--- | :--- |
| **Init** | Page_Init | A page is requested from the server. This event is raised before the view state of the page controls has been restored. |
| **Load** | Page_Load | A page is requested from the server, after all controls have been initialized and view state has been restored. This is the event you typically use to perform initialization operations such as retrieving data and initializing form controls. |
| **PreRender** | Page_PreRender | All the control events for the page have been processed but before the HTML that will be sent back to the browser is generated. |

## Common ASP.NET control events

| Event | Occurs when... |
| :--- | :--- |
| **Click** | The user clicks a button, link button, or image button control. |
| **TextChanged** | The user changes the value in a text box. |
| **CheckedChanged** | The user selects a radio button in a group of radio buttons or selects or unselects a check box. |
| **SelectedIndexChanged** | The user selects an item from a list box, a drop-down list, a check box list, or a radio button list. |

## Code for the Click event of the btnClear button

```
protected void btnClear_Click(object sender, EventArgs e)
{
    ddlMonthlyInvestment.SelectedIndex = 0;
    txtInterestRate.Text = "";
    txtYears.Text = "";
    lblFutureValue.Text = "";
}
```

## Description

- All of the events associated with an ASP.NET web page and its server controls are executed on the server. Because of that, the page must be posted back to the server to process any event for which you've coded an event handler.
- When a page is posted back to the server, the **Init** and **Load** events are always raised so any event handlers for those events are run first. Next, the event handlers for any control events that were raised are executed in the order they were raised. When these event handlers finish, the **PreRender** event is raised and any event handler for that event is run.

## The C# code for the Future Value form

Figure 2-19 presents the complete C# code for the code-behind file of the Future Value form. It consists of three event handlers that handle the Load event for the page and the Click events of the Calculate and Clear buttons. This code also includes a method named CalculateFutureValue that is called by the event handler for the Click event of the Calculate button.

In this code, I’ve highlighted the two page properties that are commonly tested in the code for web forms. The first one is the IsPostBack property that’s used in the Page_Load method. If it is True, it means that the page is being posted back from the user. If it is False, it means that the page is being requested by the user for the first time.

As a result, the statements within the if statement in the Page_Load method are only executed if the page is being requested for the first time. In that case, the values 50 through 500 are added to the drop-down list. For all subsequent requests by that user, the IsPostBack property will be True so the values aren’t added to the drop-down list.

The other page property that’s commonly tested is the IsValid property. It’s useful when the user’s browser doesn’t support the client-side scripts for the validation controls. In that case, the application has to rely on the validation that’s always done on the server. Then, if IsValid is True, it means that all of the input data is valid. But if IsValid is False, it means that one or more controls contain invalid input data so the processing shouldn’t be done.

In the btnCalculate_Click method, you can see how the IsValid test is used. If it isn’t True, the processing isn’t done. But otherwise, this method uses the SelectedValue property of the drop-down list to get the value of the selected item, which represents the investment amount. Then, it gets the years and interest rate values from the text boxes and converts them to monthly units. Last, it calls the CalculateFutureValue method to calculate the future value, uses the ToString method convert the future value to a string with currency format, and puts the formatted value in the label of the form. When this method ends, the web form is sent back to the user’s browser.

With the exception of the IsPostBack and IsValid properties, this is all standard C# code so you shouldn’t have any trouble following it. But if you do, you can quickly upgrade your C# skills by getting our latest C# book.

## The C# code for the Future Value form

```
using System;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
if (!IsPostBack)
for (int i = 50; i <= 500; i += 50)
ddlMonthlyInvestment.Items.Add(i.ToString());
}
protected void btnCalculate_Click(object sender, EventArgs e)
{
if (IsValid)
{
int monthlyInvestment =
Convert.ToInt32(ddlMonthlyInvestment.SelectedValue);
decimal yearlyInterestRate =
Convert.ToDecimal(txtInterestRate.Text);
int years =
Convert.ToInt32(txtYears.Text);
int months = years * 12;
decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;
decimal futureValue =
this.CalculateFutureValue(monthlyInvestment,
monthlyInterestRate, months);
lblFutureValue.Text = futureValue.ToString("c");
}
}
protected decimal CalculateFutureValue(int monthlyInvestment,
decimal monthlyInterestRate, int months)
{
decimal futureValue = 0;
for (int i = 0; i < months; i++)
{
futureValue = (futureValue + monthlyInvestment)
* (1 + monthlyInterestRate);
}
return futureValue;
}
protected void btnClear_Click(object sender, EventArgs e)
{
ddlMonthlyInvestment.SelectedIndex = 0;
txtInterestRate.Text = "";
txtYears.Text = "";
lblFutureValue.Text = "";
}
}
```

![](img/c024ccf88e28c30c07dd410d4342288f_88_0.png)

## How to test a web application

After you design the forms and develop the code for a web application, you need to test it to be sure it works properly. Then, if you discover any errors in the application, you can debug it, correct the errors, and test it again.

In chapter 4, you'll learn all the skills you need to test and debug a web application. For now, I just want to show you how to run a web site with the built-in development server so you can test any applications that you develop for this chapter. Then, I'll show you the HTML code that's sent to the browser so you can see how that works.

## How to run a web site with the built-in development server

When you run a file-system web site by using one of the techniques in figure 2-20, Visual Studio compiles the application. If the application compiles without errors, Visual Studio automatically launches the built-in ASP.NET Development Server and displays the starting page of the web site in your default browser. Then, you can test the application to make sure that it works the way you want it to.

However, if any errors are detected as part of the compilation, Visual Studio opens the Error List window and displays the errors. These can consist of errors that have to be corrected as well as warning messages. In this figure, three errors and one warning are displayed in the Error List window.

To fix an error, you can double-click on it in the Error List window. This moves the cursor to the line of code that caused the error in the Code Editor. By moving from the Error List window to the Code Editor for all of the messages, you should be able to find the coding problems and fix them.

As you're testing an application with the development server, exceptions may occur. If an exception isn't handled by the application, ASP.NET switches to the Code Editor window and highlights the statement that caused the exception. In this case, you can end the application by clicking on the Stop Debugging button in the Debug toolbar or using the Debug➡Stop Debugging command. Then, you can fix the problem and test again.

In chapter 4, you'll learn all of the debugging skills that you'll need for more complex applications. For simple applications, though, you should be able to get by with just the skills you have right now.
