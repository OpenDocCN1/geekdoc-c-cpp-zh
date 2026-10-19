+   - Are all the declared variables being used?
+   - Are all variables bound at appropriate times—that is, are you striking a conscious balance between the flexibility of late binding and the increased complexity associated with late binding?
+   - Does each variable have one and only one purpose?
+   - Is each variable’s meaning explicit, with no hidden meanings?

# Key Points

+   - Data initialization is prone to errors, so use the initialization techniques described in this chapter to avoid the problems caused by unexpected initial values.
+   - Minimize the scope of each variable. Keep references to a variable close together. Keep it local to a routine or class. Avoid global data.
+   - Keep statements that work with the same variables as close together as possible.
+   - Early binding tends to limit flexibility but minimize complexity. Late binding tends to increase flexibility but at the price of increased complexity.
+   - Use each variable for one and only one purpose.