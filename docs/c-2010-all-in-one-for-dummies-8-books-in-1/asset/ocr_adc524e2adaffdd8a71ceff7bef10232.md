+   3. Debug the program.

The program should stop on the `load` method.

+   4. Open the Immediate window.

You should be able to do this in the Debug window, or by pressing Ctrl+D, I.

+   5. Type ?this.

See the IntelliSense menu?

+   6. After the dot, type windowPosition.

The question mark in Step 5 means Print. This command prints the window position to the screen.

The response should be `windowDefaultLocation`.

That's what the Immediate window is for. You can do more than print values, you can change execution of your program. It is a powerful part of your debugging toolbox.

+   **The Breakpoints window**: Don't change anything in Visual Studio after trying the last. Press Ctrl+D, B. The Breakpoints window appears, and the breakpoint you added will be in it. (See Figure 2-13)

Figure 2-13:
The Breakpoints window, which isn't called the Bookmark window.

![](bbox=[0.218, 0.536, 0.555, 0.683])

What's here is that you can right-click on any breakpoint and completely alter the properties of breakpoint. Try it — the important options are described in this list:

+   * **Location**: Specifies the location of the line of code that should hold the breakpoint. This is convenient if you have filters set and you need to shift a line back.

+   * **Condition**: You can teach the breakpoint to stop at this line only if a certain variable is a specific value.

+   * **Hit Count**: Stop here only after the xth time it is hit.