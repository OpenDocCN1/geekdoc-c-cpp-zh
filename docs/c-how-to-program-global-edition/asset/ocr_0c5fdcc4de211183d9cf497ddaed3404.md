# Common Programming Error 2.9

Placing commas (when none are needed) between conversion specifiers in the format control string of a scanf statement.

# Comparing Numbers

The if statement in lines 17–19

```
if ( num1 == num2 ) {
    printf(" %d is equal to %d\n", num1, num2 );
} // end if
```

compares the values of variables num1 and num2 to test for equality. If the values are equal, the statement in line 18 displays a line of text indicating that the numbers are equal. If the conditions are true in one or more of the if statements starting in lines 21, 25, 29, 33 and 37, the corresponding body statement displays an appropriate line of text. Indenting the body of each if statement and placing blank lines above and below each if statement enhances program readability.

# Common Programming Error 2.10

Placing a semicolon immediately to the right of the right parenthesis after the condition in an if statement.

A left brace, {, begins the body of each if statement (e.g., line 17). A corresponding right brace, }, ends each if statement's body (e.g., line 19). Any number of statements can be placed in the body of an if statement.

# Good Programming Practice 2.11

A lengthy statement may be spread over several lines. If a statement must be split across lines, choose breaking points that make sense (such as after a comma in a comma-separated list). If a statement is split across two or more lines, indent all subsequent lines. It's not correct to split identifiers.

Figure 2.14 lists from highest to lowest the precedence of the operators introduced in this chapter. Operators are shown top to bottom in decreasing order of precedence. The equals sign is also an operator. All these operators, with the exception of the assignment operator =, associate from left to right. The assignment operator (=) associates from right to left.

# Good Programming Practice 2.12

Refer to the operator precedence chart when writing expressions containing many operators. Confirm that the operators in the expression are applied in the proper order. If you're uncertain about the order of evaluation in a complex expression, use parentheses to group expressions or break the statement into several simpler statements. Be sure to observe that some of C's operators such as the assignment operator (=) associate from right to left rather than from left to right.