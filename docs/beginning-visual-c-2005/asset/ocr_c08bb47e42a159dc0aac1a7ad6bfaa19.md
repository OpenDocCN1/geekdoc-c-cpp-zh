# Advanced Breakpoints

A more advanced way of specifying breakpoints is provided through a window you can display by pressing Alt+F9 or by selecting Breakpoints from the list displayed when you select the Windows button on the Debug toolbar — it’s at the right end. This window is shown in Figure 10-4.

![](bbox=[0.18, 0.18, 0.76, 0.34])

Figure 10-4

The Columns button on the toolbar enables you to add more columns to be displayed in the window. For example, you can display the source file name or the function name where the breakpoint is, or you can display what happens when the statement is reached.

You can set further options for a breakpoint by right-clicking the breakpoint line in the Breakpoints window and selecting from the pop-up. As well as setting a breakpoint at a location other than the beginning of a statement, you can set a breakpoint when a particular Boolean expression evaluates to true. This is a powerful tool but it does introduce very substantial overhead in a program as the expression needs to be re-evaluated continuously. Consequently, execution is slow, even on the fastest machines. You can also arrange that execution only breaks when the hit count, which is the number of the point has been reached, reaches a given value. This is most useful for code inside a loop where you won’t want to break execution on every iteration. If you set any condition on a breakpoint, the glyph changes so that a + appears in the center.

# Setting Tracepoints

A tracepoint is a special kind of breakpoint that has a custom action associated with it. You create a tracepoint by right-clicking the line where you want the tracepoint to be set and selecting the Breakpoint > When Hit menu item from the pop-up. You’ll see the dialog window shown in Figure 10-5.