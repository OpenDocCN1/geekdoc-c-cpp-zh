# Appendix C Pseudocode Reference 595

Case value_2:
statement
statement
etc. These statements are executed if the testExpression is equal to value_2.

Insert as many Case sections as necessary

Case value_N:
statement
statement
etc. These statements are executed if the testExpression is equal to value_N.

Default:
statement
statement
etc. These statements are executed if the testExpression is not equal to any of the values listed after the Case statements.

End Select This is the end of the structure.

The first line of the structure starts with the Select statement, followed by a testExpression. Inside the structure there are one or more blocks of statements that begin with a Case statement. Notice that the Case word is followed by a value.

When the Case statement executes, it compares the value with the values that follow each of the Case statements (from top to bottom). If it finds a value that matches the testExpression's value, the program branches to the Case statement. The statements that immediately follow the Case statement are executed, and then the program jumps out of the structure. If the testExpression does not match any of the Case values, the program branches to the Default statement and executes the statements that immediately follow it. Here is an example:

+   Select month
Case 1:
Display "January"
Case 2:
Display "February"
Case 3:
Display "March"
Default:
Display "Error: Invalid month"
End Select

# The While Loop

General format:

While condition
statement
statement
etc. These statements are the body of the loop. They are repeated while the condition is true.

End While

In the general format, the condition is a Boolean expression, and the statements that appear on the lines between the While and the End clauses are the body of the loop. When the loop executes, the condition is tested. If it is true, the statements that appear in the body of the loop are executed, and then the loop starts over. If the