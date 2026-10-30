
Table 22.5 shows the conditions, actions, and action arguments for mcrReportMenuEnhanced (shown in Figure 22.16), which opens one of three reports.

## TABLE 22.5 mcrReportMenuEnhanced

| Condition | Action | Action Argument | Action Argument Setting |
|---|---|---|---|
|  | SetTempVar | Name | ReportName |
|  |  | Expression | [Forms]![frmReportMenuEnhanced]![cboReport] |
|  | SetTempVar | Name | ReportView |
|  |  | Expression | [Forms]![frmReportMenuEnhanced]![fraView] |
| [TempVars]![ReportView]=1 | OpenReport | Report Name | =[TempVars]![ReportName] |
|  |  | View | Print |
|  |  | Window Mode | Normal |
| [TempVars]![ReportView]=2 | OpenReport | Report Name | =[TempVars]![ReportName] |
|  |  | View | Print Preview |
|  |  | Window Mode | Normal |
|  | RemoveTempVar | Name | ReportName |
|  | RemoveTempVar | Name | ReportView |

The first two SetTempVar actions in mcrReportMenuEnhanced set the values of the temporary variables—ReportName and ReportView—from cboReport and fraView on frmReportMenuEnhanced. The OpenReport actions use the temporary variables in the Condition column and for the ReportName argument. When using temporary variables as a setting for an argument, you must use an equal (=) sign in front of the expression:

```
=[TempVars]![ReportName]
```

There are still two OpenReport actions in this macro. Certain arguments—such as View—don't allow the use of temporary variables in expressions. Because one of your variables is a setting for the report's view, you still have to use the Condition column to decide which view to open the report in.

The last two RemoveTempVar lines remove the temporary variables—ReportName and ReportView—from memory. Because these variables probably won't be used later on in the application, it's important to remove them.

You can use temporary variables to store values to use later on in the macro, or anywhere in the application. Just remember that you have only 255 temporary variables to use, so don't forget to clean up after yourself by removing them from memory once you're finished using them.

## FIGURE 22.16

mcrReportMenuEnhanced uses temporary variables to open the report in Print or Print Preview view.

![](img/1e45673ab6eca9d20e67635ff5b9b318_770_0.png)

## Using temporary variables in VBA

You may start out using macros to automate your application, but over time, you may begin using VBA code to automate and add functionality to other areas. What do you do with the temporary variables you've already implemented with macros? Well, you don't have to abandon them; instead, you can use them directly in your VBA code.

To access a temporary variable in VBA, use the same syntax used in macros:

```
X = [TempVars]![VariableName]
```

If you don't use spaces in your variable names, you can omit the brackets:

```
X = TempVars!VariableName
```

Use the previous syntax to assign a new value to an existing temporary variable. The only difference is to put the temporary variable on the left side of the equation:

```
TempVars!VariableName = NewValue
```

Use the TempVars object to create and remove temporary variables in VBA. The TempVars object contains three methods: Add, Remove, and RemoveAll. To create a new temporary variable and set its value, use the Add method of the TempVars object as follows:

```
TempVars.Add "VariableName", Value
```

Use the Remove method of the TempVars object to remove a single temporary variable from memory:

```
TempVars.Remove "VariableName"
```

> **TIP**
>
> When adding or removing temporary variables in VBA, remember to put the temporary variable’s name in quotation marks.

To remove all the temporary variables from memory, use the RemoveAll method of the TempVars object as follows:

```
TempVars.RemoveAll
```

Any VBA variables you create are available to use in your macros, and vice versa. Any variables you remove in VBA are no longer available to use in your macros, and vice versa. Using temporary variables, your macros and VBA code no longer have to be independent from each other.

## Error Handling and Macro Debugging

Prior to Access 2007, if an error occurred in a macro, the macro stopped execution, and your user saw an ugly dialog box (shown in Figure 22.17) that didn’t really explain what was going on. If he was unfamiliar with Access, he quickly became disgruntled using the application. The lack of error handling in macros is one main reason many developers use VBA instead of macros to automate their applications.

