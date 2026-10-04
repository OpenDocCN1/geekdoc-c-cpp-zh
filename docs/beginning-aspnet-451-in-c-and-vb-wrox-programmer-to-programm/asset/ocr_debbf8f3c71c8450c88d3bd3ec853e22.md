In this exercise you also learned how to use data tips, the small tooltip windows that appear when you hover your mouse over selected variables. For simple types, such as an Integer or a string, all you see is the variable's value. For complex types, such as results returned from a LINQ query, you get a much richer data tip, providing you with a lot more detail.

Useful as the debugging tips may seem, they are only a small part of the rich debugging features. In the next section, you get an overview of all the debugging tools that ship with VS.

# TOOLS SUPPORT FOR DEBUGGING

With a number of shortcut keys and menu items, VS lets you move around the code that you are debugging, giving you the option to execute code by line or larger blocks of code at once. Additionally, the IDE provides you with a lot of windows that enable you to diagnose and change the execution environment, including the values of variables at run time. See how to move around code first, which is followed by a discussion on the numerous debugging windows.

# Moving Around in Debugged Code

When your code has halted at a breakpoint, you can use a number of keyboard shortcuts to determine what to do next. The following table lists the most common shortcuts.

| KEY | DESCRIPTION |
| F5 | Press this key to start debugging, as demonstrated in the previous exercise. When you press this key during debugging, the code continues until the next breakpoint is hit, or until all code is executing. |
| F11 | Press this key to execute the current line and step into a member's being called, if possible. You see how this works later. |
| F10 | Press this key to execute the current line without stepping into the code that is being called, unless that code itself contains a breakpoint. |
| Shift+F11 | Press this key combination to complete the code in the current code block and return to the code that initially called it. |
| Shift+F5 | Press this key combination to stop debugging. |
| Ctrl+Shift+F5 | Press this key to restart the debugging process. |

In addition to these keyboard shortcuts, you can also use the Debugging toolbar shown in Figure 18-10, which offers similar functionality.

This toolbar should appear automatically when you start debugging, but if it doesn't, right-click an existing toolbar and choose Debug. To start debugging using the toolbar, press the button with the green arrow on the Standard toolbar.

![](bbox=[0.588, 0.796, 0.882, 0.943])