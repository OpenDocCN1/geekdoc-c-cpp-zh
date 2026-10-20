
## How to code generic methods for data validation

Since it’s common to check entries for valid data, it often makes sense to create generic methods like the ones shown in figure 7-9 for data validation. These methods perform the same types of validation described in the previous figure, but they work for any entry instead of a specific text box. That includes entries on non-Windows forms, since these methods don’t require the Windows.Forms namespace. In this chapter, of course, these methods are coded within a Windows form, so they could use this namespace. In a real-world application, though, methods like these would be coded in a separate class and stored in a class library. You’ll learn how to code classes like this in chapter 12, and you’ll how to create and use class libraries in chapter 16.

In this figure, the IsPresent() method checks that the user has entered a value. To do that, it accepts two parameters that contain the value to be validated and a name that describes the value. This method starts by setting a variable named msg to an empty string. Then, if the user hasn’t entered any characters into the text box, it adds a message to the msg variable that includes the name parameter. Finally, it returns the value of the msg variable.

The IsDecimal() method accepts the same parameters as the IsPresent() method, but it uses an if statement that calls the TryParse() method of the Decimal class to check if the value entered by the user is a decimal value. If it isn’t, the TryParse() method will return a false value and a message will be added to the msg variable. Then, the method returns the value of this variable.

Once you understand how the IsDecimal() method works, you can code methods for other numeric types. For example, you can code an IsInt32() method that uses the Int32.TryParse() method to check if the user has entered a valid int value.

The IsWithinRange() method accepts two additional parameters that contain the minimum and maximum values that can be entered into the text box. Before it checks the range, it calls the TryParse() method of the Decimal class to be sure the value is numeric. You’ll see why that’s necessary when you see the code that calls these methods in the next figure. If the value is numeric, the IsWithinRange() method uses an if statement to check if the decimal value is within the range specified by the min and max parameters. If not, this method adds a message to the msg variable and returns the value of this variable.

Since the IsWithinRange() method uses the decimal type, which is the widest (most accurate) numeric data type, this method works with all numeric types. That’s because all numeric types can be automatically cast to the decimal type. If, for example, you pass arguments of the int type to the min and max parameters, they will be cast to the decimal type.

### A method that checks for a required field

```
private string IsPresent(string value, string name)
{
    string msg = "";
    if (value == "")
    {
        msg += name + " is a required field.\n";
    }
    return msg;
}
```

### A method that checks for a valid numeric format

```
private string IsDecimal(string value, string name)
{
    string msg = "";
    if (!Decimal.TryParse(value, out _))
    {
        msg += name + " must be a valid decimal value.\n";
    }
    return msg;
}
```

### A method that checks for a valid numeric range

```
private string IsWithinRange(string value, string name, decimal min, decimal max)
{
    string msg = "";
    if (Decimal.TryParse(value, out decimal number))
    {
        if (number < min || number > max)
        {
            msg += name + " must be between " + min + " and " + max + ".\n";
        }
    }
    return msg;
}
```

### Description

- Since it’s common to need to check text boxes for valid data, it often makes sense to create generic methods like these for data validation.
- These methods can be used to validate entries on Windows and non-Windows forms, since they don’t require the Windows.Forms namespace. Then, you can code them in a separate class as shown in chapter 12, and you can store the class in a class library as shown in chapter 16.

## How to validate multiple entries

Figure 7-10 shows how to code a method named IsValidData() that validates multiple entries on a form. The method shown here validates the Monthly Investment and Interest Rate text boxes on the Future Value form using the IsDecimal() and IsWithinRange() methods you saw in figure 7-9. In addition, it uses the IsWithinRange() method and a method named IsInt32() to validate the Years text box. The IsInt32() method works similarly to the IsDecimal() method, but it checks for an integer value using the TryParse() method of the Int32 class. Because this method checks every entry on the form for validity, all the validation code is in one location, which makes the code easy to read and maintain.

This code starts by declaring two variables named success and errorMessage. The success variable is a Boolean that will be used to determine if the validation is successful. The errorMessage variable is a string that will store any error messages to be displayed.

Next, this method calls the IsDecimal() method and passes the Text and Tag properties of the Monthly Investment text box as arguments. For this to work, the Tag property must be set so it identifies the value that’s being validated. Then, the ToString() method is called to convert this property to a string, and this string is included in any error messages.

