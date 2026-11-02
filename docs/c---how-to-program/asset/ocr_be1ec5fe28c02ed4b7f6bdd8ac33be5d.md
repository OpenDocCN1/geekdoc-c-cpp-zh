+   - The **getchar function** (from the standard input/output library) reads and returns as an int one character from the keyboard.
+   - Characters are normally stored in variables of type **char** (p. 157). Characters can be stored in any integer data type because they're usually represented as one-byte integers in the computer. Thus, we can treat a character as either an integer or a character, depending on its use.
+   - Many computers today use the **ASCII (American Standard Code for Information Interchange;** p. 158) character set in which 97 represents the lowercase letter 'a'.
+   - Characters can be read with **scanf** by using the conversion specifier `%c`.
+   - **Assignment expressions** as a whole actually have a value. This value is assigned to the variable on the left side of the `=`.
+   - The fact that assignment statements have values can be useful for setting several variables to the same value, as in `a = b = c = 0;`.
+   - **EOF** is often used as a sentinel value. EOF is a symbolic integer constant defined in `<stdio.h>`.
+   - On Linux/UNIX systems and many others, the EOF indicator is entered by typing `<Ctrl>d`. On other systems, such as Microsoft Windows, the EOF indicator can be entered by typing `<Ctrl>z`.
+   - Keyword **switch** is followed by the **controlling expression** (p. 159) in parentheses. The value of this expression is compared with each of the case labels. If a match occurs, the statements for that case execute. If no match occurs, the default case executes.
+   - The **break statement** causes program control to continue with the statement after the switch. The break statement prevents the cases in a switch statement from running together.
+   - Each case can have one or more actions. The switch statement is different from all other control statements in that braces are not required around multiple actions in a case of a switch.
+   - Listing several case labels together simply means that the same set of actions is to occur for any of these cases.
+   - Remember that the switch statement can be used only for testing a **constant integral expression** (p. 161)—i.e., any combination of character constants and integer constants that evaluates to a constant integer value. A character constant can be represented as the specific character in single quotes, such as 'A'. Characters must be enclosed within single quotes to be recognized as character constants. Integer constants are simply integer values.
+   - In addition to integer types `int` and `char`, C provides types **short int** (which can be abbreviated as **short**) and **long int** (which can be abbreviated as **long**), as well as **unsigned** versions of all the integral types. The C standard specifies the minimum value range for each type, but the actual range may be greater, depending on the implementation. For short ints the minimum range is −32767 to +32767. The minimum range of values for long ints is −2147483647 to +2147483647. The range of values for an int is greater than or equal to that of a short int and less than or equal to that of a long int. On many of today's platforms, ints and long ints represent the same range of values. The data type `signed char` can be used to represent integers in the range −127 to +127 or any of the characters in the computer's character set. See Section 5.2.4.2 of the C standard document for the complete list of signed and unsigned integer-range ranges.

# Section 4.8 **do...while Iteration Statement**

+   - The **do...while statement** tests the loop-continuation condition after the loop body is performed. Therefore, the loop body executes at least once. When a do...while terminates, execution continues with the statement after the while clause.

# Section 4.9 **break and continue Statements**

+   - The **break statement**, when executed in a while, for, do...while or switch statement, causes immediate exit from that statement. Program execution continues with the next statement.