# H.4 Controlling Execution Using the **step**, **finish** and **next** Commands

Sometimes you’ll need to execute a program line by line to find and fix errors. Walking through a portion of your program this way can help you verify that a function’s code executes correctly. The commands in this section allow you to execute a function line by line, execute all the statements of a function at once or execute only the remaining statements of a function (if you have already executed some statements within the function).

+   1. **Starting the debugger.** Start the debugger by typing `gdb fig1_03`.
+   
+   2. **Setting a breakpoint.** Type `break 25` to set a breakpoint at line 25.
+   
+   3. **Running the program.** Run the program by typing `run`, then enter `13` at the prompt. After the program displays its two output messages, the debugger indicates that the breakpoint has been reached and displays the code at line 25. The debugger then pauses and waits for the next command to be entered.
+   
+   4. **Using the step command.** The **step command** executes the next statement in the program. If the next statement to execute is a function call, control transfers to the called function. The step command enables you to enter a function and study its individual statements. For instance, you can use the print and set commands to view and modify the variables within the function. Type `step` to enter the debit member function of class Account (Fig. H.2). The debugger indicates that the step has been completed and displays the next executable statement (Fig. H.21)—in this case, line 33 of class Account (Fig. H.2).
+   
+   5. **Using the finish command.** After you have stepped into the debit member function, type **finish**. This command executes the remaining statements in the function and returns control to the place where the function was called. The finish command executes the remaining statements in member function debit, then pauses at line 28 in `main` (Fig. H.22). In lengthy functions, you may want to look at a few key lines of code, and then continue debugging the caller’s code. The finish command is useful for situations in which you do not want to step through the remainder of a function line by line.
+   
+   6. **Using the continue command to continue execution.** Enter the `continue` command to continue execution until the program terminates.
+   
+   7. **Running the program again.** Breakpoints persist until the end of the debugging session in which they are set. So, the breakpoint you set in Step 2 is still set. Type `run` to run the program and enter `13` at the prompt. As in Step 3, the program runs until the breakpoint at line 25 is reached, then the debugger pauses and waits for the next command (Fig. H.23).

```
```text
(gdb) step
Account::debit (this=0xbff81700, amount=13) at Account.cpp:33
33      if ( amount <= balance ) // debit amount does not exceed balance
(gdb)
```
```

![](bbox=[0.142, 0.83, 0.856, 0.949])