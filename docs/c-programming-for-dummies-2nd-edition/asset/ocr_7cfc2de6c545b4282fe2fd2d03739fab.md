12. Keep clicking the Next Line button to work through the for loop.

When you're satisfied that the code has been debugged:

13. Click the Stop button.

The program runs fine after you fix the stray semicolon. See the later section "Watching variables" for insight into how variable values can be examined by the debugger.

# Setting a breakpoint

No one wants to step through 200 lines of source code to find a bug. Odds are that you have a good idea where the bug is, either by the program's output or because it ran just five minutes ago, before you edited that one particular section. If so, you know where you want to snoop into operations. It's at that place in your code that you set a debugging breakpoint.

A breakpoint is like a stop sign in your text. In fact, that's the exact icon used by Code::Blocks, as shown in Figure 25-2. To set a breakpoint, click the mouse between the line number and the green line (or yellow line, if you haven't saved yet). The Breakpoint icon appears.

![](bbox=[0.25, 0.6, 0.75, 0.82])

FIGURE 25-2:
A breakpoint in the code.

![](bbox=[0.15, 0.85, 0.22, 0.9])

To run your code to the breakpoint, click the Debug/Continue button on the Debugging toolbar. The program runs, but then comes to a screeching halt at the breakpoint. From this point on, you can work the debugger to see what's going wrong.