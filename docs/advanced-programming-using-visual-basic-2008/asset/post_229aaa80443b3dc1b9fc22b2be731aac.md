
The string that you specify for TitlebarText will appear in the title bar of the message box. If you choose the first form of the Show method, without the TitlebarText, the title bar will appear empty.

You specify the buttons to display using the MessageBoxButtons constants from the MessageBox class. The choices are OK, OKCancel, RetryCancel, YesNo, YesNoCancel, and AbortRetryIgnore. The default for the Show method is OK, so unless you specify otherwise, you will get only the OK button. The Show method returns a DialogResult object that you can check to see which button the user clicked.

The easy way to select the icon to display is to select from IntelliSense, which pops up with the complete list. The actual appearance of the icons varies from one operating system to another. You can see a description of the icons in Help under the “MessageBoxIcon Enumeration” topic.

## Declaring an Object Variable for the Method Return

To capture the information about the outcome of the Show method, declare a variable to hold an instance of the DialogResult type.

```
Dim ResponseDialogResult As DialogResult

ResponseDialogResult = MessageBox.Show("Clear the current order figures?", _
"Clear Order", MessageBoxButtons.YesNo, MessageBoxIcon.Question)
```

The next step is to check the value of the return, comparing to the DialogResult constants, such as Yes, No, OK, Retry, Abort, and Cancel.

```
If ResponseDialogResult = Windows.Forms.DialogResult.Yes Then
    ' Code to clear the order.
End If
```

## Specifying a Default Button and Options

Two additional signatures for the MessageBox.Show method are

```
MessageBox.Show(TextMessage, TitlebarText, MessageBoxButtons, MessageBoxIcons, _
MessageBoxDefaultButton)
MessageBox.Show(TextMessage, TitlebarText, MessageBoxButtons, MessageBoxIcons, _
MessageBoxDefaultButton, MessageBoxOptions)
```

To make the second button (the No button) the default, use this statement:

```
ResponseDialogResult = MessageBox.Show("Clear the current order figures?", _
"Clear Order", MessageBoxButtons.YesNo, MessageBoxIcon.Question, _
MessageBoxDefaultButton.Button2)
```

You can make the message appear right-aligned in the message box by setting the MessageBoxOptions argument:

```
ResponseDialogResult = MessageBox.Show("Clear the current order figures?", _
"Clear Order", MessageBoxButtons.YesNo, MessageBoxIcon.Question, _
MessageBoxDefaultButton.Button2, MessageBoxOptions.RightAlign)
```

```
```vb
Private Sub PrintHeadings()

End Sub
```
```

Of course, you also can type the parameter list and the parentheses, if you wish.

```
```vb
Private Sub PrintHeadings(ByVal EndingDate As Date)
```
```

The parameter passed to the PrintHeadings sub procedure is a local variable inside the procedure. Call the PrintHeadings sub procedure in any of these ways:

