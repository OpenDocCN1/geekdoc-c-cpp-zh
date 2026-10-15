
In this section, you used the debugger’s **step** and **finish** commands to debug functions called during your program’s execution. You saw how the **next** command can step over a function call. You also learned that the **quit** command ends a debugging session.

## H.5 watch Command

The *watch command* tells the debugger to watch a data member. When that data member is about to change, the debugger will notify you. In this section, you’ll use the watch command to see how the Account object’s data member balance is modified during execution.

- **1. Starting the debugger.** Start the debugger by typing `gdb FigH_03`.

- **2. Setting a breakpoint and running the program.** Type `break 14` to set a breakpoint at line 14. Then, run the program with the command `run`. The debugger and program will pause at the breakpoint at line 14 (Fig. H.26).

```text
(gdb) break 14
Breakpoint 1 at 0x80486e5: file FigH_03.cpp, line 14.
(gdb) run
Starting program: /home/nuke/AppH/FigH_03

Breakpoint 1, main () at FigH_03.cpp:14
14        Account account1( 50 ); // create Account object
(gdb)
```

**Fig. H.26** | Running the program until the first breakpoint.

- **3. Watching a class’s data member.** Set a watch on account1’s balance data member by typing `watch account1.balance` (Fig. H.27). This watch is labeled as watchpoint 2 because watchpoints are labeled with the same sequence of numbers as breakpoints. You can set a watch on any variable or data member of an object currently in scope. Whenever the value of a watched variable changes, the debugger enters break mode and notifies you that the value has changed.

```text
(gdb) watch account1.balance
Hardware watchpoint 2: account1.balance
(gdb)
```

**Fig. H.27** | Setting a watchpoint on a data member.

- **4. Executing the constructor.** Use the `next` command to execute the constructor and initialize the account1 object’s balance data member. The debugger indicates that the balance data member’s value changed, shows the old and new values and enters break mode at line 20 (Fig. H.28).

```text
(gdb) next
Hardware watchpoint 2: account1.balance

Old value = 0
New value = 50
Account (this=0xbfcd6b90, initialBalance=50) at Account.cpp:20
20        if ( initialBalance < 0 )
(gdb)
```

**Fig. H.28** | Stepping into the constructor.

- **5. Exiting the constructor.** Type `finish` to complete the constructor’s execution and return to `main`.

- **6. Withdrawing money from the account.** Type `continue` to continue execution and enter a withdrawal value at the prompt. The program executes normally. Line 25 of Fig. H.3 calls Account member function debit to reduce the Account object’s balance by a specified amount. Line 34 of Fig. H.2 inside function debit changes the value of balance. The debugger notifies you of this change and enters break mode (Fig. H.29).

```text
(gdb) continue
Continuing.
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

Hardware watchpoint 2: account1.balance

Old value = 50
New value = 37
0x0804893b in Account::debit (this=0xbfcd6b90, amount=13) at Account.cpp:34
34            balance = balance - amount;
(gdb)
```

**Fig. H.29** | Entering break mode when a variable is changed.

- **7. Continuing execution.** Type continue—the program will finish executing function main because the program does not attempt any additional changes to balance. The debugger removes the watch on account1’s balance data member because the account1 object goes out of scope when function main ends. Removing the watchpoint causes the debugger to enter break mode. Type continue again to finish execution of the program (Fig. H.30).

```text
(gdb) continue
Continuing.
account1 balance: $37

Watchpoint 2 deleted because the program has left the block in which its expression is valid.
0xb7da0595 in exit () from /lib/tls/i686/cmov/libc.so.6
(gdb) continue
Continuing.

Program exited normally.
(gdb)
```

**Fig. H.30** | Continuing to the end of the program.

- **8. Restarting the debugger and resetting the watch on the variable.** Type run to restart the debugger. Once again, set a watch on account1 data member balance by typing watch account1.balance. This watchpoint is labeled as watchpoint 3. Type continue to continue execution (Fig. H.31).

```text
(gdb) run
Starting program: /home/nuke/AppH/FigH_03

Breakpoint 1, main () at FigH_03.cpp:14
14          Account account1( 50 ); // create Account object
(gdb) watch account1.balance
Hardware watchpoint 3: account1.balance
(gdb) continue
Continuing.
Hardware watchpoint 3: account1.balance

Old value = 0
New value = 50
Account (this=0xbfd8eb90, initialBalance=50) at Account.cpp:20
20          if ( initialBalance < 0 )
(gdb)
```

