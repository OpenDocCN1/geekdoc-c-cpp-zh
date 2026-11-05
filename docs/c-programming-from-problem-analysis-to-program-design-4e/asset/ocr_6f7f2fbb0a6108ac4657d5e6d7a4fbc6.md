The ?: operator is the only ternary operator in C#. The expression that comes before the question mark, expression1, is evaluated first. When expression1 evaluates to true, expression2, following the question mark, is executed; otherwise expression3, following the colon, is executed.

An example of a statement using the conditional operator is as follows:

```
grade = examScore > 89 ? 'A' : 'C';
```

This reads if examScore is greater than 89, assign A to grade; otherwise, assign C to grade. When examScore has a value of 75, the first expression, examScore > 89, evaluates to false; thus, expression3, C, following the colon is executed, and C is assigned to the grade memory location.

It performs the same operation as:

```
if (examScore > 89)
    grade = 'A';
else
    grade = 'C';
```

> NOTE The ternary conditional operator ( ? : ) is often used in an assignment statement.

Consider Example 5-25.

# EXAMPLE 5.25

Most service companies have a minimum charge they use for making house calls. Take, for example, a washing machine repairperson. He may charge $50.00 per hour; however, his minimum charge for traveling to your home is $100.00. Thus, when it takes him less than two hours, the charge is $100. A conditional expression to calculate the charges follows:

```
double charges,
    timeAtSite = 3.5;
charges = timeAtSite < 2.0 ? 100.00 : timeAtSite * 50.00;
```

The value stored in charges would be 175. The first expression (timeAtSite < 2.0) evaluates to false; thus, the last expression (timeAtSite * 50.00) is evaluated and 175 is stored in charges since the assignment operator, the equal symbol, has the lowest precedence in the expression and is performed last.

> NOTE The ternary conditional operator ( ? : ) is not as readable as the if statement. The if statement is used more often than other forms of the selection statement.