execution of a **switch** statement. Note that in the figure following a case value, the box containing **statement** and/or the box containing **break** may or may not appear. Following the figure, we give the general rules that a **switch** statement follows.

![](bbox=[0.183, 0.158, 0.91, 0.7])

**FIGURE 4-4**  *switch statement*

The **switch** statement executes according to the following rules:

+   1. When the value of the **expression** is matched against a case value (also called a label), the statements execute until either a **break** statement is found or the end of the **switch** structure is reached.
+   2. If the value of the **expression** does not match any of the case values, the statements following the **default** label execute. If the **switch** structure has no **default** label and if the value of the **expression** does not match any of the case values, the action of the **switch** statement is null.
+   3. A **break** statement causes an immediate *exit* from the **switch** structure.