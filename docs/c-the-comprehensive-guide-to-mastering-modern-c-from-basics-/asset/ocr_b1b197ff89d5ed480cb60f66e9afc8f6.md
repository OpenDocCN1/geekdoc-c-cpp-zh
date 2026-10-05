parameter also ends up on the stack. For example, the computer copies the x from func(x) onto the stack. The copy is then called arg within func—as seen in line 4 of the stack. Conversely, the return value of the function remains as the only value on the stack for the return (Line 6), to end up in ival for the assignment.

The gray-shaded part of the stack also indicates that func only has access to its own section of the stack: ival and x are not visible within the function. What is shown here for the int built-in type also applies to more complex data types such as standard containers and custom classes.

# Multifunctional Stack

However, the stack not only contains variables, parameters, and return values. For example, the system also stores where it needs to return when it jumps to a function.

Due to some programming errors, it can happen that you write beyond the boundaries of a variable—and that means you overwrite your neighbors. While it is at least annoying if you corrupt neighboring variable values, it is deadly if you overwrite a return address. If that happens, the program will very likely crash at the next opportunity.

Or—even worse—your program becomes the target of a hacker attack and jumps into a function of a computer virus instead of its own function. It is a popular attack method to exploit programming errors