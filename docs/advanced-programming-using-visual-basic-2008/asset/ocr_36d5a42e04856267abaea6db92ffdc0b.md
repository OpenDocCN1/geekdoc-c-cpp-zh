3. Use the Autos window, which "automatically" displays all variables and control contents that are referenced in the current statement and three statements on either side of the current one. Note that the Autos window is not available in the Express Edition.

```
' Add to the correct total.
If BlueRadioButton.Checked Then
    BlueTotalDecimal += QuantityDecimal
ElseIf RedRadioButton.Checked Then
    RedTotalDecimal += QuantityDecimal
ElseIf WhiteRadioButton.Checked Then
    WhiteTotalDecimal += 1
End If
```

![](bbox=[0.06, 0.43, 0.97, 0.65])

# Single-Step through Code

The best way to debug a project is to thoroughly understand what the project is doing every step of the way. Use the Visual Studio stepping tools to trace program execution line by line and see the progression of the program as it executes through your code.

You step through code at break time. Set a breakpoint or choose one of the stepping commands at design time; the program will begin running and immediately transfer to break time.

The three stepping commands are Step Into, Step Over, and Step Out. These commands force the project to execute a single line at a time and to display the Editor window with the current statement highlighted. As you execute the project, by pressing a button, for example, the Click event occurs. Execution transfers to the Click event handler, the Editor window for that procedure appears on the screen, and you can follow line-by-line execution.