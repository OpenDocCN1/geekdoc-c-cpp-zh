+   5. Click the Next Line button on the Debugger toolbar so that you are one line beyond the following line:

```
int i = 10;
```

The application changes the value of i to 10, as shown in Figure 3-7. The variable is still shown in red because its value has just changed. However, notice that NumberOfPieces is now shown in black because its value hasn't changed since the last instruction.

FIGURE 3-7: Assigning a value to i changes its value in the Watches window.

![](bbox=[0.248, 0.267, 0.588, 0.413])

+   6. Click Next Line on the Debugger toolbar.
+   7. Click Debug/Continue.
+   8. Remove any breakpoints you've set in the example application.

# Changing values

Sometimes you need to verify that the application works as intended by simulating changes that might occur in the code. In many cases, this means changing a value from its default to the value you want to test. Fortunately, the Watches window provides the means to perform this task. Follow these steps to see how you can change variable values:

+   1. Set a breakpoint at the `i = i + SpecialMath(i);` line in `main()`.
+   2. Click Debug/Continue.