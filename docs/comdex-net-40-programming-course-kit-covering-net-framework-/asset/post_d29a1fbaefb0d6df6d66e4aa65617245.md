
### Listing 1.1: Writing the If...Else Statement

```vb
Module Module1
    Sub Main()
        Dim Number As Integer
        Console.Write("Enter the Number")
        Number = Int32.Parse(Console.ReadLine())
        If Number < 10 Then
            Console.WriteLine("Number is less than 10")
        ElseIf Number < 100 Then
            Console.WriteLine("Number is less than 100")
        Else
            Console.WriteLine("An invalid number entered")
        End If
        Console.ReadLine()
    End Sub
End Module
```

In Listing 1.1, a variable of the Integer type named Number is declared. After that, the user is prompted to enter a number, which is stored in the Number variable. The If statement is used to check the condition whether the value of the Number variable is less than 10. If the entered value is less than 10, the message, Number is less than 10, is displayed. The ElseIf statement is used to check another condition to determine whether the number is less than 100. If it is, the message, Number is less than 100, is displayed. If the preceding conditions are not true and you enter a value that is either equal to 100 or is more than 100, for example, 101, then the statement in the Else block is executed and the message, An invalid number entered, is displayed.

- 8. Run the application by pressing the F5 key on the keyboard. The output is displayed (Fig.VB-1.1).
- 9. Enter the value 9 and press the ENTER key on the keyboard. This displays the output, (Fig.VB-1.2).

![](img/9862a98a1a2d3bb14334137965a1ec60_76_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_76_1.png)

Note that in Fig.VB-1.2, a message corresponding to the conditions specified in Listing 1.1, is displayed on the screen.

## Using the Select...Case Statement

The Select...Case statement compares the value of an expression with different values of other expressions in the given Case statements. If the Case statement matches the specified expression, the program control is transferred to that statement and as a result, the statements inside that Case statement are executed. You can have multiple Case statements in a Select statement. The syntax for a Select...Case statement is as follows:

```text
Select [ Case ] expression
    [ Case expressionlist
        [ statements ] ]
    [ Case Else
        [ elsestatements ] ]
End Select
```

In the preceding syntax, the expression is compared with a list of expressions in each Case statement one by one and the set of statements corresponding to the Case statement whose expression list matches the test expression is executed. In case no match is found for the test expression, the set of statements corresponding to the Case Else statement is executed.

Perform the following steps to use a Select...Case statement in a Console application:

- 1. *Start* Visual Studio 2010.
- 2. Select File➤New➤Project from the menu bar. The New Project dialog box opens.
- 3. Select Visual Basic➤Windows from the Installed Templates section in the left pane of the New Project dialog box.
- 4. Select Console Application from the middle pane to create a Console application.
- 5. Enter the name, SELECTCASE, in the Name text box and an appropriate location for the application in the Location combo box.
- 6. Click the OK button to close the New Project dialog box. The SELECTCASE application (also available on the CD) is created.
- 7. Add the highlighted code snippet, shown in Listing 1.2, to the Module1.vb file.

### Listing 1.2: Writing the Select...Case Statement

```vb
Module Module1
    Sub Main()
        Dim Number As Integer
        Console.Write("Enter the Number:")
        Number = Int32.Parse(Console.ReadLine())
        Select Case Number
            Case 1 To 4
                Console.WriteLine("The number is between 1 and 4")
            Case 5, 6
                Console.WriteLine("The number is 5 or 6")
            Case 7 To 10
                Console.WriteLine("The number is between 7 and 10")
            Case Else
                Console.WriteLine("The number is not between 1 and 10")
        End Select
        Console.ReadLine()
    End Sub
End Module
```

In Listing 1.2, a variable of the Integer type, called Number, is declared. After that, the user is prompted to enter a number, which is stored in the Number variable. The Select...Case statement is used to print different messages on the screen depending on the value stored in the Number variable. You compare the value stored in the Number variable with the value contained in the Case statement. If the value stored in the Number variable falls between 1 and 4, the statement, Case 1 To 4, evaluates to True, and as a result the message, The number is between 1 and 4, is displayed on the screen. If the Number variable contains a value between 5 and 6, the statement, Case 5, 6, evaluates to True, and the message, The number is 5 or 6, is displayed on the screen. Similarly, if the Number variable contains the value between 7 and 10, the message, The number is between 7 and 10, is displayed on the screen. If the preceding conditions are not true, and you enter a value that is more than 10, the statement in the Else block is executed and the message, The number is not between 1 and 10, is displayed on the screen.

- 8. Run the application by pressing the F5 key on the keyboard. The output of the application is displayed, (Fig.VB-1.3).
- 9. Enter the value 3 and press the ENTER key on the keyboard. The output is displayed, (Fig.VB-1.4).

![](img/9862a98a1a2d3bb14334137965a1ec60_77_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_77_1.png)

Fig.VB-1.3

Fig.VB-1.4

Note that in Fig.VB-1.4, a message corresponding to the conditions specified in Listing 1.2, is displayed on the screen.

Let's now discuss the different iteration statements available in Visual Basic 2010.

## Working with Iteration Statements

An iteration statement executes a statement or a set of statements repeatedly. Suppose you want to execute a set of statements 50 times in your program. However, writing the same code 50 times is a tedious and time consuming task. Instead of writing the code 50 times, you can place the code inside a loop and specify a condition that the loop has to execute 50 times. This saves the complexity and time involved in coding. Visual Basic 2010 supports four types of iteration statements:

- The For...Next statement
- The For...Each statement
- The While...End While statement
- The Do...Loop statement

Let’s now discuss these statements, one by one.

### Using the For...Next Statement

The For...Next statement is used when you want to execute a group of statements repeatedly for a specified number of times. The For statement needs a loop index, which contains the lower value, for its execution and counts the number of loop iterations. The syntax of the For...Next statement is as follows:

```vb
For counter [ as datatype ] = start To end [ Step step ]
    [ statements ]
    [ Exit For ]
    [ statements ]
Next [ counter ]
```

In the preceding syntax, when the statement starts, counter is set to start. Each time during the looping cycle, counter is incremented by one. You can increment the counter more than 1 by specifying a positive value in the For statement. In case you do not specify a value, a default value, 1, is set. When the value of counter equals to end, the loop ends. The term, datatype, represents the data type of counter. You can also terminate a For...Next statement any time with an Exit For keyword.

Perform the following steps to use a For...Next statement in a Console application:

- 1. *Start* Visual Studio 2010.
- 2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box appears.
- 3. *Select* **Visual Basic→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Console Application** from the middle pane to create a Console application.
- 5. *Enter* the name, FORNEXT, in the Name text box and an appropriate location for the application in the Location combo box.
- 6. *Click* the **OK** button to close the **New Project** dialog box. The **FORNEXT** application (also available on the CD) is created.
- 7. *Add* the highlighted code snippet, shown in Listing 1.3, to the Module1.vb file:

### Listing 1.3: Writing the For...Next Statement

```vb
Module Module1
    Sub Main()
        Dim Number As Integer
        Console.WriteLine("Iteration using For...Next Statement:")
        For Number = 1 To 3
            Console.WriteLine(Number)
        Next
        Console.ReadLine()
    End Sub
End Module
```

In Listing 1.3, a variable, Number, of the Integer type is declared. In the For...Next statement, the Number variable is initially assigned a value 1, and 3 represents the maximum value of the variable. The Next statement increments the value of the Number variable by 1.
