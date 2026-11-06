# How to Combine Various Conditions

SQL allows you to combine different conditions on your database queries. You just have to include the OR and AND operators in your SQL commands. SQL users refer to OR and AND as conjunctive operators.

Basically, the conjunctive operators allow you to perform multiple comparisons in a single SQL command. Let’s discuss OR first:

# OR

You may use this operator to combine various conditions in a command’s WHERE clause. The syntax of this operator is:

```
SELECT column1, column2, columnN
FROM table name
WHERE [condition1] OR [condition2],...OR [conditionN]
```

N represents the quantity of conditions that you can combine using OR. Your SQL statements will perform an action only if one of your specified conditions is true.

# AND

This operator allows you to place several conditions in the WHERE clause of an SQL command. Here’s the syntax that you should use:

```
SELECT column1, column2, columnN
FROM table name
WHERE [condition1] AND [condition2],...AND [conditionN]
```

“N” represents the quantity of conditions that you can combine. Keep in mind that your SQL command will only perform an action if all of the conditions are true.