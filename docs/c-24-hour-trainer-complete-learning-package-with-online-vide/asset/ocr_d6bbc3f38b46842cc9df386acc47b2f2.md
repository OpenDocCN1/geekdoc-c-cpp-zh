Statement from the context menu. Alternatively, you can place the cursor on the line and press Ctrl+Shift+F10. When you let the program continue, it starts executing from this line.

Setting the next statement to execute is useful for replaying history to see where an error occurred, re-executing a line after you change a variable's value (described in the “Using the Immediate Window” section later in this lesson), or to jump forward to skip some code.

Note that you can jump to only certain lines of code. For example, you can't jump to a comment or other line of code that doesn't actually do anything (you can't set a breakpoint there either), you can't jump to a different method, you can't jump at all if an error has just occurred, you can't jump to a variable declaration unless it also initializes the variable, and so forth. C# does its best, but it has its limits.

# USING WATCHES

Sometimes you may want to check a variable's value frequently as you step through the code one line at a time. In that case, pausing between steps to hover over a variable could slow you down, particularly if you have a lot of code to step through.

To make monitoring a variable easier, the debugger provides watches. A watch displays a variable's value whenever the program stops.

To create a watch, break execution, right-click a variable, and select Add Watch from the context menu. The bottom of Figure 12-4 shows a watch set on the variable subtotal. Each time the program executes a line of code and stops, the watch updates to display the variable's current value.

![](bbox=[0.15, 0.6, 0.52, 0.85])

FIGURE 12-4

The Watch window also highlights variables that have just changed in red. If you're tracking a lot of watches, this makes it easy to find the values that have just changed.