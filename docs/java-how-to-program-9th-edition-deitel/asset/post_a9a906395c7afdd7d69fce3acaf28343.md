
Fig. F.27 | Reaching the breakpoint at line 13 in the Interest application.

![](img/009e962758dcc71dbc43a493362e6dc0_1429_0.png)

Fig. F.28 | Reaching the breakpoint at line 22 in the Interest application.

![](img/009e962758dcc71dbc43a493362e6dc0_1429_1.png)

Fig. F.29 | Printing year and amount during the first iteration of Interest’s for.

![](img/009e962758dcc71dbc43a493362e6dc0_1429_2.png)

6. Continuing execution. Type cont to continue execution. Line 22 executes and prints the current values of year and amount. After the for enters its second iteration, the debugger notifies you that the breakpoint at line 22 has been reached a second time. The debugger pauses each time a line where a breakpoint has been set is about to execute—when the breakpoint appears in a loop, the debugger pauses during each iteration. Print the values of variables year and amount again to see how the values have changed since the first iteration of the for (Fig. F.30).

![](img/009e962758dcc71dbc43a493362e6dc0_1429_3.png)

Fig. F.30 | Printing year and amount during the second iteration of Interest’s for.

7. Removing a breakpoint. You can display a list of all of the breakpoints in the application by typing clear (Fig. F.31). Suppose you’re satisfied that the Interest application’s for statement is working properly, so you want to remove the breakpoint at line 22 and allow the remaining iterations of the loop to proceed normally. You can remove the breakpoint at line 22 by typing clear Interest:22. Now type clear to list the remaining breakpoints in the application. The debugger should indicate that only the breakpoint at line 13 remains (Fig. F.31). This breakpoint has already been reached and thus will no longer affect execution.

![](img/009e962758dcc71dbc43a493362e6dc0_1430_0.png)

Fig. F.31 | Removing the breakpoint at line 22.

8. Continuing execution after removing a breakpoint. Type cont to continue execution. Recall that execution last paused before the print statement in line 22. If the breakpoint at line 22 was removed successfully, continuing the application will produce the correct output for the current and remaining iterations of the for statement without the application halting (Fig. F.32).

![](img/009e962758dcc71dbc43a493362e6dc0_1430_1.png)

Fig. F.32 | Application executes without a breakpoint at line 22.

In this appendix, you learned how to insert and remove breakpoints in the debugger. Breakpoints allow you to pause application execution so you can examine variable values with the debugger's print command. This capability will help you locate and fix logic errors in your applications. You saw how to use the print command to examine the value of an expression and how to use the set command to change the value of a variable. You also learned debugger commands (including the step, step up and next commands) that can be used to determine whether a method is executing correctly. You learned how to use the watch command to keep track of a field throughout the life of an application. Finally, you learned how to use the clear command to list all the breakpoints set for an application or remove individual breakpoints to continue execution without breakpoints.

## F.7 Wrap-Up

## Self-Review Exercises

F.1 Fill in the blanks in each of the following statements:
- a) A breakpoint cannot be set at a(n) ______.
- b) You can examine the value of an expression by using the debugger’s ______ command.
- c) You can modify the value of a variable by using the debugger’s ______ command.
- d) During debugging, the ______ command executes the remaining statements in the current method and returns program control to the place where the method was called.
- e) The debugger’s ______ command behaves like the step command when the next statement to execute does not contain a method call.
- f) The watch debugger command allows you to view all changes to a(n) ______.

F.2 State whether each of the following is true or false. If false, explain why.
- a) When application execution suspends at a breakpoint, the next statement to be executed is the statement after the breakpoint.
- b) Watches can be removed using the debugger’s clear command.
- c) The -g compiler option must be used when compiling classes for debugging.
- d) When a breakpoint appears in a loop, the debugger pauses only the first time that the breakpoint is encountered.

## Answers to Self-Review Exercises

F.1 a) comment. b) print. c) set. d) step up. e) next. f) field.

F.2 a) False. When application execution suspends at a breakpoint, the next statement to be executed is the statement at the breakpoint. b) False. Watches can be removed using the debugger’s unwatch command. c) True. d) False. When a breakpoint appears in a loop, the debugger pauses during each iteration.

## Formatted Output

![](img/009e962758dcc71dbc43a493362e6dc0_1432_0.png)

> *All the news that's fit to print.*
> —Adolph S. Ochs

> *What mad pursuit? What struggle to escape?*
> —John Keats

> *Remove not the landmark on the boundary of the fields.*
> —Amenehope

## Objectives

In this appendix you'll learn:
- To understand input and output streams.
- To use printf formatting.
- To print with field widths and precisions.
- To use formatting flags in the printf format string.
- To print with an argument index.
- To output literals and escape sequences.
- To format output with class Formatter.

| G.i | G.x |
|-----|-----|
| Introduction | Using Flags in the printf Format String |
| Streams | Printing with Argument Indices |
| Formatting Output with printf | Printing Literals and Escape Sequences |
| Printing Integers | Formatting Output with Class Formatter |
| Printing Floating-Point Numbers | Wrap-Up |
| Printing Strings and Characters |  |
| Printing Dates and Times |  |
| Other Conversion Characters |  |
| Printing with Field Widths and Precisions |  |

## G.1 Introduction

In this appendix, we discuss the formatting features of method printf and class Formatter (package java.util). Class Formatter formats and outputs data to a specified destination, such as a string or a file output stream. Many features of printf were discussed earlier in the text. This appendix summarizes those features and introduces others, such as displaying date and time data in various formats, reordering output based on the index of the argument and displaying numbers and strings with various flags.

## G.2 Streams

Input and output are usually performed with streams, which are sequences of bytes. In input operations, the bytes flow from a device (e.g., a keyboard, a disk drive, a network connection) to main memory. In output operations, bytes flow from main memory to a device (e.g., a display screen, a printer, a disk drive, a network connection).

When program execution begins, three streams are created. The standard input stream typically reads bytes from the keyboard, and the standard output stream typically outputs characters to a command window. A third stream, the standard error stream (System.err), typically outputs characters to a command window and is used to output error messages so they can be viewed immediately. Operating systems typically allow these streams to be redirected to other devices. Streams are discussed in detail in Chapter 17, Files, Streams and Object Serialization, and Chapter 27, Networking.

## G.3 Formatting Output with printf

Precise output formatting is accomplished with printf. Java borrowed (and enhanced) this feature from the C programming language. Method printf can perform the following formatting capabilities, each of which is discussed in this appendix:
- 1. Rounding floating-point values to an indicated number of decimal places.
- 2. Aligning a column of numbers with decimal points appearing one above the other.
- 3. Right justification and left justification of outputs.

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises
