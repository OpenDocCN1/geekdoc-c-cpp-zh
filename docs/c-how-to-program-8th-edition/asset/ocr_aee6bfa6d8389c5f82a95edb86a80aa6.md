+   7. **Running the program again.** Breakpoints persist until the end of the debugging session in which they are set. So, the breakpoint you set in *Step 2* is still set. Type `run` to run the program and enter 13 at the prompt. As in *Step 3*, the program runs until the breakpoint at line 21 is reached, then the debugger pauses and waits for the next command (Fig. I.23).

```
```text
(gdb) run
Starting program: /home/nuke/App7/Fig1_03
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

Breakpoint 1, main () at Fig1_03.cpp:21
  21          account1.debit(withdrawalAmount); // try to subtract from account1
(gdb)
```
```

*Fig. I.23* | Restarting the program.

+   8. **Using the next command.** Type `next`. This command behaves like the step command, except when the next statement to execute contains a function call. In that case, the called function executes in its entirety and the program advances to the next executable line after the function call (Fig. I.24). In *Step 4*, the step command enters the called function. In this example, the next command executes Account member function debit, then the debugger pauses at line 24.

```
```text
(gdb) next
24          cout << "account1 balance: $" << account1.getBalance() << endl;
(gdb)
```
```

*Fig. I.24* | Using the next command to execute a function in its entirety.

+   9. **Using the quit command.** Use the quit command to end the debugging session (Fig. I.25). While the program is running, this command causes the program to immediately terminate rather than execute the remaining statements in main.

```
```text
(gdb) quit
The program is running.  Exit anyway? (y or n) y
$
```
```

*Fig. I.25* | Exiting the debugger using the quit command.

In this section, you used the debugger’s **step** and **finish** commands to debug functions called during your program’s execution. You saw how the next command can step over a function call. You also learned that the quit command ends a debugging session.