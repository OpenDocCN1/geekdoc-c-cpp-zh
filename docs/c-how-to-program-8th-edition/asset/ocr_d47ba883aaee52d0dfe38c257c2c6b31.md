**5. Modifying values.** You can change the values of variables during the program’s execution in the debugger. This can be valuable for experimenting with different values and for locating logic errors. You can use the debugger’s `set` command to change a variable’s value. Type `set withdrawalAmount = 42` to change the value of `withdrawalAmount`, then type `print withdrawalAmount` to display its new value (Fig. I.18).

```
```text
(gdb) set withdrawalAmount = 42
(gdb) print withdrawalAmount
$3 = 42
(gdb)
```
```

**Fig. I.18** | Setting the value of a variable while in break mode.

**6. Viewing the program result.** Type `continue` to continue program execution. Line 21 of Fig. I.3 executes, passing `withdrawalAmount` to Account member function `debit`. Function `main` then displays the new balance. Note that the result is $8 (Fig. I.19). This shows that the preceding step changed the value of `withdrawalAmount` from the value 13 that you input to 42.

```
```text
(gdb) continue
Continuing.
account1 balance: $8

Program exited normally.
(gdb)
```
```

**Fig. I.19** | Using a modified variable in the execution of a program.

**7. Using the quit command.** Use the `quit` command to end the debugging session (Fig. I.20). This command causes the debugger to terminate.

```
```text
(gdb) quit
$
```
```

**Fig. I.20** | Exiting the debugger using the quit command.

In this section, you used the debugger’s `print` command to evaluate arithmetic and boolean expressions. You also learned how to use the `set` command to modify the value of a variable during your program’s execution.

# 1.4 Controlling Execution Using the step, finish and next Commands

Sometimes you’ll need to execute a program line by line to find and fix errors. Walking through a portion of your program this way can help you verify that a function’s code ex-