![](bbox=[0.225, 0.108, 0.777, 0.322])

Fig. F.13 | Reaching the breakpoint in the AccountTest application.

the individual statements of that method. For instance, you can use the print and set commands to view and modify the variables within the method. You'll now use the step command to enter the credit method of class Account (Fig. 3.13) by typing step (Fig. F.14). The debugger indicates that the step has been completed and displays the next executable statement—in this case, line 21 of class Account (Fig. 3.13).

![](bbox=[0.225, 0.515, 0.777, 0.61])

Fig. F.14 | Stepping into the credit method.

+   5. Using the step up command. After you've stepped into the credit method, type step up. This command executes the remaining statements in the method and returns control to the place where the method was called. The credit method contains only one statement to add the method's parameter amount to instance variable balance. The step up command executes this statement, then pauses before line 22 in AccountTest. Thus, the next action to occur will be to print the new account balance (Fig. F.15). In lengthy methods, you may want to look at a few key lines of code, then continue debugging the caller's code. The step up command is useful for situations in which you do not want to continue stepping through the entire method line by line.

+   6. Using the cont command to continue execution. Enter the cont command (Fig. F.16) to continue execution. The statement at lines 22–23 executes, displaying the new balance, then the application and the debugger terminate.

+   7. Restarting the debugger. Restart the debugger by typing jdb.