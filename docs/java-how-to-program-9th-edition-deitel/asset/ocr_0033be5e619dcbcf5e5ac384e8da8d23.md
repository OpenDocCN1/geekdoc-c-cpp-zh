# # F.7 Wrap-Up

application's for statement is working properly, so you want to remove the break- point at line 22 and allow the remaining iterations of the loop to proceed normal- ly. You can remove the breakpoint at line 22 by typing clear Interest:22. Now type clear to list the remaining breakpoints in the application. The debugger should indicate that only the breakpoint at line 13 remains (Fig. F.31). This breakpoint has already been reached and thus will no longer affect execution.

![](bbox=[0.12, 0.32, 0.88, 0.48])

Fig. F.31 | Removing the breakpoint at line 22.

8. Continuing execution after removing a breakpoint. Type cont to continue execution. Recall that execution last paused before the print statement in line 22. If the breakpoint at line 22 was removed successfully, continuing the application will produce the correct output for the current and remaining iterations of the for statement without the application halting (Fig. F.32).

![](bbox=[0.12, 0.74, 0.88, 0.9])

Fig. F.32 | Application executes without a breakpoint at line 22.

In this appendix, you learned how to insert and remove breakpoints in the debugger. Breakpoints allow you to pause application execution so you can examine variable values with the debugger's print command. This capability will help you locate and fix logic errors in your applications. You saw how to use the print command to examine the value of an expression and how to use the set command to change the value of a variable. You also learned debugger commands (including the step, step up and next commands) that can be used to determine whether a method is executing correctly. You learned how to use the watch command to keep track of a field throughout the life of an application. Finally, you learned how to use the clear command to list all the breakpoints set for an application or remove individual breakpoints to continue execution without breakpoints.