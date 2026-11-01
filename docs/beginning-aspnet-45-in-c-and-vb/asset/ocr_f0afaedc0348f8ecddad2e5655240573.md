# Immediate Window

The last interesting debugging window is the Immediate window. This window enables you to execute code as if you had written it in a page, for example. You can use this window to test expressions, see what values a function returns, and so on. For example, when you are in debug mode, you can enter the following command in the Immediate window:

```
VB.NET
? New Calculator().Add(3, 4)
```

```
C#
? new Calculator().Add(3, 4);
```

The question mark is used to output to the Immediate window. The code then instantiates a new Calculator instance and directly passes the values 3 and 4 to its Add method. The code is executed and the Add method returns 7, which is then printed in the Immediate window.

This window is great for quickly testing out code. Instead of writing code you want to test in a page, you can type it directly in the Immediate window and see its output.

In the following Try It Out, you see these debugging windows at work.

# TRY IT OUT Extensive Debugging

In this exercise, you look at all the debugging windows that have been discussed earlier. Because a lot of windows and options are available, you won’t see a detailed discussion of every step in the process. Instead, you’re encouraged to experiment. Try adding more variables to the Watch window, type your own code in the Immediate window, and so on. Experimenting is the best way to discover the large number of debugging capabilities in VS.

+   1. If you’re still in debug mode from the preceding exercise, press Shift+F5 or press the Stop button on the debugging toolbar. Open the Code Behind of CalculatorDemo.aspx again and press Ctrl+Shift+F9 to clear all previously set breakpoints in all code files. Click Yes to confirm the deletion.
+   2. Click the line that declares the variable value1 and press F9 to set a breakpoint. Your Document Window should look similar to Figure 18-14, which shows the Document Window for the C# project.

![](bbox=[0.2, 0.85, 0.8, 0.95])

FIGURE 18-14