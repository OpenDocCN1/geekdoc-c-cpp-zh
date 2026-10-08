```
{
  stmt1;
  stmt2;
}
```

Since the two embedded sequences contain the same statements, this can also be written as:

```
if(cond1 || cond2)
{
  stmt1;
  stmt2;
}
```

As an example consider the solution of the quadratic equation $ax^2 + bx + c = 0$. If $a = 0$ or $b^2 - 4ac < 0$, the formula for solving the equation for real roots cannot be used. The following code would be used to solve the equation.

```
if(a == 0 || (b * b - 4 * a * c ) < 0)
{
  printf("This is not a solvable equation");
}
else
{
  d = sqrt(b * b - 4 * a * c);
  x1 = (-b + d) / (2 * a);
  x2 = (-b - d) / (2 * a);
}
```

Compound logical expressions can be used. In the following example, a senior student is eligible for a scholarship if he or she has a grade point average of least 3.5. The same scholarship can be awarded to a junior student who has a grade point average of at least 3.75.

```
If((level == senior) && (GPA >Bplus) || (level == junior) && (GPA > Aminus))
{
  printf("student-id : %d is eligible for a scholarship\n", std_id);
}
```