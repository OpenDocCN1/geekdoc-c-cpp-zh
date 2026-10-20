# F.1 Introduction

In Chapter 2, you learned that there are two types of errors—syntax errors and logic errors—and you learned how to eliminate syntax errors from your code. Logic errors do not prevent the application from compiling successfully, but they do cause an application to produce erroneous results when it runs. The JDK includes software called a debugger that allows you to monitor the execution of your applications so you can locate and remove logic errors. The debugger will be one of your most important application development tools. Many IDEs provide their own debuggers similar to the one included in the JDK or provide a graphical user interface to the JDK’s debugger.

This appendix demonstrates key features of the JDK’s debugger using command-line applications that receive no input from the user. The same debugger features discussed here can be used to debug applications that take user input, but debugging such applications requires a slightly more complex setup. To focus on the debugger features, we’ve opted to demonstrate the debugger with simple command-line applications involving no user input. For more information on the Java debugger visit download.oracle.com/javase/6/docs/technotes/tools/windows/jdb.html.

# F.2 Breakpoints and the run, stop, cont and print Commands

We begin our study of the debugger by investigating breakpoints, which are markers that can be set at any executable line of code. When application execution reaches a breakpoint, execution pauses, allowing you to examine the values of variables to help determine whether logic errors exist. For example, you can examine the value of a variable that stores the result of a calculation to determine whether the calculation was performed correctly. Setting a breakpoint at a line of code that is not executable (such as a comment) causes the debugger to display an error message.

To illustrate the features of the debugger, we use application AccountTest (Fig. F.1), which creates and manipulates an object of class Account (Fig. 3.13). Execution of AccountTest begins in main (lines 7–24). Line 9 creates an Account object with an initial balance of $50.00. Recall that Account’s constructor accepts one argument, which specifies the Account’s initial balance. Lines 12–13 output the initial account balance using Account method getBalance. Line 15 declares and initializes a local variable depositAmount. Lines 17–19 then print depositAmount and add it to the Account’s balance using

+   F.1 Introduction
+   F.2 Breakpoints and the run, stop, cont and print Commands
+   F.3 The print and set Commands
+   F.4 Controlling Execution Using the step, step up and next Commands
+   F.5 The watch Command
+   F.6 The clear Command
+   F.7 Wrap-Up

Self-Review Exercises | Answers to Self-Review Exercises