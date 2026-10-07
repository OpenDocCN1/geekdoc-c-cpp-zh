# Common subproblems

Finding the right problem takes creativity and experimentation. But there are a few standard choices that seem to arise repeatedly in dynamic programming.

+   i. The input is $x_1, x_2, \dots, x_n$ and a subproblem is $x_1, x_2, \dots, x_i$.

```
$x_1\quad x_2\quad x_3\quad x_4\quad x_5\quad x_6\quad x_7\quad x_8\quad x_9\quad x_{10}$
```

The number of subproblems is therefore linear.

+   ii. The input is $x_1, \dots, x_n$ and $y_1, \dots, y_m$. A subproblem is $x_1, \dots, x_i$ and $y_1, \dots, y_j$.

```
$x_1\quad x_2\quad x_3\quad x_4\quad x_5\quad x_6\quad x_7\quad x_8\quad x_9\quad x_{10}$
```

```
$y_1\quad y_2\quad y_3\quad y_4\quad y_5\quad y_6\quad y_7\quad y_8$
```

The number of subproblems is $O(mn)$.

+   iii. The input is $x_1, \dots, x_n$ and a subproblem is $x_i, x_{i+1}, \dots, x_j$.

```
$x_1\quad x_2\quad x_3\quad x_4\quad x_5\quad x_6\quad x_7\quad x_8\quad x_9\quad x_{10}$
```

The number of subproblems is $O(n^2)$.

+   iv. The input is a rooted tree. A subproblem is a rooted subtree.

![](bbox=[0.4585, 0.4945, 0.8015, 0.7045])

If the tree has $n$ nodes, how many subproblems are there?

We've already encountered the first two cases, and the others are coming up shortly.