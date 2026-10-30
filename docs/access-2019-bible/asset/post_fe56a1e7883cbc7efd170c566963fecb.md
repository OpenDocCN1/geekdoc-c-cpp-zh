
## FIGURE 27.10

Variables are in scope when in break mode.

Using ? to display a variable's value

Immediate window

Locals window

![](img/1e45673ab6eca9d20e67635ff5b9b318_926_0.png)

Current position indicator arrow

Code at breakpoint

## Using Stop Statements Instead of Setting Breakpoints

An alternative to setting breakpoints is to use Stop statements. The Stop statement halts execution but is more permanent than a breakpoint. A Stop statement, like any other VBA statement, persists from session to session until explicitly removed. You can, however, surround the Stop statement with conditional compilation expressions and toggle their action by changing the value assigned to a conditional compilation constant. The following figure illustrates using the Stop statement.

Using Stop is a bit dangerous, however. Because Stop is an executable statement, unless it's carefully controlled with compiler directives, deleted, or commented out, your application will, literally, stop executing in front of a user. You're probably better off using regular breakpoints than Stop statements in most situations.

Continues

![](img/1e45673ab6eca9d20e67635ff5b9b318_927_0.png)

The most fundamental operation at a breakpoint is to walk through the code, one statement at a time, enabling you to view what’s happening to the application’s logic and variables. After you’ve reached a breakpoint, you use a few keystroke combinations to control the execution of the application. You’re able to step through code one statement at a time, automatically walk through the local procedure, or step over the procedure and continue execution on the "other side" of the procedure.

In Figure 27.11, a breakpoint has been inserted near the top of the UsingBreakpoints() subroutine. When execution reaches this statement a breakpoint asserts itself, allowing you to take control of program execution.

In Figure 27.12, the break has occurred, and we’ve clicked the Step Into button (or pressed F8). The Step Into button executes the current statement and moves to the next statement in the program’s flow of execution. In this case, the db variable is set, and the current line becomes the statement that sets the sSQL variable (indicated by a yellow highlight and an arrow in the left margin). At this point, the sSQL assignment statement has not been executed, and the value of sSQL is an empty string. Press F8 again to execute the sSQL assignment statement and move the current line to the next line. After sSQL is set, you can see the value of sSQL in the Immediate window by using ?sSQL or by opening the Locals window (described in the "Looking at variables with the Locals window" section, later in this chapter).

## Chapter 27: Debugging Your Access Applications

## FIGURE 27.11

Insert a breakpoint near the location of the code you want to step through.

![](img/1e45673ab6eca9d20e67635ff5b9b318_928_0.png)

## FIGURE 27.12

Step Into executes one line at a time.

![](img/1e45673ab6eca9d20e67635ff5b9b318_928_1.png)

Consecutive clicks on the Step Into button (or pressing F8) executes the code one statement at a time. If a statement includes a call to a child procedure, you'll be taken to that procedure, and each of its lines will execute one at a time. If you want, you can use the Step Over button (or press Shift+F8) to execute all the code in the child routine (not one line at a time) but continue in the calling procedure one line at a time. If you've previously debugged the child routine and you're sure it contains no errors, there is no reason to walk through its code. The code in the called routine is actually executed when you click the Step Over button, changing any variables involved.

When you're satisfied that you don't need to continue walking through the code in the child procedure, click the Step Out button (or press Ctrl+F8) to complete the procedure. The Step Out button is handy if you've stepped into a called routine and you're sure there's nothing interesting going on in it.

One very nice feature in the Access VBA window is the Auto Data Tips option in the Editor tab in the Options dialog box (see Chapter 25 for more on VBE Options). With this option selected, you're able to view the value of any variable in a ScreenTip-like window by hovering the mouse pointer over the variable's name in the module window (see Figure 27.13).

## FIGURE 27.13

Auto Data Tips are a powerful tool for debugging.

![](img/1e45673ab6eca9d20e67635ff5b9b318_929_0.png)

The Auto Data Tips display you see by hovering the mouse over a variable is very dynamic. The value shown in Auto Data Tips changes whenever the variable is assigned a new value. Because hovering the mouse is easy to do, you don’t have to use the Immediate window to view every variable in your code. You can hover over any variable in the procedure, not just on the current line. In Figure 27.13, the mouse is over the sSql variable in the line with the execution pointer (the first argument of OpenRecordset).

> NOTE
> The Auto Data Tips option must be selected in the Editor tab in order for the data tip you see in Figure 27.13 to appear.

> TIP
> Figure 27.13 shows an Auto Data Tip for a variable with a very long string. You can’t see the whole value using this method. You can, however, see the last part of the screen by holding down the Ctrl key while you hover over a variable.

One very nice feature of breakpoints is that the execution pointer (the yellow arrow in the left margin) is movable. You can use the mouse to reposition the pointer to another statement within the current procedure. For example, you can drag the pointer to a position above its current location to re-execute several lines of code.

You can easily reposition the execution pointer in such a way that your code’s execution is invalid, such as moving it into the body of an If...Then...Else statement, or into the middle of a loop. Also, moving the pointer to a position lower in the code may mean that variables aren’t set correctly or an important bit of code is ignored. Overall, though, the ability to easily re-execute a few lines of code is a valuable debugging aid.

## Looking at variables with the Locals window

The Locals window (View ⇨ Locals Window) shows all variables that are currently in scope, saving you from having to examine each variable one at a time. The variable’s name, its data type, and its current value are displayed.

Notice the items in the Locals window in Figure 27.14. Any line in the Locals window that begins with a plus sign will unfold to reveal more information. For example, you can set a breakpoint on the rs.Close statement near the bottom of the UsingBreakpoints procedure to halt execution so that you can examine the results of the rs assignment statement. Unfolding the rs entry in the Locals window reveals all the properties of the rs object and its contents (see Figure 27.14).

## FIGURE 27.14

Use the Locals window to examine the values of complex objects.

![](img/1e45673ab6eca9d20e67635ff5b9b318_931_0.png)

One powerful feature of the Locals window is that you can set the values of simple variables (numeric, string, and so on) by clicking the Value column in a variable's row and typing in a new value for the variable. This makes it very easy to test how various combinations of variable values affect your application.

In the preceding section, we tell you how to move the execution point within a procedure by dragging the yellow arrow with the mouse. By changing the value of a variable and moving the execution point to different places in the procedure, you can verify that the code executes as expected. Directly manipulating variables is much easier than other methods of testing the effect of outliers and unexpected values.

# NOTE

The Locals window shows only module-level variables under the name of the module. Globally scoped variables are not shown in the Locals window. You have to use the Immediate window or the Auto Data Tips to inspect global variables.
