# Running code with the Immediate window

Open the Immediate window (also called the Debug window) by choosing View ▸ Immediate Window or by pressing Ctrl+G. You can open the Immediate window any time (for example, while you're working on a form's design). You'll sometimes find it useful to test a line of code or run a procedure (both of which are supported by the Immediate window) while you're working on a form or report.

The Immediate window is shown in Figure 27.6. The Immediate window permits certain interactivity with the code and provides an output area for Debug.Print statements. The basic debugging procedures include stopping execution so that you can examine code and variables, dynamically watching variable values, and stepping through code.

# FIGURE 27.6

Get to know the Immediate window. You'll use it a lot in Access.

![](bbox=[0.18, 0.52, 0.88, 0.68])

One of the most basic uses of the Immediate window is to run code, such as built-in functions, or subroutines and functions that you've written. Figure 27.7 shows several examples that have been run in the Immediate window.

# FIGURE 27.7

Running code from the Immediate window is a common practice.

![](bbox=[0.18, 0.88, 0.88, 0.96])

The first example in Figure 27.7 shows how to run a subprocedure (UsingDebugDotPrint) that's been added to the VBA project. This subprocedure includes a Debug.Print statement that returns a long SQL statement, and that output is shown below the procedure name when the Enter key is pressed.

In the second example, the built-in Now() function has been run from the Immediate window, returning the current date and time. The question mark (?) in front of the Now()