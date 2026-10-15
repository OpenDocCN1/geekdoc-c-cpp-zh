
```
(gdb) print withdrawalAmount
$2 = 13
(gdb) print account1
$3 = {balance = 50}
(gdb)
```

Fig. H.9 | Printing the values of variables.

around the object’s data members. In this case, there is a single data member—balance—which has a value of 50.

8. Using convenience variables. When you use print, the result is stored in a convenience variable such as $1. Convenience variables are temporary variables created by the debugger that are named using a dollar sign followed by an integer. Convenience variables can be used to perform arithmetic and evaluate boolean expressions. Type print $1. The debugger displays the value of $1 (Fig. H.10), which contains the value of withdrawalAmount. Note that printing the value of $1 creates a new convenience variable—$3.

9. Continuing program execution. Type continue to continue the program’s execution. The debugger encounters no additional breakpoints, so it continues executing and eventually terminates (Fig. H.11).

10. Removing a breakpoint. You can display a list of all of the breakpoints in the program by typing info break. To remove a breakpoint, type delete, followed by a space and the number of the breakpoint to remove. Remove the first breakpoint by typing delete 1. Remove the second breakpoint as well. Now type info break to list the remaining breakpoints in the program. The debugger should indicate that no breakpoints are set (Fig. H.12).

11. Executing the program without breakpoints. Type run to execute the program. Enter the value 13 at the prompt. Because you successfully removed the two breakpoints, the program’s output is displayed without the debugger entering break mode (Fig. H.13).

```
(gdb) print $1
$3 = 13
(gdb)
```

Fig. H.10 | Printing a convenience variable.

```
(gdb) continue
Continuing.
account1.balance: $37

Program exited normally.
(gdb)
```

Fig. H.11 | Finishing execution of the program.

```
(gdb) info break
Num Type           Disp Enb Address    What
1   breakpoint      keep y   0x080486f6 in main at FigJ_03.cpp:17
    breakpoint already hit 1 time
2   breakpoint      keep y   0x08048799 in main at FigJ_03.cpp:25
    breakpoint already hit 1 time
(gdb) delete 1
(gdb) delete 2
(gdb) info break
No breakpoints or watchpoints.
(gdb)
```

Fig. H.12 | Viewing and removing breakpoints.

```
(gdb) run
Starting program: /home/nuke/AppJ/FigJ_03
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

account1 balance: $37

Program exited normally.
(gdb)
```

Fig. H.13 | Program executing with no breakpoints set.

## 12. Using the quit command.

Use the quit command to end the debugging session (Fig. H.14). This command causes the debugger to terminate.

In this section, you used the gdb command to start the debugger and the run command to start debugging a program. You set a breakpoint at a particular line number in the main function. The break command can also be used to set a breakpoint at a line number in another file or at a particular function. Typing break, then the filename, a colon and the line number will set a breakpoint at a line in another file. Typing break, then a function name will cause the debugger to enter the break mode whenever that function is called.

Also in this section, you saw how the help list command will provide more information on the list command. If you have any questions about the debugger or any of its commands, type help or help followed by the command name for more information.

Finally, you examined variables with the print command and remove breakpoints with the delete command. You learned how to use the continue command to continue execution after a breakpoint is reached and the quit command to end the debugger.

```
(gdb) quit
$
```

Fig. H.14 | Exiting the debugger using the quit command.

## H.3 print and set Commands

In the preceding section, you learned how to use the debugger’s print command to examine the value of a variable during program execution. In this section, you’ll see how to use the print command to examine the value of more complex expressions. You’ll also learn the set command, which allows you to assign new values to variables. We assume you are working in the directory containing this appendix’s examples and have compiled for debugging with the -g compiler option.

- 1. *Starting debugging.* Type gdb figJ_03 to start the GNU debugger.
- 2. *Inserting a breakpoint.* Set a breakpoint at line 25 in the source code by typing break 25 (Fig. H.15).
- 3. *Running the program and reaching a breakpoint.* Type run to begin the debugging process (Fig. H.16). This will cause main to execute until the breakpoint at line 25 is reached. This suspends program execution and switches the program into break mode. The statement in line 25 is the next statement that will execute.
- 4. *Evaluating arithmetic and boolean expressions.* Recall from Section H.2 that once the debugger enters break mode, you can explore the values of the program’s variables using the print command. You can also use print to evaluate arithmetic and boolean expressions. Type print withdrawalAmount - 2. This expression returns the value 11 (Fig. H.17), but does not actually change the value of withdrawalAmount. Type print withdrawalAmount == 11. Expressions containing the == symbol return bool values. The value returned is false (Fig. H.17) because withdrawalAmount withdrawalAmount still contains 13.
- 5. *Modifying values.* You can change the values of variables during the program’s execution in the debugger. This can be valuable for experimenting with different