A common error that’s easy to demonstrate is the divide-by-zero error. For the next example, mcrDivision (shown in Figure 22.18) contains two temporary variables—MyNum and MyDenom—set with the InputBox() function asking for a numerator and denominator. The MessageBox action shows the result—[TempVars]![MyNum] & " divided by " & [TempVars]![MyDenom]—in a message box, and the RemoveTempVar actions remove the variables from memory.

## FIGURE 22.17

Errors in macros cause the macro to cease operation.

![](img/1e45673ab6eca9d20e67635ff5b9b318_772_0.png)

## FIGURE 22.18

mcrDivision divides the numerator by the denominator and generates an error when the denominator is zero.

![](img/1e45673ab6eca9d20e67635ff5b9b318_772_1.png)

Run the macro and enter 1 for the numerator and 2 for the denominator; the macro runs and displays a message box saying 1 divided by 2 is 0.5. Run the macro again and enter 0 in the denominator; a divide-by-zero error occurs, and the macro stops running.

Without error handling, the two RemoveTempVar actions won’t run and won’t remove the temporary variables from memory.

If an error occurs in another macro—such as a string of action queries—any queries after an error occurs won’t run. Adding error handling to your macros allows you to choose what to do when an error occurs while a macro’s running.

## The OnError action

The OnError action lets you decide what happens when an error occurs in your macro. This action has two arguments: Go to and Macro Name. The Go to argument has three settings, and the Macro Name argument is used only with one of these settings, described as follows:

- **Next:** This setting records the details of the error in the MacroError object but does not stop the macro. The macro continues with the next action.
- **Macro Name:** This setting stops the current macro and runs the macro in the Macro Name argument of the OnError action.
- **Fail:** This setting stops the current macro and displays an error message. This is the same as not having error handling in the macro.

The VBA equivalents of these settings are as follows:

```
On Error Resume Next          'Next
On Error GoTo LABELNAME       'Macro Name
On Error GoTo 0               'Fail
```

The simplest way to add error handling to a macro is to make OnError the first action and set the Go to argument to Next. This will cause your macro to run without stopping, but you won’t have any clue which actions ran and which ones didn’t.

Instead, create an error-handling structure. Table 22.6 shows the macro names, actions, and action arguments for mcrDivisionErrorHandling (shown in Figure 22.19).

## TABLE 22.6 mcrDivisionErrorHandling

| Submacro Name | Action | Action Argument | Action Argument Setting |
|---|---|---|---|
|  | OnError | Go to | Macro Name |
|  |  | Macro Name | ErrorHandler |
|  | SetTempVar | Name | MyNum |
|  |  | Expression | InputBox("Enter Numerator.") |
|  | SetTempVar | Name | MyDenom |
|  |  | Expression | InputBox("Enter Denominator.") |
|  | MessageBox | Message | = [TempVars]![MyNum] & " divided by " & [TempVars]![MyDenom] & " is " & [TempVars]![MyNum] / [TempVars]![MyDenom] |
|  |  | Beep | Yes |
|  |  | Type | Information |
|  |  | Title | Division Example |
|  | RunMacro | Macro Name | mcrDivisionErrorHandling.Cleanup |
| ErrorHandler | MessageBox | Message | = "The following error occurred: " & [MacroError].[Description] |
|  |  | Beep | Yes |
|  |  | Type | Warning |
|  |  | Title | ="Error Number: " & [MacroError].[Number] |
|  | ClearMacroError |  |  |
|  | RunMacro | Macro Name | mcrDivisionErrorHandling.Cleanup |
| Cleanup | RemoveTempVar | Name | MyNum |
|  | RemoveTempVar | Name | MyDenom |

The first OnError action in the macro lets Access know to move to the submacro ErrorHandler when an error occurs. If an error occurs (by entering 0 as the denominator), the macro stops and moves to the ErrorHandler submacro. The ErrorHandler submacro displays a message box—using the MacroError object (described in the next section) to display the error’s description in the Message and the error’s number in the Title, using the following expressions:

```
[MacroError].[Description]
[MacroError].[Number]
```

After the error handler’s message box, the ClearMacroError action clears the MacroError object. The RunMacro action moves execution to the Cleanup submacro. The Cleanup section of the macro removes the temporary variables.
