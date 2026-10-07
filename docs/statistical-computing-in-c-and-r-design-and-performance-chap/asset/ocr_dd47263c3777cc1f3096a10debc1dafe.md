# EXERCISES

b) How many decimal places of accuracy can be expected for a double under this storage scheme?

c) Can you conclude from this storage specification (why or why not) summing the series $1/j^2$ in reverse order as in Section 2.5 except with double precision is accurate to seven decimals?

2.9. Show that upon completion Algorithm 2.3 will return the sample residual sum-of squares.

2.10. Show that the algorithm below, due to Youngs and Cramer (1971), computes the sample residual sum-of-squares.

# Algorithm 2.5 Youngs and Cramer algorithm

```
$T = x_1$
$RSS = 0$
for $j = 2$ to $n$ do
  $T := T + x_j$
  $RSS := RSS + \frac{(x_j-T)^2}{T}$
end for
return $\sqrt{\frac{RSS}{n-1}}$
```

2.11. Consider the quadratic polynomial $q(x) = x^2 - 111.11x + 1.2121.

+   a) Find the roots of $q$ using the quadratic formula but using only five decimal digits with chopping in all your calculations (addition, multiplication, square root, etc.).

+   b) For a quadratic polynomial $ax^2+bx+c$ show that the roots $x_1$ and $x_2$ satisfy $x_1x_2 = c/|a|$. Use this latter relationship to evaluate the root having smaller absolute value for $q$ under the same conditions for digit retention and rounding and compare the result with your previous answer.

> (Conte and de Boer 1972)