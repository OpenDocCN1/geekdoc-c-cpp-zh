to increment the loop counter. An operational semantics description of the C for statement is shown next. Because C expressions can be used as statements, expression evaluations are shown as statements.

```
expression_1
loop:
    if expression_2 = 0 goto out
    [loop body]
    expression_3
    goto loop
out: . . .
```

Following is an example of a skeletal C for statement:

```
for (count = 1; count <= 10; count++)
. . .
}
```

All of the expressions of C's for are optional. An absent second expression is considered true, so a for without one is potentially an infinite loop. If the first and/or third expressions are absent, no assumptions are made. For example, if the first expression is absent, it simply means that no initialization takes place.

Note that C's for need not count. It can easily model counting and logical loop structures, as demonstrated in the next section.

The C for design choices are the following: There are no explicit loop variables or loop parameters. All involved variables can be changed in the loop body. The expressions are evaluated in the order stated previously. Although it can create havoc, it is legal to branch into a C for loop body.

C's for is one of the most flexible, because each of the expressions can comprise multiple expressions, which in turn allow multiple loop variables that can be of any type. When multiple expressions are used in a single expression of a for statement, they are separated by commas. All C statements have values, and this form of multiple expression is no exception. The value of such a multiple expression is the value of the last component.

Consider the following for statement:

```
for (count1 = 0, count2 = 1.0;
    count1 <= 10 && count2 <= 100.0;
    sum = ++count1 + count2, count2 *= 2.5);
```

The operational semantics description of this is

```
count1 = 0
count2 = 1.0
loop:
    if count1 > 10 goto out
    if count2 > 100.0 goto out
    count1 = count1 + 1
```