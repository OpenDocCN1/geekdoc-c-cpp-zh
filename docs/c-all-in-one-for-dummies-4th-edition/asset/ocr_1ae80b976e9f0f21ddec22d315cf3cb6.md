![](bbox=[0.24, 0.05, 0.85, 0.45])

FIGURE 3-1: Code::Blocks displays any breakpoints you set using a red octagon.

The application runs until it gets to the breakpoint you chose for the `int BrokenMirror::GetNumberOfPieces()` line, as shown in Figure 3-2. Note that execution actually ends with the opening curly brace because this is the beginning of execution for this function. The yellow, right-pointing triangle tells you the current instruction that the Code::Blocks debugger will execute. You can now click the Next Line button (the button with two squares and an arrow pointing from the upper square to the lower square) to move to the next line, or you can click Debug/Continue to run the rest of the application.

# ## Enabling and disabling breakpoints

You may have times when you have several breakpoints set and you want to turn them off momentarily but don't want to lose them because you may want to turn them back on later. You can do this by *disabling* the breakpoints. Disabling the breakpoint is faster than removing the breakpoints and then going back and finding them again to turn them back on. Use the following steps to disable a breakpoint:

+   1. **Right-click the red octagon on the left side of the editor and choose Edit Breakpoint from the context menu.**

You see the Edit Breakpoint dialog box, as shown in Figure 3-3.