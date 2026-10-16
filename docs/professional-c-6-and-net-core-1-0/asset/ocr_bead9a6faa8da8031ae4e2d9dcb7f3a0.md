currently being executed.

+   - **Watch**—Monitors any variables that you have explicitly specified typing their names into the Watch window. You can drag and drop variables to the Watch window.

These windows are only visible when the program is running under th debugger. If you do not see them, select Debug ↩ Windows, and then select the desired menu. The Watch window offers four different windows in case there’s so much to watch and you want to group that With all these windows you can both watch and change the values, enabling you to try different paths in the program without leaving the debugger. The Locals window is shown in Figure 17.42.

![](bbox=[0.105, 0.284, 0.895, 0.48])

# Figure 17.42

Another window that doesn’t directly relate to the other windows discussed but is still an important one for monitoring and changing variables is the *Immediate window*. This window also makes it possib for you to look at variable values. You can use this window to enter co and run it. This is very helpful when you’re doing some tests during a debug session; it enables you to home in on details, try a method out, and change a debug run dynamically.

# Exceptions

Exceptions are great when you are ready to ship your application, ensuring that error conditions are handled appropriately. Used well, they can ensure that users are never presented with technical or annoying dialogs. Unfortunately, exceptions are not so great when you are trying to debug your application. The problem is twofold:

+   - If an exception occurs when you are debugging, you often do not want it to be handled automatically—especially if automatically handling it means retiring gracefully and terminating execution! Rather, you want the debugger to help you determine why the exception has occurred. Of course, if you have written good, robus defensive code, your program automatically handles almost anything—including the bugs that you want to detect!

+   - If an exception for which you have not written a handler occurs, th