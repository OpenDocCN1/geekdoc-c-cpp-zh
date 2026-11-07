![](bbox=[0.336, 0.118, 0.681, 0.189])

Value of account1’s balance data member displayed in red

**Fig. H.14** | Displaying the value of local variables.

valuable for experimenting with different values and for locating logic errors. In the Locals window, expand the account node and double click the Value field in the balance row to select the value 37. Type 33, then press Enter. The debugger changes the value of balance and displays its new value in red (Fig. H.15).

![](bbox=[0.336, 0.367, 0.681, 0.452])

Value modified in the Locals window

**Fig. H.15** | Modifying the value of a variable.

+   8. **Setting a breakpoint at at main’s closing brace.** Set a breakpoint at line 25 in the source code to prevent the program from closing immediately after displaying its result. If you do not set this breakpoint, you won’t be able to view the program’s output before the console window closes.

+   9. **Viewing the program result.** Select **Debug > Continue** to continue program execution. Function main executes until the return statement in line 29 and displays the result. Notice that the result is $33 (Fig. H.16). This shows that Step 7 changed the value of balance from the calculated value (37) to 33.

![](bbox=[0.257, 0.711, 0.743, 0.803])

**Fig. H.16** | Output displayed after modifying the account1 variable.

+   10. **Stopping the debugging session.** Select **Debug > Stop Debugging**. This will close the Command Prompt window. Remove all remaining breakpoints.

In this section, you learned how to use the debugger’s Watch and Locals windows to evaluate arithmetic and Boolean expressions. You also learned how to modify the value of a variable during your program’s execution.