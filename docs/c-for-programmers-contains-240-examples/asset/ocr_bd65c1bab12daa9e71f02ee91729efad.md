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

# 12. Using the quit command.

Use the quit command to end the debugging session (Fig. H.14). This command causes the debugger to terminate.

In this section, you used the gdb command to start the debugger and the run command to start debugging a program. You set a breakpoint at a particular line number in the main function. The break command can also be used to set a breakpoint at a line number in another file or at a particular function. Typing break, then the filename, a colon and the line number will set a breakpoint at a line in another file. Typing break, then a function name will cause the debugger to enter the break mode whenever that function is called.

Also in this section, you saw how the help list command will provide more information on the list command. If you have any questions about the debugger or any of its commands, type help or help followed by the command name for more information.

Finally, you examined variables with the print command and remove breakpoints with the delete command. You learned how to use the continue command to continue execution after a breakpoint is reached and the quit command to end the debugger.

```
(gdb) quit
$
```

Fig. H.14 | Exiting the debugger using the quit command.