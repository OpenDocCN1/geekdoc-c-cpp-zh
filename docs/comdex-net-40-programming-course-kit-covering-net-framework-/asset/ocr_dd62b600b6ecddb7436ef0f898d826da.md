Now, when the value of the Counter variable becomes 10, the condition evaluates to **False** and the Control exits the While statement.

+   8. *Run* the application by pressing the F5 key on the keyboard. The output of the application is displayed, as shown in Fig.VB-1.7:

![](bbox=[0.375, 0.203, 0.648, 0.298])

Fig.VB-1.7

In Fig.VB-1.7, the **While...End While** statement displays the values from 1 to 9 on the screen.

# Using the Do...Loop Statement

Similar to other iteration statements, the **Do...Loop** statement is also used to execute a group of statements repeatedly. You need to use either the **While** keyword or the **Until** keyword with the **Do...Loop** statement. When you use the **While** keyword, the **Do...Loop** statement executes a group of statements repeatedly as long as a given condition is **True**. On the other hand, when you use the **Until** keyword, the **Do...Loop** statement executes a group of statements until a given condition evaluates to **True**. The syntax of the **Do...Loop** statement is as follows:

```
```text
Do { while | until } condition
    [ statements ]
[ Exit Do ]
    [ statements ]
Loop
```
```

In the preceding syntax, the **Do...Loop** statement keeps executing the set of statements till the given condition is **True** or until the given condition evaluates to **True**.

Perform the following steps to use a **Do...Loop** statement in a Console application:

+   1. *Start* Visual Studio 2010.
+   2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box opens.
+   3. *Select* **Visual Basic→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
+   4. *Select* **Console Application** from the middle pane to create a Console application.
+   5. *Enter* the name, **DOLOOP**, in the **Name** text box and an appropriate location for the application in the **Location** combo box.
+   6. *Click* the **OK** button to close the **New Project** dialog box. The **DOLOOP** application (also available on the CD) is created.
+   7. *Add* the highlighted code snippet, shown in Listing 1.6, to the **Module1.vb** file:

# Listing 1.6: Writing the Do...Loop Statement

```
```vb
Module Module1
    Sub Main()
        Dim Number As Integer = 10
        Console.WriteLine("Iteration using Do...Loop Statement:")
        Do While Number < 20
            Console.WriteLine(Number)
            Number = Number + 1
        Loop
        Console.ReadLine()
    End Sub
End Module
```
```