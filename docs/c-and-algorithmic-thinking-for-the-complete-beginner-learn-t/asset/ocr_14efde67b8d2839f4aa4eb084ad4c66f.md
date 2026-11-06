When multiplication and division exist in the same expression, and since both are of the same precedence, they are performed left to right (the same way as you read), which means that the expression

```
y = 6 / 3 * 2
```

is equivalent to $y = \frac{6}{3} \cdot 2$, and assigns a value of 4 to variable $y$, (division is performed before multiplication).

If you want, however, the multiplication to be performed before the division, you can use parentheses to change the precedence, that is:

```
y = 6 / (3 * 2)
```

which is equivalent to $y = \frac{6}{3 \cdot 2}$

> **Notice:** C++ programs can be written using your computer’s text editor application, but keep in mind that it is not possible to write fractions in the form of $\frac{6}{3}$ or $\frac{4x+5}{6}$. Forget it! There is no equation editor in a text editor! All fractions must be written on one single line. For example, $\frac{6}{3}$ should be written as 6/3, and $\frac{4x+5}{6}$ should be written as (4*x+5)/6.

The order of operations can be summarized as follows:

+   1. Any operations enclosed in parentheses are performed first.
+   2. Next, any multiplication and division operations are performed from left to right.
+   3. In the end, any addition and subtraction operations are performed from left to right.

So, in statement $y = (20 + 3) + 12 + 8 / 4 * 3$;

the operations are performed as follows:

+   1. 20 is added to 3, yielding a result of 23.
+   2. 8 is divided by 4, yielding a result of 2. This result is then multiplied by 3, yielding a result of 6.
+   3. 23 is added to 12, yielding a result of 35. This result is then added to 6, yielding a final result of 41.

Next is the same sequence of operations presented in a more graphical way.