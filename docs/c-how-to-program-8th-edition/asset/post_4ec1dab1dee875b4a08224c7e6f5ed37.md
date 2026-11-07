
- 7. **Running the program again.** Breakpoints persist until the end of the debugging session in which they are set. So, the breakpoint you set in *Step 2* is still set. Type `run` to run the program and enter 13 at the prompt. As in *Step 3*, the program runs until the breakpoint at line 21 is reached, then the debugger pauses and waits for the next command (Fig. I.23).

```text
(gdb) run
Starting program: /home/nuke/App7/FigI_03
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

Breakpoint 1, main () at FigI_03.cpp:21
  21          account1.debit(withdrawalAmount); // try to subtract from account1
(gdb)
```

*Fig. I.23* | Restarting the program.

- 8. **Using the next command.** Type `next`. This command behaves like the step command, except when the next statement to execute contains a function call. In that case, the called function executes in its entirety and the program advances to the next executable line after the function call (Fig. I.24). In *Step 4*, the step command enters the called function. In this example, the next command executes Account member function debit, then the debugger pauses at line 24.

```text
(gdb) next
24          cout << "account1 balance: $" << account1.getBalance() << endl;
(gdb)
```

*Fig. I.24* | Using the next command to execute a function in its entirety.

- 9. **Using the quit command.** Use the quit command to end the debugging session (Fig. I.25). While the program is running, this command causes the program to immediately terminate rather than execute the remaining statements in main.

```text
(gdb) quit
The program is running.  Exit anyway? (y or n) y
$
```

*Fig. I.25* | Exiting the debugger using the quit command.

In this section, you used the debugger’s **step** and **finish** commands to debug functions called during your program’s execution. You saw how the next command can step over a function call. You also learned that the quit command ends a debugging session.

- 5. **Exiting the constructor.** Type `finish` to complete the constructor’s execution and return to main.

- 6. **Withdrawing money from the account.** Type `continue` to continue execution and enter a withdrawal value at the prompt. The program executes normally. Line 21 of Fig. I.3 calls Account member function debit to reduce the Account object’s balance by a specified amount. Line 32 of Fig. I.2 inside function debit changes the value of balance. The debugger notifies you of this change and enters break mode (Fig. I.29).

```text
(gdb) continue
Continuing.
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

Hardware watchpoint 2: account1.balance

Old value = 50
New value = 37
0x0804893b in Account::debit (this=0xbfcd6b90, amount=13) at Account.cpp:32
32        balance = balance - amount;
(gdb)
```

*Fig. I.29* | Entering break mode when a variable is changed.

- 7. **Continuing execution.** Type `continue`—the program will finish executing function main because the program does not attempt any additional changes to balance. The debugger removes the watch on account1’s balance data member because the account1 object goes out of scope when function main ends. Removing the watchpoint causes the debugger to enter break mode. Type `continue` again to finish execution of the program (Fig. I.30).

```text
(gdb) continue
Continuing.
account1 balance: $37

Watchpoint 2 deleted because the program has left the block in
which its expression is valid.
0xb7da0595 in exit () from /lib/tls/i686/cmov/libc.so.6
(gdb) continue
Continuing.

Program exited normally.
(gdb)
```

*Fig. I.30* | Continuing to the end of the program.

- 8. **Restarting the debugger and resetting the watch on the variable.** Type `run` to restart the debugger. Once again, set a watch on account1 data member balance by typing `watch account1.balance`. This watchpoint is labeled as watchpoint 3. Type `continue` to continue execution (Fig. I.31).

```text
(gdb) run
Starting program: /home/nuke/App3/FigI_03

Breakpoint 1, main () at FigI_03.cpp:10
10        Account account1(50 ); // create Account object
(gdb) watch account1.balance
Hardware watchpoint 3: account1.balance
(gdb) continue
Continuing.
Hardware watchpoint 3: account1.balance

Old value = 0
New value = 50
Account::Account (this=0xbfdb8eb90, initialBalance=50) at Account.cpp:18
18        if ( initialBalance < 0 )
(gdb)
```

**Fig. I.31** | Resetting the watch on a data member.

- 9. **Removing the watch on the data member.** Suppose you want to watch a data member for only part of a program’s execution. You can remove the debugger’s watch on variable balance by typing `delete 3` (Fig. I.32). Type `continue`—the program will finish executing without reentering break mode.

```text
(gdb) delete 3
(gdb) continue
Continuing.
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

account1 balance: $37

Program exited normally.
(gdb)
```

**Fig. I.32** | Removing a watch.

In this section, you used the watch command to enable the debugger to notify you when the value of a variable changes. You used the delete command to remove a watch on a data member before the end of the program.

## I.6 Wrap-Up

In this appendix, you learned how to insert and remove breakpoints in the debugger. Breakpoints allow you to pause program execution so you can examine variable values with the debugger’s `print` command, which can help you locate and fix logic errors. You used the `print` command to examine the value of an expression, and you used the `set` command to change the value of a variable. You also learned debugger commands (including the `step`, `finish` and `next` commands) that can be used to determine whether a function is executing correctly. You learned how to use the `watch` command to keep track of a data member throughout the scope of that data member. Finally, you learned how to use the `info break` command to list all the breakpoints and watchpoints set for a program and the `delete` command to remove individual breakpoints and watchpoints.

## Summary

### Section I.1 Introduction

- GNU includes software called a debugger, which allows you to monitor the execution of your programs to locate and remove logic errors.

### Section I.2 Breakpoints and the run, stop, continue and print Commands

- The GNU debugger works only with executable files that were compiled with the `-g` compiler option, which generates information that is used by the debugger to help you debug your programs.
- The `gdb` command will start the GNU debugger and enable you to use its features. The `run` command will run a program through the debugger.
- Breakpoints are markers that can be set at any executable line of code. When program execution reaches a breakpoint, execution pauses.
- The `break` command inserts a breakpoint at the line number specified after the command.
- When the program runs, it suspends execution at any line that contains a breakpoint and is said to be in break mode.
- The `continue` command causes the program to continue running until the next breakpoint is reached.
- The `print` command allows you to peek inside the computer at the value of one of your variables.
- When the `print` command is used, the result is stored in a convenience variable such as `$1`. Convenience variables are temporary variables that can be used in the debugging process to perform arithmetic and evaluate Boolean expressions.
- You can display a list of all of the breakpoints in the program by typing `info break`.
- To remove a breakpoint, type `delete`, followed by a space and the number of the breakpoint to remove.

### Section I.3 print and set Commands

- Use the `quit` command to end the debugging session.
- The `set` command allows you to assign new values to variables.

### Section I.4 Controlling Execution Using the step, finish and next Commands

- The `step` command executes the next statement in the program. If the next statement to execute is a function call, control transfers to the called function. The `step` command enables you to enter a function and study the individual statements of that function.
- The `finish` command executes the remaining statements in the function and returns control to the place where the function was called.
