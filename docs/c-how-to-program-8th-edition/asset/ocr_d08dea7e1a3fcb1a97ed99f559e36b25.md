# H.4 Controlling Execution Using the Step Into, Step Over, Step Out and Continue Commands

Sometimes executing a program line by line can help you verify that a function’s code executes correctly, and can help you find and fix logic errors. The commands you learn in this section allow you to execute a function line by line, execute all the statements of a function at once or execute only the remaining statements of a function (if you’ve already executed some statements within the function).

+   1. **Setting a breakpoint.** Set a breakpoint at line 21 by clicking in the margin indicator bar to the left of the line.

+   2. **Starting the debugger.** Select **Debug > Start**. Enter the value 13 at the **Enter withdrawal amount for account1:** prompt. Execution will halt when the program reaches the breakpoint at line 21.

+   3. **Using the Step Into command.** The **Step Into** command executes the next statement in the program (line 21), then immediately halts. If that statement is a function call (as is the case here), control transfers into the called function. This enables you to execute each statement inside the function individually to confirm the function’s execution. Select **Debug > Step Into** to enter the debit function. Then, Select **Debug > Step Into** again so the yellow arrow is positioned at line 31 of Account.cpp, as shown in Fig. H.17.

![](bbox=[0.269, 0.513, 0.726, 0.694])

**Fig. H.17** | Stepping into the debit function.

+   4. **Using the Step Over command.** Select **Debug > Step Over** to execute the current statement (line 31 in Fig. H.17) and transfer control to line 32 (Fig. H.18). The **Step Over** command behaves like the **Step Into** command when the next statement to execute does not contain a function call. You’ll see how the **Step Over** command differs from the **Step Into** command in *Step 10*.

+   5. **Using the Step Out command.** Select **Debug > Step Out** to execute the remaining statements in the function and return control to the next executable statement (line 28 in Fig. H.3). Often, in lengthy functions, you’ll want to look at a few key lines of code, then continue debugging the caller’s code. The **Step Out** command enables you to continue program execution in the caller without having to step through the entire called function line by line.