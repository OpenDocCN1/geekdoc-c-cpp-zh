function name is a shortcut for the Print keyword. Instead of typing ?Now, you can type Print Now. Both the question mark and the Print keyword are a directive to the Immediate window to display (or print) the value returned by the Now() function.

The third example in Figure 27.7 shows calling a function (IsLastDayOfMonth) from the Immediate window. As with Now(), the question mark is used to direct VBA to return the value from the function. The one required argument is passed, and the result is shown below the function call. This function was changed from Private to Public for this example, as only Public functions can be called from the Immediate window.

# Suspending execution with breakpoints

You suspend execution by setting a breakpoint in the code. When Access encounters a breakpoint, execution immediately stops, allowing you to switch to the Immediate window to set or examine the value of variables.

Setting a breakpoint is easy. Open the code window and click the gray Margin Indicator bar to the left of the statement on which you want execution to stop (see Figure 27.8). Alternatively, position the cursor on the line and click the Breakpoint toolbar button. The breakpoint itself appears as a large brown dot in the gray bar along the left edge of the code window and as a brown highlight behind the code. The text of the breakpoint statement appears in a bold font.

FIGURE 27.8

Setting a breakpoint is easy.

![](bbox=[0.22, 0.7, 0.88, 0.93])