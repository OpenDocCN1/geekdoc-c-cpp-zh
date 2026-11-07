
- **4. Continuing execution.** Select **Debug > Continue** to execute the program until the second breakpoint at line 18. The **Autos** window displays uninitialized local variable `withdrawalAmount` (Fig. H.22), which has a large negative value.

![](img/bfd978e7e9b192bab46ec2a89e481263_1235_0.png)

**Fig. H.22** | Autos window displaying local variable withdrawalAmount.

- **5. Entering data.** Select **Debug > Step Over** to execute line 18. At the program’s input prompt, enter a value for the withdrawal amount. The **Autos** window updates the value of local variable `withdrawalAmount` with the value you entered (Fig. H.23).

![](img/bfd978e7e9b192bab46ec2a89e481263_1235_1.png)

**Fig. H.23** | Autos window displaying updated local variable withdrawalAmount.

- **6. Stopping the debugger.** Select **Debug > Stop Debugging** to end the debugging session. Remove all remaining breakpoints.

## H.6 Wrap-Up

In this appendix, you learned how to insert, disable and remove breakpoints in the Visual Studio debugger. Breakpoints allow you to pause program execution so you can examine variable values. This capability will help you locate and fix logic errors in your programs. You saw how to use the **Locals** and **Watch** windows to examine the value of an expression and how to change the value of a variable. You also learned debugger commands **Step Into**, **Step Over**, **Step Out** and **Continue** that can be used to determine whether a function is executing correctly. Finally, you learned how to use the **Autos** window to examine variables used specifically in the previous and next commands.

## Summary

### Section H.1 Introduction

- Most C++ compiler vendors provide software called a debugger, which allows you to monitor the execution of your programs to locate and remove logic errors.
- Breakpoints are markers that can be set at any executable line of code. When program execution reaches a breakpoint, execution pauses.

## Self-Review Exercises

- **H.1** Fill in the blanks in each of the following statements:
  - a) When the debugger suspends program execution at a breakpoint, the program is said to be in break mode.
  - b) The ______ feature in Visual Studio 2005 allows you to look at the value of a variable by positioning the mouse over the variable name in the code.
  - c) You can examine the value of an expression by using the debugger’s ______ window.
  - d) The ______ command behaves like the Step Into command when the next statement to execute does not contain a function call.

- **H.2** State whether each of the following is true or false. If false, explain why.
  - a) When program execution suspends at a breakpoint, the next statement to be executed is the statement after the breakpoint.
  - b) When a variable’s value is changed, it becomes yellow in the Autos and Locals windows.
  - c) During debugging, the Step Out command executes the remaining statements in the current function and returns program control to the place where the function was called.

## Answers to Self-Review Exercises

- **H.1** a) break. b) *Quick Info*. c) *Watch*. d) **Step Over**.

- **H.2** a) False. When program execution suspends at a breakpoint, the next statement to be executed is the statement at the breakpoint. b) False. A variable turns red when its value is changed. c) True.

## I Using the GNU C++ Debugger

![](img/bfd978e7e9b192bab46ec2a89e481263_1238_0.png)

> And so shall I catch the fly.
>
> —William Shakespeare
>
> We are built to make mistakes,
> coded for error.
>
> —Lewis Thomas
>
> What we anticipate seldom
> occurs; what we least expect
> generally happens.
>
> —Benjamin Disraeli

### Objectives

In this appendix you’ll learn:

- To use the `run` command to run a program in the debugger.
- To use the `break` command to set a breakpoint.
- To use the `continue` command to continue execution.
- To use the `print` command to evaluate expressions.
- To use the `set` command to change variable values during program execution.
- To use the `step`, `finish` and `next` commands to control execution.
- To use the `watch` command to see how a data member is modified during program execution.
- To use the `delete` command to remove a breakpoint or a watchpoint.

```cpp
// Fig. I.1: Account.h
// Definition of Account class.
class Account
{
public:
   Account( int ); // constructor initializes balance
   void credit( int ); // add an amount to the account balance
   void debit( int ); // subtract an amount from the account balance
   int getBalance(); // return the account balance
private:
   int balance; // data member that stores the balance
}; // end class Account
```

**Fig. I.1** | Header file for the Account class.

```cpp
// Fig. I.2: Account.cpp
// Member-function definitions for class Account.
#include <iostream>
#include "Account.h" // include definition of class Account
using namespace std;

// Account constructor initializes data member balance
Account::Account( int initialBalance )
{
   balance = 0; // assume that the balance begins at 0

   // if initialBalance is greater than 0, set this value as the
   // balance of the Account; otherwise, balance remains 0
   if ( initialBalance > 0 )
      balance = initialBalance;

   // if initialBalance is negative, print error message
   if ( initialBalance < 0 )
      cout << "Error: Initial balance cannot be negative.\n" << endl;
} // end Account constructor

// credit (add) an amount to the account balance
void Account::credit( int amount )
{
   balance = balance + amount; // add amount to balance
} // end function credit

// debit (subtract) an amount from the account balance
void Account::debit( int amount )
{
   if ( amount <= balance ) // debit amount does not exceed balance
      balance = balance - amount;
   else // debit amount exceeds balance
      cout << "Debit amount exceeded account balance.\n" << endl;
} // end function debit
```

**Fig. I.2** | Definition for the Account class. (Part 1 of 2.)

```text
$ gdb FigI_03
GNU gdb 6.3-debian
Copyright 2004 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it and/or distribute copies of it under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB. Type "show warranty" for details.
This GDB was configured as "i486-linux-gnu"...Using host libthread_db library "/lib/tls/i686/cmov/libthread_db.so.1".

(gdb)
```

**Fig. I.4** | Starting the debugger to run the program.

```text
(gdb) run
Starting program: /home/nuke/App1/FigI_03
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

account1 balance: $37

Program exited normally.
(gdb)
```

**Fig. I.5** | Running the program with no breakpoints set.

The line number specified as its argument (i.e., 13). You can set as many breakpoints as necessary. Each breakpoint is identified by the order in which it was created. The first breakpoint is known as Breakpoint 1. Set another breakpoint at line 21 by typing `break 21` (Fig. I.6). This new breakpoint is known as Breakpoint 2. When the program runs, it suspends execution at any line that contains a breakpoint and the debugger enters **break mode**. Breakpoints can be set even after the debugging process has begun. *[Note: If you do not have a numbered listing for your code, you can use the `list` command to output your code with line numbers. For more information about the list command type `help list` from the gdb prompt.]*

```text
(gdb) break 13
Breakpoint 1 at 0x80486f6: file FigI_03.cpp, line 13.
(gdb) break 21
Breakpoint 2 at 0x8048799: file FigI_03.cpp, line 21.
(gdb)
```

**Fig. I.6** | Setting two breakpoints in the program.

- **5. Running the program and beginning the debugging process.** Type `run` to execute your program and begin the debugging process (Fig. I.7). The debugger enters
