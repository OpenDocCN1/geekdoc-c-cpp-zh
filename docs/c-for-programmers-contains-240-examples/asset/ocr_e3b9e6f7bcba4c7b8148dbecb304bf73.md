# G.5 Autos Window

The *Autos window* displays the variables used in the previous statement executed (including the return value of a function, if there is one) and the variables in the next statement to execute.

+   1. *Setting breakpoints.* Set breakpoints at lines 14 and 22 in main by clicking in the margin indicator bar.
+   
+   2. *Using the Autos window.* Start the debugger by selecting **Debug > Start**. When the debugger enters break mode at line 14, open the *Autos* window (Fig. G.22) by selecting **Debug > Windows > Autos**. Since we are just beginning the program’s execution, the *Autos* window lists only the variables in the next statement that will execute—in this case, the account1 object, its value and its type. Viewing the values stored in an object lets you verify that your program is manipulating these variables correctly. Notice that account1 contains a large negative value. This value, which may be different each time the program executes, is account1’s uninitialized value. This unpredictable (and often undesirable) value demonstrates why it is important to initialize all C++ variables before they are used.
+   
+   3. *Using the Step Over command.* Select **Debug > Step Over** to execute line 14. The *Autos* window updates the value of account1’s balance data member (Fig. G.23) after it is initialized. The value of balance is displayed in red to indicate that it just changed.
+   
+   4. *Continuing execution.* Select **Debug > Continue** to execute the program until the second breakpoint at line 22. The *Autos* window displays uninitialized local variable withdrawalAmount (Fig. G.24), which has a large negative value.

![](bbox=[0.206, 0.576, 0.791, 0.644])

**Fig. G.22** | *Autos* window displaying the state of account1 object.

![](bbox=[0.206, 0.706, 0.791, 0.775])

**Fig. G.23** | *Autos* window displaying the state of account1 object after initialization.

![](bbox=[0.206, 0.836, 0.791, 0.905])

**Fig. G.24** | *Autos* window displaying local variable withdrawalAmount.