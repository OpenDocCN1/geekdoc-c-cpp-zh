To manually break the execution of your program, you can use Break All from the Debug menu. This causes the debugger to stop the execution of all programs running under the debugger.

As the name implies, a breakpoint tells the debugger that your application should break execution at a certain point. When a breakpoint is set, the line is shown in red by default, and a solid red circle displays in the editor margin, as shown in Figure 16.10.

# **FIGURE 16.10**
An enabled breakpoint

![](bbox=[0.349, 0.248, 0.723, 0.284])

There are multiple ways to set a breakpoint. To set a breakpoint on an entire line, you can click the margin next to the line of code, place the mouse cursor over the line of code and use the Insert Breakpoint context menu option, or place the caret (the text cursor represented by the vertical bar) in the line of code and press the F9 key.

After a breakpoint has been set, your application will break at that location every time it is run under a debugger. When you no longer want the breakpoint set, you can remove it by clicking the breakpoint symbol in the margin. You can also place the mouse cursor over the line of code containing the breakpoint and use the Delete Breakpoint context menu option, or place the caret (the text cursor represented by the vertical bar) in the line of code and press the F9 key.

Sometimes, however, you only want to disable a breakpoint. To do this, you can right-click the breakpoint symbol in the margin or place the mouse cursor over the line of code containing the breakpoint, and use the Disable Breakpoint context menu option. You can also place the caret in the line of code and press the Ctrl+F9 keys. A disabled breakpoint, shown in Figure 16.11, is displayed with a red outlined circle in the editor margin and a red border around the line containing the breakpoint.

# **FIGURE 16.11**
A disabled breakpoint

![](bbox=[0.349, 0.658, 0.723, 0.694])

# *By the Way*

# **Visual Studio with MSDN Editions**

If you use one of the Visual Studio with MSDN editions, you have a few extra breakpoint capabilities not found in the Visual C# Express edition.

The most apparent one is the ability to create a tracepoint. A tracepoint is a breakpoint, which, by default, does not break program execution but instead performs a custom action. Tracepoints are most commonly used for printing messages when your program reaches a certain point.

In addition to tracepoints, you can also place restrictions on when a breakpoint will actually cause the debugger to break program execution by applying a