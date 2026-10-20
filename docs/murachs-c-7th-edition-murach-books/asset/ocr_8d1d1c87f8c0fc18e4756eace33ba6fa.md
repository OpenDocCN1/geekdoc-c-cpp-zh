# Perspective

As you can now appreciate, Visual Studio provides a powerful set of debugging tools. With tools like these, a difficult debugging job becomes more manageable.

# Terms

+   - break mode
+   - data tip
+   - Edit and Continue feature
+   - breakpoint
+   - logical error
+   - tracepoint
+   - step through an application
+   - PerfTip
+   - Run to Click feature
+   - watch expression
+   - call stack

# Exercise 11-1 Step through an application

If you did exercise 5-2 in chapter 5, you’ve already set breakpoints, used the Locals window, and stepped through an application. So in this exercise, you’ll use some of the new skills that were presented in this chapter.

# Use the Edit and Continue feature

+   1. Open the application that’s in the C:\C#\Chapter 11\FutureValue directory. Then, run the project with the default entries, and notice that the future value amount is formatted as a percent.
+   2. End the application and set a breakpoint on the statement in the btnCalculate_Click() method that calls the method that calculates the future value. Then, run the application with the default entries so it enters break mode. In break mode, notice that the statement after the breakpoint uses p instead of c as the formatting code. Correct this code, and press F5 to continue running the application and notice that the formatting is now correct.
+   3. This illustrates the Edit and Continue feature. Sometimes, though, Visual Studio won’t let you change the code in break mode. Then, you can click on the Stop Debugging button, make the change, and restart the application.

# Use the Locals window

+   4. Click on the Calculate button to enter break mode again, display the Locals window, click on the ▷ symbol to the left of the this keyword, scroll down to txtMonthlyInvestment, and click on its ▷ symbol to expand this entry. Then, scroll down to the Text property to see its string value and the Visualizer icon in the Value column.
+   5. Click on the Visualizer icon to display the value in the Text Visualizer dialog box. Then, close this dialog box, and click on the ◁ symbol to the left of the this keyword to collapse this entry.