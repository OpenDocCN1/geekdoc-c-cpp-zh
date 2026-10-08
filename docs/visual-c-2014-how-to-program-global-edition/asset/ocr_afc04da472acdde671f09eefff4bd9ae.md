# Answers to Self-Review Exercises

6.1 a) for, b) after. c) switch. d) continue. e) && (conditional AND) or && (boolean logical AND). f) false. g) static.

6.2 a) The default label is optional. If no default action is needed, there's no need for a default label. You could terminate the case with other statements, such as a return.
c) False. The body of relational expressions must be true for this expression to be true when using the && operator.
d) True. True) False. The switch statement does not provide a mechanism for testing ranges of values, you must list every value in a separate case label. g) True.

6.3 The answers to Self-Review Exercise 6.3 are as follows:

```
a) sum = 0;
for (count = 1; count <= 99; count += 2)
{
sum += count;
}
b) double result = Math.Pow(2.5, 3);
c) i = 1;
```

```
while (i <= 20)
{
Console.Write(i);
if (i % 5 == 0)
{
Console.WriteLine();
else
{
Console.Write('\t');
}
}
++i;
```

```
d) for (i = 1; i <= 20; ++i)
{
Console.Write(i);
if (i % 5 == 0)
{
Console.WriteLine();
else
{
Console.Write('\t');
}
}
```

6.4 The answers to Self-Review Exercise 6.4 are as follows:

+   a) Error: The semicolon after the while header causes an infinite loop, and there's a missing left brace for the body of the while statement.
Correction: Remove the semicolon and add a { before the loop's body.