```
```vb
PrintHeadings(Today)          ' Pass today's date.
PrintHeadings(MyFavoriteDate)
PrintHeadings(#2/2/2009#)
```
```

The PrintHeadings sub procedure uses the EndingDate parameter inside the procedure to reference the value passed for the parameter.

```
```vb
Private Sub PrintHeadings(ByVal EndingDate As Date)
    ' Print the date.

    Debug.WriteLine(EndingDate.ToShortDateString())
End Sub
```
```

## Writing Function Procedures

Functions return a value, so a function procedure must have a data type for the return value. The procedure header for a function looks like this:

```
```vb
{[Public|Private|Protected|Friend|Protected Friend] -
 Function FunctionName(ParameterList) As DataType
```
```

Somewhere inside the function procedure, before exiting, you must return a value. You can use the Return statement (the preferred technique) or assign a value to the function name (which was the technique used in VB 6). That value is returned to the calling statement.

```
```vb
Private Function AverageCost(ByVal FirstCostDecimal As Decimal, _
    ByVal SecondCostDecimal As Decimal, _
    ByVal ThirdCostDecimal As Decimal) As Decimal
    ' Calculate the average of three numbers.

    ' Preferred Return statement:
    Return (FirstCostDecimal + SecondCostDecimal + ThirdCostDecimal) / 3D

    ' Alternate Return statement:
    ' AverageCost = (FirstCostDecimal + SecondCostDecimal + ThirdCostDecimal) / 3D
End Function
```
```

## ByRef and ByVal

By default, arguments are passed ByVal (by value), which is a change from VB 6. ByVal forces VB to make a copy of the data and passes the copy. If the called

## Public, Private, Protected, Friend, or Protected Friend

Just as for variable declarations, you can declare sub procedures and functions to be Public, Private, Protected, Friend, or Protected Friend. The accessibility of procedures matches that of similarly declared variables. If you omit the accessibility keyword when writing a procedure, the default is Public.

## VB Functions and Methods

VB provides many intrinsic functions and methods for math operations, financial calculations, string manipulation, and date/time processing.

IntelliSense helps you type the arguments of functions and methods. When you type the parentheses, the arguments pop up, showing the correct order. The argument to enter is shown in bold. The order of the arguments is important because the function uses the values based on their position in the argument list. If the arguments are supplied in the incorrect order, the result is wrong. And if the data types are incorrect, a compile error occurs.

Methods may have overloaded parameter lists, which means that there is more than one way to call the method. When you enter the arguments, you must match one of the parameter lists exactly. Note that VB does allow implicit widening conversions, so a supplied argument may be of a wider data type than that specified in the parameter.

## Working with Dates

You can use the methods of the DateTime structure to retrieve the system date, break down a date into component parts, test whether the contents of a field are compatible with the Date data type, and convert other data types to a Date.

## The DateTime Structure

When you declare a variable of Date data type in VB, the .NET Common Language Runtime uses the DateTime structure, which has an extensive list of properties and methods. You can use the shared members of the DateTime structure (identified by a yellow “S” in the MSDN Help lists) without declaring an instance of Date or DateTime. For example, to use the Now property:

```
TodaysDate = Now
```

To use the nonshared members, you must reference an instance of a DateTime structure, such as a variable of Date type:

```
TimeLabel.Text = TodaysDate.ToShortTimeString()
```

Here is a partial list of some useful properties and methods of the Date-Time structure:

| Property or method | Purpose |
|---|---|
| Date | Date component. |
| Day | Integer day of month; 1–31. |
| DayOfWeek | Integer day; 0 = Sunday. |
| DayOfYear | Integer day; 1–366. |
| Hour | Integer hour; 0–23. |
| Minute | Integer minutes; 0–59. |
| Second | Integer seconds; 0–59. |
| Month | Integer month; 1 = January. |
| Now (shared) | Retrieve system date and time. |
| Today (shared) | Retrieve system date. |
| Year | Year component. |
| ToLongDateString | Date formatted as long date. |
| ToLongTimeString | Date formatted as long time. |
| ToShortDateString | Date formatted as short date. |
| ToShortTimeString | Date formatted as short time. |

## Retrieving the System Date and Time

You can retrieve the system date and time from your computer's clock using the Now property or the Today property. Now retrieves both the date and time; Today retrieves only the date.

```
Dim DateAndTimeDate As Date
DateAndTimeDate = Now

Dim TodaysDate As Date
TodaysDate = Today
```

To display the values formatted:

```
DateTimeLabel1.Text = DateAndTimeDate.ToLongDateString()
DateLabel1.Text = TodaysDate.ToShortDateString()
```

## Date Variables

The Date data type may hold values of many forms that represent a date. Examples could be May 26, 2009 or 5/26/09 or 5-26-2009. When you assign a literal value to a Date variable, enclose it in # signs:

```
Dim TheDate as Date = #5/26/2009#
```
