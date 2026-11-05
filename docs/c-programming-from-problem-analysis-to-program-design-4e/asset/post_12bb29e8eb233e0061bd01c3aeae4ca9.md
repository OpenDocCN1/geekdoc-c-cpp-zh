
```
if (conditional_expression) // No semicolon is placed on this line
    statement;               // Could be another if statement
else
    statement;               // Could be another if statement
```

In a nested if...else, the inner if statement is said to be nested inside the outer if. However, the inner if may also contain another if statement. There are no restrictions on the depth of nesting. The limitation comes in the form of whether you and others can read and follow your code. The mark of a good program is that it is readable.

When you are designing a solution that requires a nested if...else, sometimes it is easier to develop your algorithm if you graphically map out the different options. A flowchart could be used. Another option is a decision tree, which is a design tool that allows you to represent complex procedures visually. Nodes are used to represent decision points, and lines branch out from the nodes to represent either further conditions or, eventually, the action to be taken based on the conditions expressed to the left. Figure 5-7 shows a decision tree used to calculate bonus for both hourly and salaried employees. Hourly employees working more than 40 hours per week receive $500. Other hourly employees get $100. Salaried employees who have been employed longer than 10 years receive $300, while the others receive $200. Figure 5-7 illustrates this situation in a decision tree.

![](img/36e48639a06772bcb0fa1ea2525b33a3_313_0.png)

## FIGURE 5-7 Bonus decision tree

Example 5-14 shows how a nested if...else is used to determine the bonus amount illustrated in Figure 5-7.

## EXAMPLE 5.14

```text
// For hourlyEmployees working more than 40 hours, a bonus of $500
// is issued. If hourlyEmployees has not worked more than 40 hours,
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

The logic for Example 5-14 could be written using four one-way if statements, as shown in Example 5-15. Here, each statement uses the && operator.

## EXAMPLE 5.15

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

The single nested if...else solution in Example 5-14 is much more efficient than the four statements in Example 5-15. In Example 5-15, every one of the statements is evaluated, even if the first one evaluates to true. In Example 5-14, when the first two lines evaluate to true, 500 is assigned to bonus and no additional evaluations are performed.

Notice how a statement written using a logical && can be rewritten as a nested if...else.

```text
if (hourlyEmployee && hours > 40)
```

produces the same result as

```text
if (hourlyEmployee)
    if (hours > 40)
```

When programming a nested `if...else` statement, it is important to know which `else` matches which `if` statement. The rule for lining up, or matching, elses is that an `else` goes with the closest previous `if` that does not have its own `else`. By properly lining up the `else` clauses with their corresponding `if` clauses, you encounter fewer logic errors that necessitate debugging. Example 5–16 illustrates the importance of properly lining up `if` and `else` clauses. Can you match each `else` with the correct `if`?

## EXAMPLE 5.16

```text
if (aValue > 10)                 Line 1
if (bValue == 0)                 Line 2
amount = 5;                      Line 3
else                             Line 4
if (cValue > 100)                Line 5
if (dValue > 100)                Line 6
amount = 10;                     Line 7
else                             Line 8
amount = 15;                     Line 9
else                             Line 10
amount = 20;                     Line 11
else                             Line 12
if (eValue == 0)                 Line 13
amount = 25;                     Line 14
```

As shown in Example 5–17, the `else` in Line 12 matches the `if` in Line 1; Line 10 matches Line 5. What value would be stored in amount if aValue, bValue, cValue, dValue, and eValue are all equal to 0? Did you get 25 when you traced the logic? Look at Example 5–17. By properly lining up the `else` clauses with their corresponding `if` clauses, the answer can be determined much more quickly.

## EXAMPLE 5.17

```text
if (aValue > 10)                 Line 1
    if (bValue == 0)             Line 2
        amount = 5;              Line 3
    else                         Line 4
        if (cValue > 100)        Line 5
            if (dValue > 100)    Line 6
                amount = 10;     Line 7
            else                 Line 8
                amount = 15;     Line 9
        else                     Line 10
            amount = 20;         Line 11
else                             Line 12
    if (eValue == 0)             Line 13
        amount = 25;              Line 14
```

The rule indicates that an `else` matches up with the closest previous `if` that does not already have an `else` attached to it. However, you can use braces to attach an `else` to an outer `if`, as shown in Example 5–18.

## EXAMPLE 5.18

```c
if (average > 59)
{
    if (average < 71)
        grade = 'D';
}
else
    grade = 'F';
```

The braces enclose the `true` statement associated with the expression of (average > 59). The inner `if` statement is ended as a statement when the closing curly brace is encountered.

Consider the statements in Example 5–19 that determine a grade based on testing the value in average.

## EXAMPLE 5.19

```c
if (average > 89)
    grade = 'A';
else
    if (average > 79)
        grade = 'B';
    else
        if (average > 69)
            grade = 'C';
        else
            if (average > 59)
                grade = 'D';
            else
                grade = 'F';
```

Pay particular attention to the conditional expressions in Example 5–19. It is not necessary for the second expression to be a compound expression using &&. You do not have to write `if (average > 79 && average <= 89)`. Make sure you understand that execution would never have reached the expression `(average > 79)` unless the first expression was `false`. If the average is not greater than 89, it must be either equal to 89 or less than 89.

As you reviewed Example 5–17 and 5–19, you probably wondered what happens when you keep indenting. Your statements soon start to go off to the right, out of sight.

A solution to this problem used by many programmers is to write a series of `else...if` statements when they have a long, nested, multiway statement.

The lines in Example 5–19 could be written with a series of `else...if` statements, as shown in Example 5–20. This prevents the indentation problem.

## EXAMPLE 5.20

```csharp
if (average > 89)
    grade = 'A';
else if (average > 79)
    grade = 'B';
else if (average > 69)
    grade = 'C';
else if (average > 59)
    grade = 'D';
else
    grade = 'F';
```

Examples 5–19 and 5–20 are multiway `if` statements. A single variable is tested using a relational operator.

A nested `if...else` statement could also be written using the equality operator in the conditional expression. Consider Example 5–21, which displays the weekday name based on testing an integer variable holding a number representing the day.

## EXAMPLE 5.21

```csharp
if (weekDay == 1)
    Console.WriteLine("Monday");
else if (weekDay == 2)
    Console.WriteLine("Tuesday");
else if (weekDay == 3)
    Console.WriteLine("Wednesday");
else if (weekDay == 4)
    Console.WriteLine("Thursday");
else if (weekDay == 5)
    Console.WriteLine("Friday");
else
    Console.WriteLine("Not Monday through Friday");
```

When you have a single variable, such as weekDay, being tested for equality against four or more values, a `switch` statement can be used. A `switch` statement is not an option for the nested `if...else` solution presented in Example 5–20. A `switch` statement only
