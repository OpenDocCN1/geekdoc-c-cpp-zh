```
if (x < 0)
    flag = 0;
else
    flag = 1;
```

can be written as

```
flag = (x < 0) ? 0 : 1;
```

Consider the evaluation of the following function:

y = 1.5x + 3    for x ≤ 2
 y = 2x + 5      for x > 2

This can be evaluated using the conditional operator as follows:

```
y = (x > 2) ? (2 * x + 5) : (1.5 * x + 3);
```

The conditional operator may be nested for evaluating more complex assignment decisions. For example, consider the weekly salary of a salesgirl who is selling some domestic products. If x is the number of products sold in a week, her weekly salary is given by

salary = { 4x + 100   for x < 40
          300        for x = 40
          4.5x + 150 for x > 40 }

This complex equation can be written as

```
salary = (x != 40) ? ((x < 40) ? (4*x + 100) : (4.5*x + 150)) : 300;
```

The same can be evaluated using if ... else statements as follows:

```
if (x <= 40)
    if (x < 40)
        salary = 4 * x +100;
    else
        salary = 300;
else
    salary = 4.5 * x + 150;
```

When the conditional operator is used, the code becomes more concise and perhaps, more efficient. However, the readability is poor. It is better to use if statements when more than a single nesting of conditional operator is required.

# Example 6.6

An employee can apply for a loan at the beginning of every six months, but he will be sanctioned the amount according to the following company rules:

+   Rule 1: An employee cannot enjoy more than two loans at any point of time.
+   Rule 2: Maximum permissible total loan is limited and depends upon the category of the employee.

A program to process loan applications and to sanction loans is given in Fig. 6.12.

The program uses the following variables:

+   loan3 - present loan amount requested
+   loan2 - previous loan amount pending
+   loan1 - previous to previous loan pending