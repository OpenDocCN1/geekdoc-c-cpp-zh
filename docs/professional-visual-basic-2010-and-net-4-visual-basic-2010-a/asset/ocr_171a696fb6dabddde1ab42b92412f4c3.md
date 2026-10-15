argument passed in. Another common place to throw an exception is after a test on the arguments passed to a method or property, if it is discovered that the argument is not appropriate and processing cannot continue, such as when a negative number is passed in for a count that must be positive.

The next section of the chapter covers the keywords in detail and includes code samples of the keywords in action. All the code in this section is included in the code download for this chapter.

# The Try, Catch, and Finally Keywords

Here is an example showing some typical, simple structured exception-handling code in Visual Basic 2010. In this case, the most likely source of an error is the `iItems` argument. If it has a value of zero, then this would lead to dividing by zero, which would generate an exception.

First, create a Windows Forms Application in Visual Basic 2010 and place a button on the default `Form1` created in the project. In the button’s `Click` event, place the following two lines of code:

```
Dim sngAvg As Single
sngAvg = GetAverage(0, 100)
```

Code snippet from ExceptionHandlingSampleCodeForm

Then put the following function in the form’s code:

```
Private Function GetAverage(iItems As Integer, iTotal As Integer) as Single
    ' Code that might throw an exception is wrapped in a Try block
    Try
        Dim sngAverage As Single
        ' This will cause an exception to be thrown if iItems = 0
        sngAverage = CSng(iTotal \ iItems)
        ' This only executes if the line above generated no error
        MessageBox.Show("Calculation successful")
        Return sngAverage
    Catch excGeneric As Exception
        ' If the calculation failed, you get here
        MessageBox.Show("Calculation unsuccessful - exception caught")
        Return 0
    End Try
End Function
```

Code snippet from ExceptionHandlingSampleCodeForm

This code traps all the exceptions with a single generic exception type, and doesn’t include any `Finally` logic. Run the program and press the button. You will be able to follow the sequence better if you place a breakpoint at the top of the `GetAverage` function and step through the lines.

> A breakpoint is a marker in a line of code indicating that you wish execution of the program to be suspended when execution reaches that line. When a breakpoint is reached, you have the opportunity to examine values of variables or perform other actions that may help you diagnose a problem. A breakpoint is set in Visual Studio by positioning the cursor on a line of code and choosing the appropriate option. Depending on your settings, you probably also have a shortcut key to set a breakpoint. The most common key used for that purpose is F9. You can also set a breakpoint by clicking next to the desired line in the vertical gray bar on the left side of the Code Editor window.

Here is a more complex example that traps the divide-by-zero exception explicitly. This second version of the `GetAverage` function (notice that the name is `GetAverage2`) also includes a `Finally` block: