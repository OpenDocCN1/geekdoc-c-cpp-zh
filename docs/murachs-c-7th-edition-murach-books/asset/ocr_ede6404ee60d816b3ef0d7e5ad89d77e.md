expression tests if the value of a variable changes or if a variable is equal to a particular value, it will appear in the Condition column of the Breakpoints window. If the expression tests for the number of times the breakpoint is hit, it will appear in the Hit Count column of the Breakpoints window.

You can also select the Actions option in the Breakpoint Settings window to define a *tracepoint*. A tracepoint is a breakpoint that writes a message to the Output window. The message can include text as well as the values of variables and expressions. If you include a variable or expression, it must be enclosed in braces like this:

```
Future value: {futureValue}
```

# How to control the execution of an application

Once you’re in break mode, you can use a variety of commands to control the execution of the application. These commands are summarized in figure 11-5. Most of these commands are available from the Debug menu or the Debug toolbar, but a couple of them are available only from the shortcut menu for the Code Editor. You can also use shortcut keys to execute some of these commands.

To *step through* an application one statement at a time, you use the Step Into command. Then, the application enters break mode before each statement is executed. If a statement calls another method, the Step Into command causes the application to execute each statement of the called method. The Step Over command works similarly except that the statements in called methods are executed without interruption (they are “stepped over”).

Although you can use either of these commands to start application execution or to restart execution from break mode, you’re most likely to use them from break mode. That’s because if you use them to start execution of a typical form class, you first step through some of the code that’s been generated for the form.

If you use the Step Into command to enter a method, you can use the Step Out command to execute the remaining statements in the method without interruption. After that, the application enters break mode before the next statement in the calling method is executed.

To skip code that you know is working properly, you can use the Run To Cursor or Set Next Statement command. You can also use the Set Next Statement command to rerun lines of code that were executed before an exception occurred. And if the next statement to be executed is no longer displayed in the Code Editor, you can use the Show Next Statement command to move to it.

If you’re using Visual Studio 2017 or later, you can also use the *Run to Click feature* to control the execution of an application. To use this feature, you point to a line of code in the Code Editor and then click the icon that appears to the left of the line. When you do, the application is executed up to that line. This eliminates the need to add a breakpoint on the line.

Although it’s not shown in the last figure, you should know that when you step through code using the commands in this figure, Visual Studio displays the number of milliseconds that it took to execute the code up to that point. This is called a *PerfTip* (or performance tip). Although you won’t typically need this information, it can be helpful in identifying inefficient code.