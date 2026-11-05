
```
public static void PrintResults(int largestOne)
{
    Console.WriteLine( );
    Console.WriteLine("The largest value entered was "
                      + largestOne);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(largestOne));
    Console.ReadLine( );
}
}
}
```

When you are writing selection statements, try to avoid repeating code. Instead of duplicating statements for both the **true** and **false** statements, pull out common statements and place them before or after the selection statement. You might have been tempted to solve the problem presented for Example 5-11 with the following two-way **if** statement:

```
if (value1 > value2)
{
    Console.WriteLine("The largest value entered was "
                      + value1);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(value1));
}
else
{
    Console.WriteLine("The largest value entered was "
                      + value2);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(value2));
}
```

The calls to the Console.WriteLine( ) method for displaying the largest value and its square root are included only once in Example 5-11. They appear twice in the last segment.

Another solution that is not modularized, but eliminates the repeating code, is as follows:

```
int largest;
if (value1 > value2)
{
    largest = value1;
}
else
{
    largest = value2;
}
Console.WriteLine("The largest value entered was "
                  + largest);
Console.WriteLine("Its square root is {0:f2}",
                  Math.Sqrt(largest));
```

All three ways of writing the selection statement produce the same output. The modularized version in Example 5-11 is the preferred approach of the three. In this situation, you may not see a clear advantage of one approach over the other. Modularization becomes more important as the complexity of a computer program increases. Figure 5-6 shows the output produced when the program is run with 25 entered for the first value and 15 entered for the second value.

![](img/e33ae760e23d89eac66541252ad65de8_290_0.png)

**Figure 5-6** Output from LargestValue problem

What does the program in Example 5-11 print when the values entered are the same?

Because `value1` is not greater than `value2`, the `else` statement is executed and `value2` is stored in `largestOne`. If you want to display a message indicating that the values are the same, you need to add one more conditional expression as part of the `if` statement. This additional test would be to determine whether `value2` is greater than `value1`. The expression would be added as the `else` statement. Adding this second test would enable you to include a second `else` statement. The last `else` would not be entered unless both of the conditional expressions evaluated to `false`—and in this case, the values are the same. If you make this revision, the logic would need to be revised for displaying the largest value. One approach would be to return the negative value of `value1` or `value2`, when they have the same value. It does not matter which one gets returned because their values are the same. The `PrintResults()` method could test the `largestOne` variable. When it is negative, a message could be printed indicating the values are the same. The additional test is as follows:

```text
if (value1 > value2)
{
    largestOne = value1;
}
else
    if (value1 < value2)
    {
        largestOne = value2;
    }
    else
        largestOne = -(value1);
```

Sometimes, a single variable might need to be tested for multiple values. A nested if...else statement, like that described previously, can be used for this. You might also want to test a different variable inside the true (or false) statements. A nested if...else statement is also used for this. You will learn more about nested if...else statements in the following section.

## Nested if...else Statement

Any statement can be included with the statements to be executed when the expression evaluates to true. The same holds for the false statements. Therefore, it is acceptable to write an if within an if. Many different expressions can be evaluated in a single if statement. When you place an if within an if, you create a nested if...else statement, also referred to as a nested if statement.

With a nested if statement, multiple expressions can be tested. As long as the expressions evaluate to true, the true statements continue to be evaluated. When another if statement is one of the statements in the block being executed, another evaluation is performed. This continues as long as additional if statements are part of the true statements.

As with the two-way, only one segment of code is executed. You never execute the true and its associated false statements. When the block is completed, all remaining conditional expressions and their statements are skipped or bypassed. After completing the execution of that block, control always transfers to the statement immediately following the if block. The syntax for a nested if...else statement, which follows that of the two-way, is repeated here. The difference is that with a nested if...else, the statement might be another if statement:

```
if (conditional_expression)    //No semicolon is placed on this line.
    statement;                // Could be another if statement
else
    statement;                // Could be another if statement
```

In a nested if...else, the inner if statement is said to be nested inside the outer if. However, the inner if may also contain another if statement. There are no restrictions on the depth of nesting. The limitation comes in the form of whether you and others can read and follow your code. The mark of a good program is that it is readable.

When you are designing a solution that requires a nested if...else, sometimes it is easier to develop your algorithm if you graphically map out the different options. A flowchart could be used. Another option is a decision tree, which is a design tool that allows you to represent complex procedures visually. Nodes are used to represent decision points, and lines branch out from the nodes to represent either further conditions or, eventually, the action to be taken based on the conditions expressed to the left. Figure 5-7 shows a decision tree used to calculate bonus for both hourly and salaried employees. Hourly employees working more than 40 hours per week receive $500. Other hourly employees get $100. Salaried employees who have been employed longer than 10 years receive $300, while the others receive $200. Figure 5-7 illustrates this situation in a decision tree.

![](img/e33ae760e23d89eac66541252ad65de8_292_0.png)

**Figure 5-7** Bonus decision tree

Example 5-12 shows how a nested if...else is used to determine the bonus amount illustrated in Figure 5-7.

### Example 5-12

```cpp
// For hourlyEmployees working more than 40 hours, a bonus of $500
// is issued. If hourlyEmployee has not worked more than 40 hours,
// issue a bonus of $100. For those non-hourlyEmployees, issue a
// $300 bonus if they have been employed longer than 10 years;
// otherwise, issue a $200 bonus.
bool hourlyEmployee;
double hours,
       bonus;
int yearsEmployed;

if (hourlyEmployee)
    if (hours > 40)
        bonus = 500;
    else
        bonus = 100;
else
    if (yearsEmployed > 10)
        bonus = 300;
    else
        bonus = 200;
```

No equality operator is needed in the first conditional expression. That is because a Boolean variable, hourlyEmployee, is used.

The logic for Example 5-12 could be written using four one-way `if` statements, as shown in Example 5-13. Here, each statement uses the `&&` operator.

### Example 5-13

```text
if (hourlyEmployee && hours > 40)
    bonus = 500;
if (hourlyEmployee && hours <= 40)
    bonus = 100;
if ((!hourlyEmployee) && yearsEmployed > 10)
    bonus = 300;
if ((!hourlyEmployee) && yearsEmployed <= 10)
    bonus = 200;
```

The single nested `if...else` solution in Example 5-12 is much more efficient than the four statements in Example 5-13. In Example 5-13, every one of the statements is evaluated, even if the first one evaluates to `true`. In Example 5-12, when the first two lines evaluate to `true`, 500 is assigned to `bonus` and no additional evaluations are performed.

Notice how a statement written using a logical `&&` can be rewritten as a nested `if...else`.

```text
if (hourlyEmployee && hours > 40)
```

produces the same result as

```text
if (hourlyEmployee)
    if (hours > 40)
```

When programming a nested `if...else` statement, it is important to know which `else` matches which `if` statement. The rule for lining up, or matching, elses is that an `else` goes with the closest previous `if` that does not have its own `else`. By properly lining up the `else` clauses with their corresponding `if` clauses, you encounter fewer logic errors that necessitate debugging. Example 5-14 illustrates the importance of properly lining up `if` and `else` clauses. Can you match each `else` with the correct `if`?

### Example 5-14

```text
if (aValue > 10)                         Line 1
if (bValue == 10)                        Line 2
amount = 5;                              Line 3
else                                     Line 4
    if (cValue > 100)                    Line 5
        if (dValue > 100)                Line 6
        amount = 10;                     Line 7
        else                             Line 8
        amount = 15;                     Line 9
    else                                 Line 10
        amount = 20;                     Line 11
else                                     Line 12
    if (eValue == 0)                     Line 13
    amount = 25;                         Line 14
```
