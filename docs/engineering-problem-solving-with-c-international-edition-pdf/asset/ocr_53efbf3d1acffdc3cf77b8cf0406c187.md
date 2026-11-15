# 1. PROBLEM STATEMENT

Use linear interpolation to compute a new freezing temperature for water with a specified salinity.

# 2. INPUT/OUTPUT DESCRIPTION

The following diagram shows that the input to the program includes two consecutive points (a, f(a)) and (c, f(c)) and the new salinity measurement b. The output is the new freezing temperature.

![](bbox=[0.22, 0.28, 0.72, 0.41])

# 3. HAND EXAMPLE

Suppose that we want to determine the freezing temperature for water with a salinity measurement of 33 ppt. From the data, we see that this point falls between 30 and 35 ppt:

| a | 30 | 29.1 | f(a) |
| b | 33 | ? | f(b) |
| c | 35 | 28.6 | f(c) |

Using the linear equation formula, we can compute f(b):

```
f(b) = f(a) + (b - a) / (c - a) . (f(c) - f(a))
= 29.1 + 3/5 . (28.6 - 29.1)
= 28.8
```

As expected, this value falls between f(a) and f(c).

# 4. ALGORITHM DEVELOPMENT

The first step in the development of an algorithm is the decomposition of the problem solution into a set of sequentially executed steps:

*Decomposition Outline*

+   1. Read the coordinates of the adjacent points and the new salinity value.
+   2. Validate input.
+   3. Compute the new freezing temperature.
+   4. Print the new freezing temperature.