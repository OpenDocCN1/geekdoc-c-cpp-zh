
![](img/bfd978e7e9b192bab46ec2a89e481263_1228_0.png)

**Fig. H.8** | *Quick Info box showing the value of a variable.*

- 6. *Setting a breakpoint at `main`’s closing brace.* Set a breakpoint at line 25 in the source code by clicking in the margin indicator bar to the left of line 25. This will prevent the program from closing immediately after displaying its result. When there are no more breakpoints at which to suspend execution, the program will execute to completion and the **Command Prompt** window will close. If you do not set this breakpoint, you won’t be able to view the program’s output before the console window closes.

- 7. *Continuing program execution.* Use the **Debug > Continue** command to execute the code up to the next breakpoint. The program displays the result of its calculation (Fig. H.9).

![](img/bfd978e7e9b192bab46ec2a89e481263_1228_1.png)

**Fig. H.9** | *Program output.*

- 8. *Removing a breakpoint.* Click the breakpoint in the margin indicator bar.

- 9. *Finishing program execution.* Select **Debug > Continue** to execute the program to completion.

In this section, you learned how to enable the debugger and set breakpoints so that you can examine the results of code while a program is running. You also learned how to continue execution after a program suspends execution at a breakpoint and how to remove breakpoints.

## H.3 Locals and Watch Windows

In the preceding section, you learned that the *Quick Info* feature allows you to examine a variable’s value. In this section, you’ll learn to use the *Locals* window to assign new values to variables while your program is running. You’ll also use the *Watch* window to examine the value of more complex expressions.

- 1. ***Inserting breakpoints.*** Clear the existing breakpoints. Then, set a breakpoint at line 21 in the source code by clicking the margin indicator bar to the left of line 21 (Fig. H.10). Set another breakpoint at line 24 by clicking in the margin indicator bar to the left of line 24.

![](img/bfd978e7e9b192bab46ec2a89e481263_1229_0.png)

**Fig. H.10** | Setting breakpoints at lines 21 and 24.

- 2. ***Starting debugging.*** Select **Debug > Start**. Type 13 at the **Enter withdrawal amount for account1:** prompt and press *Enter* so that your program reads the value you just entered. The program executes until the breakpoint at line 21.

- 3. ***Suspending program execution.*** The debugger enters break mode at line 21 (Fig. H.11). At this point, line 18 has input the withdrawalAmount that you entered (13), lines 19–20 have output that the program will attempt to withdraw money and line 21 is the next statement that will execute.

![](img/bfd978e7e9b192bab46ec2a89e481263_1229_1.png)

**Fig. H.11** | Program execution suspended when debugger reaches the breakpoint at line 21.

![](img/bfd978e7e9b192bab46ec2a89e481263_1231_0.png)

Value of account1’s balance data member displayed in red

**Fig. H.14** | Displaying the value of local variables.

valuable for experimenting with different values and for locating logic errors. In the Locals window, expand the account node and double-click the Value field in the balance row to select the value 37. Type 33, then press Enter. The debugger changes the value of balance and displays its new value in red (Fig. H.15).

![](img/bfd978e7e9b192bab46ec2a89e481263_1231_1.png)

Value modified in the Locals window

**Fig. H.15** | Modifying the value of a variable.

- 8. **Setting a breakpoint at main’s closing brace.** Set a breakpoint at line 25 in the source code to prevent the program from closing immediately after displaying its result. If you do not set this breakpoint, you won’t be able to view the program’s output before the console window closes.

- 9. **Viewing the program result.** Select **Debug > Continue** to continue program execution. Function main executes until the return statement in line 29 and displays the result. Notice that the result is $33 (Fig. H.16). This shows that Step 7 changed the value of balance from the calculated value (37) to 33.

![](img/bfd978e7e9b192bab46ec2a89e481263_1231_2.png)

**Fig. H.16** | Output displayed after modifying the account1 variable.

- 10. **Stopping the debugging session.** Select **Debug > Stop Debugging**. This will close the Command Prompt window. Remove all remaining breakpoints.

