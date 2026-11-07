# ### *Section 5.4 Examples Using the pow Function*

+   - Standard library function `pow(x, y)` (p. 160) calculates the value of x raised to the yᵗʰ power. Function `pow` takes two arguments of type double and returns a double value.
+   - Parameterized stream manipulator `setw` (p. 162) specifies the field width in which the next value output should appear, right justified by default. If the value is larger than the field width, the field width is extended to accommodate the entire value. Stream manipulator `left` (p. 162) causes a value to be left justified and `right` can be used to restore right justification.
+   - Sticky settings are those output-formatting settings that remain in effect until they’re changed.

# ### *Section 5.5 do...while Repetition Statement*

+   - The do...while repetition statement tests the loop-continuation condition at the end of the loop, so the body of the loop will be executed at least once. The format for the do...while statement is

```
do
{
    statement
} while ( condition );
```

# ### *Section 5.6 switch Multiple-Selection Statement*

+   - The switch multiple-selection statement (p. 164) performs different actions based on its controlling expression’s value.
+   - A switch statement consists of a series of case labels (p. 169) and an optional default case (p. 169).
+   - Function `cin.get()` reads one character from the keyboard. Characters normally are stored in variables of type char (p. 168). A character can be treated either as an integer or as a character.
+   - The expression in the parentheses following switch is called the controlling expression (p. 169). The switch statement compares the value of the controlling expression with each case label.
+   - Consecutive cases with no statements between them perform the same set of statements.
+   - Each case label can specify only one constant integral expression.
+   - Each case can have multiple statements. The switch selection statement differs from other control statements in that it does not require braces around multiple statements in each case.
+   - C++ provides several data types to represent integers—int, char, short and long. The range of integer values for each type depends on the particular computer’s hardware.

# ### *Section 5.7 break and continue Statements*

+   - The break statement (p. 173), when executed in one of the repetition statements (for, while and do...while), causes immediate exit from the statement.
+   - The continue statement (p. 173), when executed in a repetition statement, skips any remaining statements in the loop’s body and proceeds with the next iteration of the loop. In a while or do...while statement, execution continues with the next evaluation of the condition. In a for statement, execution continues with the increment expression in the for statement header.

# ### *Section 5.8 Logical Operators*

+   - Logical operators (p. 175) enable you to form complex conditions by combining simple conditions. The logical operators are && (logical AND), || (logical OR) and ! (logical negation).
+   - The && (logical AND, p. 175) operator ensures that two conditions are both true.
+   - The || (logical OR, p. 176) operator ensures that either or both of two conditions are true.
+   - An expression containing && or || operators evaluates only until the truth or falsehood of the expression is known. This performance feature for the evaluation of logical AND and logical OR expressions is called short-circuit evaluation (p. 176).