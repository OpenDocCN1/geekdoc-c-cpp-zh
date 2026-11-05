Sometimes, a single variable might need to be tested for multiple values. A nested if...else statement, like that described previously, can be used for this. You might also want to test a different variable inside the true (or false) statements. A nested if...else statement is also used for this. You will learn more about nested if...else statements in the following section.

# Nested if...else Statement

Any statement can be included with the statements to be executed when the expression evaluates to true. The same holds for the false statements. Therefore, it is acceptable to write an if within an if. Many different expressions can be evaluated in a single if statement. When you place an if within an if, you create a nested if...else statement, also referred to as a nested if statement.

With a nested if statement, multiple expressions can be tested. As long as the expressions evaluate to true, the true statements continue to be evaluated. When another if statement is one of the statements in the block being executed, another evaluation is performed. This continues as long as additional if statements are part of the true statements.

As with the two-way, only one segment of code is executed. You never execute the true and its associated false statements. When the block is completed, all remaining conditional expressions and their statements are skipped or bypassed. After completing the execution of that block, control always transfers to the statement immediately following the if block. The syntax for a nested if...else statement, which follows that of the two-way is repeated here. The difference is that with a nested if...else, the statement might be another if statement:

```
if (conditional_expression)    //No semicolon is placed on this line.
    statement;                // Could be another if statement
else
    statement;                // Could be another if statement
```

In a nested if...else, the inner if statement is said to be nested inside the outer if. However, the inner if may also contain another if statement. There are no restrictions on the depth of nesting. The limitation comes in the form of whether you and others can read and follow your code. The mark of a good program is that it is readable.

When you are designing a solution that requires a nested if...else, sometimes it is easier to develop your algorithm if you graphically map out the different options. A flowchart could be used. Another option is a decision tree, which is a design tool that allows you to represent complex procedures visually. Nodes are used to represent decision points, and lines branch out from the nodes to represent either further conditions or, eventually, the action to be taken based on the conditions expressed to the left. Figure 5-7 shows a decision tree used to calculate bonus for both hourly and salaried employees. Hourly employees working more than 40 hours per week receive $500. Other hourly employees get $100. Salaried employees who have been employed longer than 10 years receive $300, while the others receive $200. Figure 5-7 illustrates this situation in a decision tree.