```
(gdb) break 25
Breakpoint 1 at 0x8048799: file FigJ_03.cpp, line 25.
(gdb)
```

Fig. H.15 | Setting a breakpoint in the program.

```
(gdb) run
Starting program: /home/nuke/AppJ/FigJ_03
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

Breakpoint 1, main () at FigJ_03.cpp:25
25          account1.debit( withdrawalAmount ); // try to subtract from
account1
(gdb)
```

Fig. H.16 | Running the program until the breakpoint at line 25 is reached.

```
(gdb) print withdrawalAmount - 2
$1 = 11
(gdb) print withdrawalAmount == 11
$2 = false
(gdb)
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_1005_0.png)

values and for locating logic errors. You can use the debugger’s set command to change a variable’s value. Type `set withdrawalAmount = 42` to change the value of withdrawalAmount, then type `print withdrawalAmount` to display its new value (Fig. H.18).

- 6. *Viewing the program result.* Type `continue` to continue program execution. Line 25 of Fig. H.3 executes, passing `withdrawalAmount` to Account member function `debit`. Function `main` then displays the new balance. Note that the result is $8 (Fig. H.19). This shows that the preceding step changed the value of `withdrawalAmount` from the value 13 that you input to 42.
- 7. *Using the quit command.* Use the `quit` command to end the debugging session (Fig. H.20). This command causes the debugger to terminate.

In this section, you used the debugger’s print command to evaluate arithmetic and boolean expressions. You also learned how to use the set command to modify the value of a variable during your program’s execution.

```
(gdb) set withdrawalAmount = 42
(gdb) print withdrawalAmount
$3 = 42
(gdb)
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_1005_1.png)

```
(gdb) continue
Continuing.
account1 balance: $8

Program exited normally.
(gdb)
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_1005_2.png)

```
(gdb) quit
$
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_1005_3.png)

## H.4 Controlling Execution Using the **step**, **finish** and **next** Commands

Sometimes you’ll need to execute a program line by line to find and fix errors. Walking through a portion of your program this way can help you verify that a function’s code executes correctly. The commands in this section allow you to execute a function line by line, execute all the statements of a function at once or execute only the remaining statements of a function (if you have already executed some statements within the function).

- 1. **Starting the debugger.** Start the debugger by typing `gdb fig1_03`.
- 2. **Setting a breakpoint.** Type `break 25` to set a breakpoint at line 25.
- 3. **Running the program.** Run the program by typing `run`, then enter `13` at the prompt. After the program displays its two output messages, the debugger indicates that the breakpoint has been reached and displays the code at line 25. The debugger then pauses and waits for the next command to be entered.
- 4. **Using the step command.** The **step command** executes the next statement in the program. If the next statement to execute is a function call, control transfers to the called function. The step command enables you to enter a function and study its individual statements. For instance, you can use the print and set commands to view and modify the variables within the function. Type `step` to enter the debit member function of class Account (Fig. H.2). The debugger indicates that the step has been completed and displays the next executable statement (Fig. H.21)—in this case, line 33 of class Account (Fig. H.2).
- 5. **Using the finish command.** After you have stepped into the debit member function, type **finish**. This command executes the remaining statements in the function and returns control to the place where the function was called. The finish command executes the remaining statements in member function debit, then pauses at line 28 in `main` (Fig. H.22). In lengthy functions, you may want to look at a few key lines of code, and then continue debugging the caller’s code. The finish command is useful for situations in which you do not want to step through the remainder of a function line by line.
- 6. **Using the continue command to continue execution.** Enter the `continue` command to continue execution until the program terminates.
- 7. **Running the program again.** Breakpoints persist until the end of the debugging session in which they are set. So, the breakpoint you set in Step 2 is still set. Type `run` to run the program and enter `13` at the prompt. As in Step 3, the program runs until the breakpoint at line 25 is reached, then the debugger pauses and waits for the next command (Fig. H.23).

```
(gdb) step
Account::debit (this=0xbff81700, amount=13) at Account.cpp:33
33      if ( amount <= balance ) // debit amount does not exceed balance
(gdb)
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_1006_0.png)
