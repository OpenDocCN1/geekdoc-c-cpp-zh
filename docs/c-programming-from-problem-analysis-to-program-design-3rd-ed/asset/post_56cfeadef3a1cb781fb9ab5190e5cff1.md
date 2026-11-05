
## Breakpoints

**Breakpoints** are markers that are placed in an application, indicating the program should halt execution when it reaches that point. When the break occurs, the program and the Debugger are said to be in break mode. While in break mode, you can examine expressions to see what values are being generated. If your program is not consistently producing correct results, this enables you to check intermediate values.

You can use several methods to add or set a breakpoint. The simplest method is to click anywhere on a line of executable code where you want to set a breakpoint and select **Toggle Breakpoint** from the **Debug** menu or use the **F9** keyboard shortcut. As the menu option name implies, pressing **F9**, or selecting **Toggle Breakpoint** a second time turns off the breakpoint. The line of code is also automatically selected, as shown in Figure 12-4. You can place any number of breakpoints in your program following these methods.

![](img/e33ae760e23d89eac66541252ad65de8_759_0.png)

**Figure 12-4** Breakpoint set

![](img/e33ae760e23d89eac66541252ad65de8_759_1.png)

It can be useful to know how many times a breakpoint has been set. When you right-click the selected breakpoint glyph, you can then choose the **Hit Count** option from the shortcut menu.

After a breakpoint is set and you run your program by selecting the **Start Debugging (F5)** option, it runs completely as before until it reaches the breakpoint. At that line, the program halts, or pauses, before it executes the line. While the program is paused, you can move the mouse over any variable and see what its current value is. You can also select conditional expressions associated with **if** statements or loop expressions and see whether they have produced a **true** or **false** result at the time the program is halted. In addition to being able to hover over the variable to see its value, the Debugger will also display a **Locals** window near the bottom of the screen. This window automatically shows all variables and their values. This is illustrated in Figure 12-5.

![](img/e33ae760e23d89eac66541252ad65de8_760_0.png)

Figure 12-5 Locals window at the breakpoint

![](img/e33ae760e23d89eac66541252ad65de8_760_1.png)

If you are in debugging mode and do not see the Locals window at the bottom of the screen, use the **Windows** option from the **Debug** menu to display the window.

In Chapter 5, an application was developed to calculate a speeding fine. The user was asked to input the speed limit, the speed they were traveling, and the student’s classification. A breakpoint was set on the line that calculated the fine. Prior to the breakpoint, in the constructor of the **Ticket** class, the speed for the fine was calculated. As you can see in the **Locals** window shown in Figure 12-5, you see values for speed, speedLimit, and classif. At that breakpoint, Fine and fine values have not been set. You can see that execution halts prior to the program statements on that line being executed.

## Continue

After reviewing the variables and expressions, pressing **F5** or selecting **Continue** from the **Debug** menu takes the program out of break mode and restores it to a run-time mode. If only one breakpoint is set, the **Locals** window closes and the execution continues until the end of the **Main()** method is reached. At that point, the program terminates. However, if more than one breakpoint is set, selecting **Continue** causes the program to execute from the halted line until it reaches the second breakpoint. At that point, the **Locals** window is updated and the program is again paused. To illustrate the changes made to the **Locals** window, a second breakpoint was set on the last line in the `SetFine()` method of the `Ticket` class. As shown in Figure 12-6, the `Fine` variable and `Fine` property were changed from 0 to 712.5. The **Debugger** highlights the line where the program halts. The process of stopping at each breakpoint would continue until the end of the program was encountered.

![](img/e33ae760e23d89eac66541252ad65de8_761_0.png)

**Figure 12-6** Next breakpoint

### Stepping Through Code

Instead of setting specific breakpoints in your source code, you could step through your code line by line, see the execution path, and examine variable and expression values as they change. The **Debug** menu, which was shown in Figures 12-2 and 12-3, offers three commands for stepping through code while you are in break mode. These commands and their keyboard shortcuts are:

- **Step Into (F11)**
- **Step Over (F10)**
- **Step Out (Shift+F11)**

