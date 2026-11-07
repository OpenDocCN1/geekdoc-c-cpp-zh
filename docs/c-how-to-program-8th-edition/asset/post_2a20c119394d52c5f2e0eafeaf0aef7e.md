
activity diagrams and hence the set of all possible structured programs. The beauty of the structured approach is that we use only seven simple single-entry/single-exit control statements and assemble them in only two simple ways.

If the rules in Fig. 5.21 are followed, an activity diagram with illegal syntax (such as that in Fig. 5.25) cannot be created. If you’re uncertain about whether a particular diagram is legal, apply the rules of Fig. 5.21 in reverse to reduce the diagram to the simplest activity diagram. If it’s reducible to the simplest activity diagram, the original diagram is structured; otherwise, it isn’t.

![](img/bfd978e7e9b192bab46ec2a89e481263_217_0.png)

**Fig. 5.25** | Activity diagram with illegal syntax.

Structured programming promotes simplicity. Böhm and Jacopini have given us the result that only *three* forms of control are needed:

- Sequence
- Selection
- Repetition

The sequence structure is trivial. Simply list the statements to execute in the order in which they should execute.

Selection is implemented in one of three ways:

- `if` statement (single selection)
- `if…else` statement (double selection)
- `switch` statement (multiple selection)

It’s straightforward to prove that the *simple if statement* is sufficient to provide any form of selection—everything that can be done with the *if…else* statement and the switch statement can be implemented (although perhaps not as clearly and efficiently) by combining if statements.

Repetition is implemented in one of three ways:

- `while` statement
- `do…while` statement
- `for` statement

It’s straightforward to prove that the *while statement* is sufficient to provide any form of repetition. Everything that can be done with the *do…while* statement and the for statement can be done (although perhaps not as smoothly) with the while statement.

### Section 5.4 Examples Using the pow Function

- Standard library function `pow(x, y)` (p. 160) calculates the value of x raised to the yᵗʰ power. Function `pow` takes two arguments of type double and returns a double value.
- Parameterized stream manipulator `setw` (p. 162) specifies the field width in which the next value output should appear, right justified by default. If the value is larger than the field width, the field width is extended to accommodate the entire value. Stream manipulator `left` (p. 162) causes a value to be left justified and `right` can be used to restore right justification.
- Sticky settings are those output-formatting settings that remain in effect until they’re changed.

### Section 5.5 do...while Repetition Statement

- The do...while repetition statement tests the loop-continuation condition at the end of the loop, so the body of the loop will be executed at least once. The format for the do...while statement is

    ```cpp
    do
    {
        statement
    } while ( condition );
    ```

### Section 5.6 switch Multiple-Selection Statement

- The switch multiple-selection statement (p. 164) performs different actions based on its controlling expression’s value.
- A switch statement consists of a series of case labels (p. 169) and an optional default case (p. 169).
- Function `cin.get()` reads one character from the keyboard. Characters normally are stored in variables of type char (p. 168). A character can be treated either as an integer or as a character.
- The expression in the parentheses following switch is called the controlling expression (p. 169). The switch statement compares the value of the controlling expression with each case label.
- Consecutive cases with no statements between them perform the same set of statements.
- Each case label can specify only one constant integral expression.
- Each case can have multiple statements. The switch selection statement differs from other control statements in that it does not require braces around multiple statements in each case.
- C++ provides several data types to represent integers—int, char, short and long. The range of integer values for each type depends on the particular computer’s hardware.

### Section 5.7 break and continue Statements

- The break statement (p. 173), when executed in one of the repetition statements (for, while and do...while), causes immediate exit from the statement.
- The continue statement (p. 173), when executed in a repetition statement, skips any remaining statements in the loop’s body and proceeds with the next iteration of the loop. In a while or do...while statement, execution continues with the next evaluation of the condition. In a for statement, execution continues with the increment expression in the for statement header.

### Section 5.8 Logical Operators

- Logical operators (p. 175) enable you to form complex conditions by combining simple conditions. The logical operators are && (logical AND), || (logical OR) and ! (logical negation).
- The && (logical AND, p. 175) operator ensures that two conditions are both true.
- The || (logical OR, p. 176) operator ensures that either or both of two conditions are true.
- An expression containing && or || operators evaluates only until the truth or falsehood of the expression is known. This performance feature for the evaluation of logical AND and logical OR expressions is called short-circuit evaluation (p. 176).
- The ! (logical NOT, also called logical negation, p. 176) operator enables a programmer to “reverse” the meaning of a condition. The unary logical negation operator is placed before a condition to choose a path of execution if the original condition (without the logical negation operator) is false. In most cases, you can avoid using logical negation by expressing the condition with an appropriate relational or equality operator.
- When used as a condition, any nonzero value implicitly converts to true; 0 (zero) implicitly converts to false.
- By default, bool values true and false are displayed by cout as 1 and 0, respectively. Stream manipulator `boolalpha` (p. 177) specifies that the value of each bool expression should be displayed as either the word “true” or the word “false.”

### Section 5.9 Confusing the Equality (==) and Assignment (=) Operators

- Any expression that produces a value can be used in the decision portion of any control statement. If the value of the expression is zero, it’s treated as false, and if the value is nonzero, it’s treated as true.
- An assignment produces a value—namely, the value assigned to the variable on the left side of the assignment operator.

### Section 5.10 Structured Programming Summary

- Any form of control can be expressed in terms of sequence, selection and repetition statements, and these can be combined in only two ways—stacking and nesting.

### Self-Review Exercises

- **5.1** State whether the following are *true* or *false*. If the answer is *false*, explain why.
    - a) The default case is required in the switch selection statement.
    - b) The break statement is required in the default case of a switch selection statement to exit the switch properly.
    - c) The expression `( x > y && a < b )` is true if either the expression `x > y` is true or the expression `a < b` is true.
    - d) An expression containing the `||` operator is true if either or both of its operands are true.

- **5.2** Write a C++ statement or a set of C++ statements to accomplish each of the following:
    - a) Sum the odd integers between 1 and 99 using a `for` statement. Assume the integer variables `sum` and `count` have been declared.
    - b) Print the value 333.546732 in a 15-character field with precisions of 1, 2 and 3. Print each number on the same line. Left-justify each number in its field. What three values print?
    - c) Calculate the value of 2.5 raised to the power 3 using function `pow`. Print the result with a precision of 2 in a field width of 10 positions. What prints?
    - d) Print the integers from 1 to 20 using a `while` loop and the counter variable `x`. Assume that the variable `x` has been declared, but not initialized. Print only 5 integers per line. *[Hint: When x % 5 is 0, print a newline character; otherwise, print a tab character.]*
    - e) Repeat Exercise 5.2(d) using a `for` statement.

**5.3** Find the errors in each of the following code segments and explain how to correct them.

a)

```cpp
x = 1;
while ( x <= 10 );
    ++x;
}
```