**Fig. H.31** | Resetting the watch on a data member.

- **9. Removing the watch on the data member.** Suppose you want to watch a data member for only part of a program’s execution. You can remove the debugger’s watch on variable balance by typing delete 3 (Fig. H.32). Type continue—the program will finish executing without reentering break mode.

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

**Fig. H.32** | Removing a watch.

In this section, you used the watch command to enable the debugger to notify you when the value of a variable changes. You used the delete command to remove a watch on a data member before the end of the program.

## H.6 Wrap-Up

In this appendix, you learned how to insert and remove breakpoints in the debugger. Breakpoints allow you to pause program execution so you can examine variable values with the debugger’s print command, which can help you locate and fix logic errors. You used the print command to examine the value of an expression, and you used the set command to change the value of a variable. You also learned debugger commands (including the step, finish and next commands) that can be used to determine whether a function is executing correctly. You learned how to use the watch command to keep track of a data member throughout the scope of that data member. Finally, you learned how to use the info break command to list all the breakpoints and watchpoints set for a program and the delete command to remove individual breakpoints and watchpoints.

## Bibliography

For additional C++ books, articles and more, please visit the Deitel C++ Resource Center at

www.deitel.com/cplusplus

- Abrahams, D. and A. Gurtovoy. *C++ Template Metaprogramming: Concepts, Tools, and Techniques from Boost and Beyond.* Boston, MA: Addison-Wesley Professional, 2004.
- Alexandrescu, A. *Modern C++ Design: Generic Programming and Design Patterns Applied.* Boston, MA: Addison-Wesley Professional, 2001.
- Alhir, S. *UML in a Nutshell.* Cambridge, MA: O’Reilly & Associates, Inc., 1998.
- Almarode, J. “Object Security.” *Smalltalk Report* Vol. 5, No. 3 November/December 1995, 15–17.
- *American National Standard, Programming Language C++.* (ANSI Document ISO/IEC 14882), New York, NY: American National Standards Institute, 1998.
- Anderson, A. E. and W. J. Heinze. *C++ Programming and Fundamental Concepts.* Englewood Cliffs, NJ: Prentice Hall, 1992.
- Arciniegas, F. *C++ XML.* Indianapolis, IN: Sams, 2001.
- Arlow, J. and I. Neustadt. *UML 2 and the Unified Process: Practical Object-Oriented Analysis and Design, Second Edition.* Boston, MA: Addison-Wesley Professional, 2005.
- Astle, D. and K. Hawkins. *Beginning OpenGL Game Programming.* Boston, MA: Course Technology PTR, 2004.
- Bar-David, T. *Object-Oriented Design for C++.* Englewood Cliffs, NJ: Prentice Hall, 1993.
- Beck, K. “Birds, Bees, and Browsers—Obvious Sources of Objects.” *The Smalltalk Report* Vol. 3, No. 8, June 1994, 13.
- Becker, P. “Shrinking the Big Switch Statement.” *Windows Tech Journal* Vol. 2, No. 5, May 1993, 26–33.
- Becker, P. “Conversion Confusion.” *C++ Report* October 1993, 26–28.
- Berard, E. V. *Essays on Object-Oriented Software Engineering: Volume I.* Englewood Cliffs, NJ: Prentice Hall, 1993.
- Binder, R. V. “State-Based Testing.” *Object Magazine* Vol. 5, No. 4, August 1995, 75–78.
- Binder, R. V. “State-Based Testing: Sneak Paths and Conditional Transitions.” *Object Magazine* Vol. 5, No. 6, October 1995, 87–89.
- Blum, A. *Neural Networks in C++: An Object-Oriented Framework for Building Connectionist Systems.* New York, NY: John Wiley & Sons, 1992.
- Booch, G. *Object Solutions: Managing the Object-Oriented Project.* Reading, MA: Addison-Wesley, 1996.
- Booch, G. *Object-Oriented Analysis and Design with Applications, Third Edition.* Reading, MA: Addison-Wesley, 2005.