In this section, you learned how to use the debugger’s Watch and Locals windows to evaluate arithmetic and Boolean expressions. You also learned how to modify the value of a variable during your program’s execution.

## H.4 Controlling Execution Using the Step Into, Step Over, Step Out and Continue Commands

Sometimes executing a program line by line can help you verify that a function’s code executes correctly, and can help you find and fix logic errors. The commands you learn in this section allow you to execute a function line by line, execute all the statements of a function at once or execute only the remaining statements of a function (if you’ve already executed some statements within the function).

- 1. **Setting a breakpoint.** Set a breakpoint at line 21 by clicking in the margin indicator bar to the left of the line.

- 2. **Starting the debugger.** Select **Debug > Start**. Enter the value 13 at the **Enter withdrawal amount for account1:** prompt. Execution will halt when the program reaches the breakpoint at line 21.

- 3. **Using the Step Into command.** The **Step Into** command executes the next statement in the program (line 21), then immediately halts. If that statement is a function call (as is the case here), control transfers into the called function. This enables you to execute each statement inside the function individually to confirm the function’s execution. Select **Debug > Step Into** to enter the debit function. Then, select **Debug > Step Into** again so the yellow arrow is positioned at line 31 of Account.cpp, as shown in Fig. H.17.

![](img/bfd978e7e9b192bab46ec2a89e481263_1232_0.png)

**Fig. H.17** | Stepping into the debit function.

- 4. **Using the Step Over command.** Select **Debug > Step Over** to execute the current statement (line 31 in Fig. H.17) and transfer control to line 32 (Fig. H.18). The **Step Over** command behaves like the **Step Into** command when the next statement to execute does not contain a function call. You’ll see how the **Step Over** command differs from the **Step Into** command in *Step 10*.

- 5. **Using the Step Out command.** Select **Debug > Step Out** to execute the remaining statements in the function and return control to the next executable statement (line 28 in Fig. H.3). Often, in lengthy functions, you’ll want to look at a few key lines of code, then continue debugging the caller’s code. The **Step Out** command enables you to continue program execution in the caller without having to step through the entire called function line by line.

- 11. **Stopping the debugger.** Select **Debug > Stop Debugging**. This will close the Command Prompt window. Remove all remaining breakpoints.

In this section, you learned how to use the debugger’s **Step Into** command to debug functions called during your program’s execution. You saw how the **Step Over** command can be used to step over a function call. You used the **Step Out** command to continue execution until the end of the current function. You also learned that the **Continue** command continues execution until another breakpoint is found or the program exits.

## H.5 Autos Window

The **Autos window** displays the variables used in the previous statement executed (including the return value of a function, if there is one) and the variables in the next statement to execute.

- 1. **Setting breakpoints.** Set breakpoints at lines 10 and 18 in main by clicking in the margin indicator bar.

- 2. **Using the Autos window.** Start the debugger by selecting **Debug > Start**. When the debugger enters break mode at line 10, open the Autos window (Fig. H.20). Since we are just beginning the program’s execution, the Autos window lists only the variables in the next statement that will execute—in this case, the account1 object, its value and its type. Viewing the values stored in an object lets you verify that your program is manipulating these variables correctly. Notice that account1 contains a large negative value. This value, which may be different each time the program executes, is account1’s uninitialized value. This unpredictable (and often undesirable) value demonstrates why it is important to initialize all C++ variables before they are used.

![](img/bfd978e7e9b192bab46ec2a89e481263_1234_0.png)

**Fig. H.20** | Autos window displaying the state of account1 object.

- 3. **Using the Step Over command.** Select **Debug > Step Over** to execute line 10. The Autos window updates the value of account1’s balance data member (Fig. H.21) after it is initialized. The value of balance is displayed in red to indicate that it just changed.

![](img/bfd978e7e9b192bab46ec2a89e481263_1234_1.png)

**Fig. H.21** | Autos window displaying the state of account1 object after initialization.
