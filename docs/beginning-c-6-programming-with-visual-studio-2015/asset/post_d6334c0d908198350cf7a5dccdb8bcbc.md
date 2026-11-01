
Again, the debug version is only compiled into debug builds.

These functions take three parameters. The first is a Boolean value, whereby a value of false causes the assertion to trigger. The second and third are string parameters to write information both to a pop-up dialog box and the Output window. The preceding example would need a function call such as the following:

```
Debug.Assert(myVar < 10, "myVar is 10 or greater.",
    "Assertion occurred in Main().");
```

Assertions are often useful in the early stages of user adoption of an application. You can distribute release builds of your application containing Trace.Assert() functions to keep tabs on things. Should an assertion be triggered, the user will be informed, and this information can be passed on to you. You can then determine what has gone wrong even if you don't know how it went wrong.

You might, for example, provide a brief description of the error in the first string, with instructions as to what to do next as the second string:

```
Trace.Assert(myVar < 10, "Variable out of bounds.",
    "Please contact vendor with the error code KCW001.");
```

Should this assertion occur, the user will see the dialog box shown in Figure 7-9.

Admittedly, this isn't the most user-friendly dialog box in the world, as it contains a lot of information that could confuse users, but if they send you a screenshot of the error, it could quickly track down the problem.

![](img/cf72ea860016d2d680fc085fc06f265a_174_0.png)

FIGURE 7-9

Now it's time to look at what you can actually do after application execution is halted and you are in break mode. In general, you enter break mode to find an error in your code (or to reassure yourself that things are working properly). Once you are in break mode, you can use various techniques, all of which enable you to analyze your code and the exact state of the application at the point in its execution where it is paused.

## Monitoring Variable Content

Monitoring variable content is just one example of how Visual Studio helps you a great deal by simplifying things. The easiest way to check the value of a variable is to hover the mouse over its name in the source code while in break mode. A tooltip showing information about the variable appears, including the variable's current value.

You can also highlight entire expressions to get information about their results in the same way. For more complex values, such as arrays, you can even expand values in the tooltip to see individual element entries.

It is possible to pin these tooltip windows to the code view, which can be useful if there is a variable you are particularly interested in. Pinned tooltips persist, so they are available even if you stop and restart debugging. You can also add comments to pinned tooltips, move them around, and see the value of the last variable value, even when the application isn't running.

You may have noticed that when you run an application, the layout of the various windows in the IDE changes. By default, the following changes are likely to occur at runtime (this behavior may vary slightly depending on your installation):

- The Properties window disappears, along with some other windows, probably including the Solution Explorer window.
- The Error List window is replaced with two new windows across the bottom of the IDE window.
- Several new tabs appear in the new windows.

The new screen layout is shown in Figure 7-10. This may not match your display exactly, and some of the tabs and windows may not look exactly the same, but the functionality of these windows as described later will be the same, and this display is customizable via the View and Debug Windows menus (during break mode), as well as by dragging windows around the screen to reposition them.

The new window that appears in the bottom-left corner is particularly useful for debugging. It enables you to keep tabs on the values of variables in your application when in break mode:

- Autos — Variables in use in the current and previous statements (Ctrl+D, A)
- Locals — All variables in scope (Ctrl+D, L)
- Watch N — Customizable variable and expression display (where N is 1 to 4, found on Debug Windows Watch)

All these tabs work in more or less the same way, with various additional features depending on their specific function. In general, each tab contains a list of variables, with information on each variable's name, value, and type. More complex variables, such as arrays, may be further examined using the + and - tree expansion/contraction symbols to the left of their names, enabling a tree view of their content. For example, Figure 7-11 shows the Locals tab obtained by placing a breakpoint in the example code. It shows the expanded view for one of the array variables, maxValIndices.

The sixth, seventh, and eighth icons control program flow in break mode. In order, they are as follows:

- **Step Into** — Execute and move to the next statement to execute.
- **Step Over** — Similar to Step Into, but won't enter nested blocks of code, including functions.
- **Step Out** — Run to the end of the code block and resume break mode at the statement that follows.

To look at every single operation carried out by the application, you can use Step Into to follow the instructions sequentially. This includes moving inside functions, such as Maxima() in the preceding example. Clicking this icon when the cursor reaches line 17, which is the call to Maxima(), results in the cursor moving to the first line inside the Maxima() function. Alternatively, clicking Step Over when you reach line 17 moves the cursor straight to line 18, without going through the code in Maxima() (although this code is still executed). If you do step into a function that you aren't interested in, you can click Step Out to return to the code that called the function. As you step through code, the values of variables are likely to change. If you keep an eye on the monitoring windows just discussed, you can clearly see this happening.

You can also change which line of code will be executed next by right-clicking on a line of code and selecting Set Next Statement, or by dragging the yellow arrow to a different line of code. This doesn't always work, such as when skipping variable initialization. However, it can be very useful for skipping problematic lines of code to see what will happen, or for repeating the execution of code by moving the arrow backward.

In code that has semantic errors, these techniques may be the most useful ones at your disposal. You can step through code right up to the point where you expect problems to occur, and the errors will be generated as if you were running the program normally. Or you can cause statements to be executed more than once by changing the executing code. Along the way, you can watch the data to see just what is going wrong. Later in this chapter, you'll step through some code to find out what is happening in an example application.

## Immediate and Command Windows

The Command and Immediate windows (found on the Debug Windows menu) enable you to execute commands while an application is running. The Command window enables you to perform Visual Studio operations manually (such as menu and toolbar operations), and the Immediate window enables you to execute additional code besides the source code lines being executed, and to evaluate expressions.

These windows are intrinsically linked. You can even switch between them by entering commands — immed to move from the Command window to the Immediate window and cmd to move back.

This section concentrates on the Immediate window because the Command window is only really useful for complex operations. The simplest use of this window is to evaluate expressions, a bit like a one-shot use of the Watch windows. To do this, type an expression and press Return. The information requested will then be displayed. An example is shown in Figure 7-15.

![](img/cf72ea860016d2d680fc085fc06f265a_179_0.png)

FIGURE 7-15

You can also change variable content here, as demonstrated in Figure 7-16.

![](img/cf72ea860016d2d680fc085fc06f265a_179_1.png)

FIGURE 7-16

In most cases, you can get the effects you want more easily using the variable monitoring windows shown earlier, but this technique is still handy for tweaking values, and it's good for testing expressions.

## The Call Stack Window

The final window to look at is the Call Stack window, which shows you the way in which the program reached the current location. In simple terms, this means showing the current function along with the function that called it, the function that called that, and so on (that is, a list of nested function calls). The exact points where calls are made are also recorded.

In the earlier example, entering break mode when in Maxima(), or moving into this function using code stepping, reveals the information shown in Figure 7-17.

![](img/cf72ea860016d2d680fc085fc06f265a_179_2.png)

FIGURE 7-17

If you double-click an entry, you are taken to the appropriate location, enabling you to track the way code execution has reached the current point. This window is particularly useful when errors are first detected, because you can see what happened immediately before the error. Where errors occur in commonly used functions, this helps you determine the source of the error.