If the Text property doesn’t contain a decimal value, the error message that’s returned by the IsDecimal() method is appended to the errorMessage variable. Then, the IsValidData() method calls the IsWithinRange() method to make sure that the value is greater than or equal to 1 and less than or equal to 1000. Remember that the IsWithinRange() method starts by checking if the value is a valid decimal, and it doesn’t check the range if it isn’t. Although that means that the value is checked twice to be sure it’s a decimal, this prevents an exception from being thrown when the range is checked.

The IsValidData() method uses similar code to validate the Interest Rate and Years text boxes. Then, it checks the errorMessage variable to see if any of the validation methods returned an error. If they did, the success variable is set to false and a message box like the one at the top of this figure is displayed. This method ends by passing the success variable to the calling method.

### A dialog box that displays three error messages

![](img/844f608d10a44654833ea5efc8a2e7a7_238_0.png)

### Code that validates multiple entries

```
private bool IsValidData()
{
    bool success = true;
    string errorMessage = "";

    // Validate the Monthly Investment text box
    errorMessage += IsDecimal(txtMonthlyInvestment.Text,
                    txtMonthlyInvestment.Tag.ToString());
    errorMessage += IsWithinRange(txtMonthlyInvestment.Text,
                    txtMonthlyInvestment.Tag.ToString(),
                    1, 1000);

    // Validate the Yearly Interest Rate text box
    errorMessage += IsDecimal(txtInterestRate.Text,
                    txtInterestRate.Tag.ToString());
    errorMessage += IsWithinRange(txtInterestRate.Text,
                    txtInterestRate.Tag.ToString(), 1, 20);

    // Validate the Number of Years text box
    errorMessage += IsInt32(txtYears.Text, txtYears.Tag.ToString());
    errorMessage += IsWithinRange(txtYears.Text, txtYears.Tag.ToString(),
                    1, 40);

    if (errorMessage != "")
    {
        success = false;
        MessageBox.Show(errorMessage, "Entry Error");
    }
    return success;
}
```

### Description

- You can use the validation methods shown in the previous figures to validate multiple entries. Then, if any of the entries are invalid, you can display a dialog box that describes the errors.

## The Future Value application with data validation

In figure 7-7, you saw a version of the Future Value application that used structured exception handling to catch all exceptions that might be thrown. Now, you’ll see an improved version of this application that includes code that validates the user entries. This code prevents format and overflow exceptions from being thrown, and it provides more descriptive messages to the user.

### The dialog boxes

Figure 7-11 shows the Future Value application after the user has entered invalid data in all three fields. Then, it shows the dialog box that’s displayed to identify those errors. Here, you can see that the monthly investment is outside the valid range, the yearly interest rate is invalid because it includes a percent sign, and the number of years is invalid because the user didn’t enter a value. The last dialog box is displayed if an exception that hasn’t been anticipated is thrown. To test this dialog box, you can code a throw statement within the code for the Future Value application as shown in figure 7-6.

### The code

Figure 7-12 shows the code for this version of the Future Value application. To start, the btnCalculate_Click() method contains an exception handler that catches and handles any unanticipated exceptions. Within the try block, an if statement checks whether the IsValidData() method returns a true value. If it does, the future value is calculated and displayed. Otherwise, none of the statements within the if block are executed. However, the IsValidData() method will display a dialog box with appropriate messages. Because this method is identical to the one you saw in the previous figure, you shouldn’t have any trouble understanding how it works.

Each method in this application performs a specific task. For example, the btnCalculate_Click() method contains the code that gets the values from the form and displays values on the form. The IsValidData(), IsDecimal(), IsInt32(), and IsWithinRange() methods contain the code that validates the data that’s entered by the user. And the CalculateFutureValue() method contains the code that performs the calculation. This is a good design because it leads to code that’s reusable and easy to maintain.

However, this code could be more efficient. For example, if the user enters a valid decimal value in the Monthly Investment text box, the value is converted to a decimal three times: once by the IsDecimal() method, once by the IsWithinRange() method, and once by the btnCalculate_Click() method. For most applications, however, the benefits that result from being able to reuse and easily maintain this code far outweigh any performance issues.
