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

# Error Handling and Macro Debugging

Prior to Access 2007, if an error occurred in a macro, the macro stopped execution, and your user saw an ugly dialog box (shown in Figure 22.17) that didn’t really explain what was going on. If he was unfamiliar with Access, he quickly became disgruntled using the application. The lack of error handing in macros is one main reason many developers use VBA instead of macros to automate their applications.

A common error that’s easy to demonstrate is the divide-by-zero error. For the next example, mcrDivision (shown in Figure 22.18) contains two temporary variables—MyNum and MyDenom—set with the InputBox() function asking for a numerator and denominator. The MessageBox action shows the result—[TempVars]![MyNum] & " divided by " & [TempVars]![MyDenom]—in a message box, and the RemoveTempVar actions remove the variables from memory.