Both the **Step Into** and **Step Over** commands tell the Debugger to execute the next line of code. The functionality of these two commands differs when a method is invoked. When the **Step Into** command encounters a line that contains a call to a method, the call is executed—the program halts at the first line of code inside the called method. The **Step Over** command differs in that it executes the entire method called before it halts. It pauses at the first line of code outside the method.

**Step Into** is useful for allowing you to look inside a method and examine the method’s program statements. **Step Over** completes all the program statements in the method before it halts—giving you no opportunity to examine the variables, expressions, or flow of program statements.

Review Figure 12-2 and note that the **Step Out** option is not shown. It does not appear until you are in debugging mode. When debugging, as shown in Figure 12-3, you can see this added option. If you are executing statements inside a method and want to return to the calling method, this third command, **Step Out**, is useful. **Step Out** causes the rest of the program statements in the method to be executed and then returns control to the method that called it. At that point, it halts the program so that you can examine the code.

When you use these step commands, the values are automatically updated in the **Locals** window with each new line of code. You can see the live changes made to variable values as you step through the program. You can also follow the flow of control and see the order of execution of program statements for the application. This can be especially helpful when the application has complex selection statements or nested loops. As illustrated in Figure 12-7, the line of code executed next is highlighted in yellow.

![](img/e33ae760e23d89eac66541252ad65de8_762_0.png)

Figure 12-7 Breakpoint location

> You can use the keyboard shortcuts F11, F10, and Shift+F11—representing **Step Into**, **Step Over**, and **Step Out**—when you are stepping through an application.

### Watches

You also have the capability of setting **Watch** windows during debugging sessions. The **Watch** window lets you type in one or more variables or expressions that you want to observe while the program is running. Unlike the **Locals** window, which shows all variables currently in scope, you selectively identify the variables or expressions for the **Watch** window. A **QuickWatch** option on the **Debug** window lets you type in a single variable or expression and have the Debugger show its value. From the **QuickWatch** dialog box, you can add the identifier to a **Watch** window. This is illustrated in Figure 12-8.

![](img/e33ae760e23d89eac66541252ad65de8_763_0.png)

Figure 12-8 QuickWatch window

> You can also do an instant watch of variable values. Hover over any variable while in break mode to see its current value.

## Exceptions

For most of the programs you have developed to this point, you have assumed nothing unusual would occur. Given perfect situations for running applications, your programs might perform beautifully. However, errors do occur. You can take several actions to keep your program from crashing. You can include `if` statements that check values used as input to ensure the value is numeric prior to parsing or converting the `string` value to its numeric equivalent. After `string` values are entered for console applications or retrieved from Windows controls, you can use the IsNumber() method of the `char` class to test each character in the `string`, as shown here.

```csharp
string aValue = "1334";
if (char.IsNumber(aValue[0])) // Tests the first character
```

Recall that one of the members of the `string` class is Length. Used with a `string` variable, the Length property returns the number of characters for that specific instance of the `string`. Length would return 4 for the aValue variable declared previously. You can use aValue.Length to create a loop that traverses through the `string` data, one character at a time, checking to see if each character making up the string is numeric.

You can also use `if` statements to test numeric values for valid ranges prior to using the number in arithmetic. You can use an `if` statement to test numeric values that will be used as divisors in arithmetic expressions to make sure the divisor is not zero prior to doing the division. You can also test subscript or index values used with arrays to make sure they are valid (that is nonnegative and one less than the dimensioned size). With Windows applications, an `if` statement can be included in your event-handling methods to test input controls, such as text boxes, for empty `string` input. You can also disable and make controls invisible by setting the Enable and Visible properties to `false` until valid entries are entered into other controls. When working with file applications, you can use `if` statements to make sure the file exists prior to attempting to retrieve values from the file. All of these suggestions can be incorporated into your solutions to reduce the likelihood of your program terminating abnormally. Some circumstances are beyond the control of the programmer, and unless provisions are made for handling exceptions, your program might crash or produce erroneous results. It is now time to take your programming skills to the next level and learn how to prevent abnormal terminations.

You have probably experienced unhandled exceptions being thrown while you browsed Web pages or during your development of C# programs. Were you ever asked if you wanted to debug some application while you were on the Internet? Have you seen a screen similar to Figure 12-9 while you were developing your C# applications in Visual Studio?
