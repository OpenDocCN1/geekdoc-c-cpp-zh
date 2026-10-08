
- Immediate window
- Breakpoints
- Execution control

## Variable Windows

  Variable windows display the name, value, and data type of variables while you debug. Although seeing the current value of a variable is helpful when you debug, modifying the value of a variable is even more helpful. Fortunately, the variable windows enable you to do just that. By double-clicking in the value column, or using the Edit Value context menu, you can edit the value of that variable. When a value has been modified, it appears in red, as shown in Figure 16.4.

  Visual C# Express provides two variable windows: the Locals window and the Watch window. These windows appear below the code editor while you debug and can be accessed using the Debug Windows menu.

## Visual Studio with MSDN Editions

  If you are using one of the Visual Studio with MSDN editions, you have a few extra capabilities not found in the Visual C# Express edition. In addition to the Locals and Watch windows, you also have an Autos window, which displays variables used in the current and preceding line of code. Like the Locals window, the debugger also automatically populates the Autos window. Although the Watch window allows you to examine many variables or expressions, the Quick Watch dialog enables you to examine a single variable or expression at a time and is useful for quickly seeing a single value or large data structure. You also have multiple Watch windows, four of them actually, instead of just one.

  The Locals window, shown in Figure 16.5, displays all the local variables that are currently in scope.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_373_0.png)

### FIGURE 16.5
Locals window

  The Watch window enables you to enter expressions directly. The simplest expression you can enter is a variable name; however, the debugger accepts most valid language expressions. The expression evaluator does not accept lambdas or LINQ query syntax expressions. To evaluate an expression in the Watch window, you can do the following:

- 1. Click on the Name column in an empty row and enter the variable name or expression.
- 2. Drag a variable or expression from the code editor to an empty row.
- 3. Use the Add Watch context menu from the selected expression.

## Expressions with Side Effects

  Expressions that change data are said to have side effects. When you enter such an expression into the watch window, the side effect occurs each time the expression is evaluated by the Watch window. If you are not aware that the expression has side effects, this can lead to unexpected results.

  When an expression is known to have side effects, it is evaluated only the first time you enter it. Subsequent evaluations are disabled; however, you can override this behavior by clicking the update icon (which resembles two green arrows circling in opposite directions within a green circle) that appears next to the value.

  The debugger automatically calls property get accessors to display results, so properties with side effects can cause unwanted behavior during debugging. In fact, the debugger assumes that property getters follow the best practices, which means they are as follows:

- 1. Fast
- 2. Side-effect free
- 3. Never throw exceptions

> Watch Out! GO TO Hour 21, “Dynamic Types and Language Interoperability,” for more information on dynamic types.

  When an expression has been added to the watch window, it remains there until you remove it. If the expression is no longer in scope, it displays in a disabled state.

  When the Watch window displays a dynamic object, a special “Dynamic View” node is added that shows the members of the dynamic object but does not enable editing the values.

## Using DataTips

  You can also view the current value using a DataTip, which is one of the more convenient ways for viewing information about variables and objects in your program while you are debugging. By placing the mouse pointer over the variable in a source editor while you debug, the DataTip displays, as shown in Figure 16.6. Just as you can in the Locals window, you can edit the value by clicking on the DataTip.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_374_0.png)

  By default, DataTips are transient and disappear when you move the mouse cursor away from the variable. DataTips can also be pinned, as shown in Figure 16.7, to a specific location in the source file by clicking the Pin to source icon (the pushpin on the right side of the DataTip).

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_374_1.png)

  Although DataTips are visible only during a debugging session, pinned DataTips display a pushpin icon in the margin of the editor that you can place the mouse cursor over to view the value from the last debugging session, as shown in Figure 16.8.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_374_2.png)

  By clicking the “Unpin from source” icon, you can float the DataTip above any open windows. A pinned or floating DataTip will be visible in the same location for any subsequent debugging sessions, including after restarting Visual Studio.

## Sharing DataTips

  You can also export DataTips to an XML file to share with other developers working on the same project.

  To export DataTips, click Export DataTips on the Debug menu, navigate to the location where you want to save the XML file, provide a name for the file, and click OK. To import DataTips, click Import DataTips on the Debug menu and select the appropriate XML file.

## Did you know?

### Using the Immediate Window

  The Immediate window enables you to evaluate expressions, execute statements, print variable values, and many other actions. The Immediate window also supports specific Visual Studio commands in addition to allowing you to execute language statements.

  For example, to display the value of the divisor variable at the time the exception occurred, you could enter the following statements in the Immediate window:

```text
>Debug.Print divisor
>? divisor
? divisor
divisor
```

  The result of each of these commands is shown in Figure 16.9. You can use the Up and Down arrow keys to cycle through previously entered commands.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_375_0.png)

### FIGURE 16.9
Immediate window

### Understanding Breakpoints

  When debugging an application using the Visual Studio debugger, your application is either executing (running) or in break mode. Break mode occurs when the debugger breaks the program execution as the result of an exception, a user-defined breakpoint, or manually breaking the execution. Most of the debugger features are available only when your application is in break mode.

  To manually break the execution of your program, you can use Break All from the Debug menu. This causes the debugger to stop the execution of all programs running under the debugger.

  As the name implies, a breakpoint tells the debugger that your application should break execution at a certain point. When a breakpoint is set, the line is shown in red by default, and a solid red circle displays in the editor margin, as shown in Figure 16.10.

## FIGURE 16.10
An enabled breakpoint

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_376_0.png)

  There are multiple ways to set a breakpoint. To set a breakpoint on an entire line, you can click the margin next to the line of code, place the mouse cursor over the line of code and use the Insert Breakpoint context menu option, or place the caret (the text cursor represented by the vertical bar) in the line of code and press the F9 key.

  After a breakpoint has been set, your application will break at that location every time it is run under a debugger. When you no longer want the breakpoint set, you can remove it by clicking the breakpoint symbol in the margin. You can also place the mouse cursor over the line of code containing the breakpoint and use the Delete Breakpoint context menu option, or place the caret (the text cursor represented by the vertical bar) in the line of code and press the F9 key.

  Sometimes, however, you only want to disable a breakpoint. To do this, you can right-click the breakpoint symbol in the margin or place the mouse cursor over the line of code containing the breakpoint, and use the Disable Breakpoint context menu option. You can also place the caret in the line of code and press the Ctrl+F9 keys. A disabled breakpoint, shown in Figure 16.11, is displayed with a red outlined circle in the editor margin and a red border around the line containing the breakpoint.

## FIGURE 16.11
A disabled breakpoint

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_376_1.png)

*By the Way*

## Visual Studio with MSDN Editions

  If you use one of the Visual Studio with MSDN editions, you have a few extra breakpoint capabilities not found in the Visual C# Express edition.

  The most apparent one is the ability to create a tracepoint. A tracepoint is a breakpoint, which, by default, does not break program execution but instead performs a custom action. Tracepoints are most commonly used for printing messages when your program reaches a certain point.

  In addition to tracepoints, you can also place restrictions on when a breakpoint will actually cause the debugger to break program execution by applying a
