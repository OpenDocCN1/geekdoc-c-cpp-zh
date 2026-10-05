
# The Visualizer drop-down menu in the Locals

![](img/3148667e42d4db35b3d08576aaa1fa01_366_0.png)

# The Text Visualizer dialog box

![](img/3148667e42d4db35b3d08576aaa1fa01_366_1.png)

# Description

- All string values that are displayed by the debugging windows have a Visualizer icon (a magnifying glass) to their right.
- To display an appropriate Visualizer dialog box for the string value, select the appropriate command from the drop-down list that is available from the Visualizer icon.

Figure 11-13 How to use the Visualizer dialog boxes to view strings

# Perspective

As you can now appreciate, Visual Studio provides a powerful set of debugging tools. With tools like these, a difficult debugging job becomes manageable.

# Terms

| break mode | logical error |
| :--- | :--- |
| data tip | step through an application |
| Edit and Continue feature | watch expression |
| breakpoint | call stack |

# Exercise 11-1 Use the debugging tools

If you did execute 5-2 in chapter 5, you've already set breakpoints, used the Locals window, and stepped through an application. So in this exercise, you'll use some of the new skills that were presented in this chapter.

## Use the Edit and Continue feature

1. Open the application that's in the C\C# 2010\Chapter 11\FutureValue directory. Then, run the project with the default entries, and notice that the future value is formatted as a percent.
2. End the application and set a breakpoint on the statement in the btmCalculate,Click method that calls the method that calculates the future value. Then, in break mode, notice that the statement after the breakpoint enters break mode. instead of c as the formatting code. Correct this code, and press F5 to running the application and notice that the formatting is now correct.
3. This illustrates the Edit and Continue feature. Sometimes, Visual Studio won't let you change the code in break mode. Then, you can click on the Stopping Debug button, make the change, and restart the application.
4. Click on the button to enter break mode again, display the Locals window, click on the plus sign to the left of this keyword, scroll down to txtMonthlyInvestment, and click on its plus sign to expand this entry. Then, scroll down to the Text property to see its string value and the Visualizer icon in the value column.
5. Click on the Visualizer icon to display the value in the Text Visualizer dialog box. Then, close this dialog box, and click on the minus sign to the left of this keyword to collapse this entry.
6. Press F11 to step through the statements, and notice the parameters and variables that are displayed in the Locals window at each step. Then, set a

## Use the Locals windows

Chapter 11    How to debug an application

second breakpoint on the last statement in the CalculateFutureValue method (the return statement), and press F5 to run the application until it enters break mode. Now, you can see the final values for the calculation.

7. Press F5 to restart the application and display the Future Value form. Click on the Calculate button to start another calculation and enter break mode again. Next, locate the variables in the Locals window, double-click in the Value column, enter 24, and press the Enter key to change the value. Then, press F5 to continue execution, and notice that 24 is used as the value of the months variable in the future value calculation.

## Use the Breakpoints window to disable both breakpoints

If you're using C# 2010 Express, skip the next two steps.

8. Display the Breakpoints window and click the Disable All Breakpoints button at the top of the Breakpoints window. This disables break points without removing them. Then, press F5 to continue execution. Since no breakpoints are enabled, this should display the Future Value form.
9. Click the Exit button to end the program. Then, use the Debug->Enable All Breakpoints command to enable both breakpoints, and run the application until it enters break mode at the first breakpoint.

## Use the Immediate window to work with a variable and a method

10. Display the Immediate window, and display the value of the months variables in this window. Then, display the percentage format of the monthly interest rate by calling the ToString method from the monthlyInterestRate variable like:
`? monthlyInterestRate.ToString("P")`
11. Assign a value of 12 to the months variable by entering an assignment statement in the Immediate window. Then, continue running the application so you can see that this value is used in the calculations.

## Use a Watch window to monitor expressions

12. Run the application one more time with a value of 1 for the years entry. When the application enters break mode, display a Watch window, highlight the futureValue variable, and drag the i to that window. Next, drag the i to the Name column of the first block row in the Watch window and enter this expression:

```
i < months
```
13. Press F11 to step through the application and check the values in the Watch window until the value of i < months becomes false.

## Use the Output window

14. Use the Console.WriteLine method in the btnCalculate_Click method to display the values of the monthlyInvestment, monthlyInterestRate, and, futureValue variables. Then, run the application and check the values.
15. When you're done, close the project.

# Section 3 Object-oriented programming

In this section, you'll learn how classes are provided by the .NET. For instance, you'll learn how to use classes to structure an application. You'll also learn how to create properties, methods, fields, and constructors. In addition, you'll see a complete application that uses user-defined classes, and you'll learn how to create structures, which are similar to classes.

When you complete this section, you'll start to see how your own classes can help the development of an application. As a bonus, you'll have a better understanding of how .NET works.

# How to create and use classes

This chapter presents the basics of creating and using classes in C#. Here, you'll learn how to create classes that include properties, methods, fields, and constructors, as well as classes that contain static members. In addition, you'll see a complete application that uses user-defined classes, and you'll learn how to create structures, which are similar to classes.
