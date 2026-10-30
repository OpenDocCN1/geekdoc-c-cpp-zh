# Tip

You can change all these colors and font characteristics in the Editor Format tab of the Options dialog box.

Removing a breakpoint involves nothing more than clicking the breakpoint indicator in the Margin Indicator bar. Breakpoints are also automatically removed when you close the application.

When execution reaches the breakpoint, Access halts execution and opens the module at the breakpoint (see Figure 27.9). You now use the Immediate window (see the preceding section) to examine the values of variables and perform other operations, or use any of the other debugging tools described in this section. Neither the code window nor the Immediate window is modal, so you still have full access to the development environment.

# FIGURE 27.9

Execution stops on the breakpoint.

![](bbox=[0.15, 0.55, 0.85, 0.85])

Figure 27.10 illustrates two techniques for viewing the values of variables while execution is stopped at a breakpoint. The Locals window contains the names and current values of all the variables in the current procedure. You open the Locals window by choosing Locals Window from the View menu. If you want to see the value of a variable in a slightly different format, use the Print command (?) in the Immediate window to display the variable's value.