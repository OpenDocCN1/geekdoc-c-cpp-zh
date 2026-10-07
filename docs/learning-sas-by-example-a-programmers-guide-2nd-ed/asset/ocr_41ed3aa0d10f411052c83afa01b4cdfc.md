As with the example using character values, you may separate the values with commas or spaces. You can also specify a range of numeric values, using a colon to separate values in the list. For example, to list observations where Subject is a 10, 22–25, or 30, you can write

```
where Subject in (10,22:25,30);
```

Remember that you should use a colon and not a dash for this work—a dash would be interpreted as a minus sign in a list of numbers separated by spaces.

> Note: The colon notation works only for integer values.

# 7.5 Using a SELECT Statement for Logical Tests

A SELECT statement provides an alternative to a series of IF and ELSE IF statements.

Here is one way to use a SELECT statement:

```
select (AgeGroup);
  when (1) Limit = 110;
  when (2) Limit = 120;
  when (3) Limit = 130;
  otherwise;
```

The expression following the SELECT statement is referred to as a select-expression; the expression following a WHEN statement is referred to as a when-expression. In this example, the select-expression (AgeGroup) is compared to each of the when-expressions. If the comparison is true, the statement following the when-expression is executed and control skips to the end of the SELECT group. If the comparison is false, the next when-expression is compared to the select-expression. If none of the comparisons are evaluated to be true, the expression following the OTHERWISE statement is executed. You can see in this example, the otherwise-expression can be a null statement. It is necessary to include an OTHERWISE statement because the program will terminate if you omit it and none of the preceding comparisons are true.

You can place more than one value in the when-expression, like this:

```
select (AgeGroup);
  when (1) Limit = 110;
  when (2) Limit = 120;
  when (3,5) Limit = 130;
  otherwise;
```

In this example, AgeGroup values of 3 or 5 will set Limit equal to 130.

To clarify this concept, let’s follow some scenarios:

If AgeGroup is equal to 1, Limit will be 110. If AgeGroup is equal to 3, Limit will be equal to 130. If AgeGroup is equal to 4, Limit will be a missing value (because it is set to a missing value in the PDV at each iteration of the DATA step and it is never assigned a value).