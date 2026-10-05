
Edition includes the most important debugging features presented in this chapter. In addition, if a debugging feature isn't available from the Express Edition, or if it works a little differently than the other editions, we have noted that in the figures of this chapter.

## How to control the execution of an application

Once you're in break mode, you can use a variety of commands to control the execution of the application. These commands are summarized in figure 11-5. Most of these commands are available from the Debug menu or the Debug toolbar, but a couple of them are available only from the shortcut menu for the Code Editor. You can also use shortcut keys to execute some of these commands.

To step through one statement at a time, you can use the Step Into command. Then, the application enters break mode before each statement is executed so you can test the values of properties and variables and perform other debugging functions. If a statement calls another method, the Step Into commands to execute each statement of the called method. The Step Over command works similarly except that the statements in called methods are executed without interruption (they are “stepped over”).

You can use either of these commands to start application execution or to restart execution when an application is in break mode. If you use them to start the execution of a typical form class, though, you first step through some of the code that has been generated for the form. As a result, you normally use these commands after a breakpoint has been reached.

If you use the Step Into command to enter a method, you can use the Step Out command to execute the remaining statements in the method without interruption. After that, the application enters break mode before the next statement in the calling method is executed.

To skip code that you are working properly, you can use the Run To Cursor or Set Next Statement command. You can also use the Set Next statement command to rerun lines of code that were executed before an exception occurred. And if you've been working in the Code Editor and have forgotten the next statement to be executed is, you can use the Show Next statement command to move to it.

## Commands in the Debug menu and toolbar

| Command | Toolbar | Keyboard | Description |
|---|---|---|---|
| Start/Continue | ▷ | F5 | Start or continue execution of the application. |
| Break All | ⏸ | Ctrl+Alt+Break | Suspend execution of the application. |
| Stop Debugging | ⬛ | Shift+F5 | Stop debugging and end execution of the application. |
| Restart | ↻ | Ctrl+Shift+F5 | Restart the entire application. |
| Show Next Statement | ↷ | | Display the next statement to be executed. Also available from the shortcut menu for the Code Editor. |
| Step Into | ⬇ | F11 | Execute one statement at a time. |
| Step Over | ↷ | F10 | Execute one statement at a time except for called methods. |
| Step Out | ⇧ | Shift+F11 | Execute the remaining lines in the current method. |

## Commands in the Code Editor's shortcut menu

| Command | Description |
|---|---|
| Run to Cursor | Execute the application until it reaches the statement that contains the insertion point. |
| Set Next Statement | Set the statement that contains the insertion point as the next statement to be executed. |

## Description

- If you use the Step Into or Step Over mode before to start the execution of an application, Visual Studio will enter break mode before it executes the first statement in the application. If you use the Run to Cursor command, Visual Studio will enter break mode when it reaches the statement that contains the insertion point.
- Once the application enters break mode, you can use the Step Into, Step Over, Step Out, and Run To Cursor command to execute one or more statements.
- To alter the normal execution sequence of the application, you can use the Set Next Statement command. Just place the insertion point in the statement you want to execute next, issue this command, and click on the Continue button.
- To enter break mode when you need to stop the execution of an application, you can use the Break All command.

![](img/3148667e42d4db35b3d08576aaa1fa01_350_0.png)

## How to use the debugging windows

Now that you know how to work with break mode, you're ready to learn how to use the primary debugging windows. These windows include the Locals window, the Autos window, the Watch windows, the Immediate window, the Call Stack window, the Call Hierarchy window, and the Output window.

### How to use the Locals window
to monitor variables

If you need to see the values of several variables used in the same area of an application, you can do that using the Locals window as shown in figure 11-6. By default, this window is displayed in the group of variables in the lower left corner of Visual Studio when an application enters break mode. If it isn't, you can display it by selecting the Locals command from the Windows submenu of Debug menu.

The Locals window displays information about the variables that are in the current scope. In this figure, for example, the Locals window shows the five variables that are in the scope of the for loop in the CalculateFuture method. In addition, it shows the keyword that includes information about the current form.

Whenever a variable contains other variables, the Locals window displays a sign (+) to the left of the variable. To drill down through this information, you can click the plus to expand the entry. In this figure, for example, you can click the plus to the left of this keyword to view information about the current form. That includes information about all of the properties for the form and all of the properties for each control.

Besides displaying the values of variables, you can use the Locals window to change these. To do that, you double-click on the value and enter a new value.

### How to use the Autos window
to monitor variables

If you want to limit the number of variables displayed, you can use the Autos window instead of the Locals window. This window works similarly to the Locals window, except it only displays information about the current statement and the previous statement. To display this window, you can select the Autos command from the Windows submenu of Debug menu. However, this window isn't available from the Express Edition.

Figure 11-6 to use the Locals and Autos windows to monitor variables

### How to use Watch windows to monitor expressions

By default, the Watch windows are located in the group of windows in the lower left corner of Visual Studio when an application enters break mode, as shown in 11-7. You can use these windows to view the values of watch expressions that you enter into these windows. These expressions are automatically updated as the application is executed.

If the Watch 1 isn't available when an application enters break mode, you can display it by pulling down the Debug menu, selecting the Windows submenu, selecting the Watch submenu, and selecting the Watch 1 item. You can also display any of the other three watch windows by selecting the appropriate item from this submenu. These windows provide the same features as the Watch 1. You can use them if you want to separate the watch expressions into groups.

To add a watch expression, you click in the Name column of an empty row and enter the expression. A watch expression can be any expression that's recognized by the debugger. If the expression exists in the application, you can also select it in the Code Editor and drag it to the Watch window. The Watch window in this figure shows two expressions that are recognized by the debugger, the futureValue variable and the Text property of the Future text box.

If the expression you add to the Watch window is the name of an object, the Watch window will display a plus sign to the left of the name. Then, you can click on the plus sign to display the properties of the object. A plus sign is also added to an expression if it's the name of an array.

You can change the value of a watch expression by double-clicking on the value in the Value column and entering the new value. To delete a watch expression, you can use the Delete Watch command on the shortcut menu that's displayed when you right-click on an expression. To delete all expressions, you can use the Select All command on the shortcut menu followed by the Delete Watch command.
