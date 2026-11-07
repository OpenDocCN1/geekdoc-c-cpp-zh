![](bbox=[0.35, 0.08, 0.78, 0.22])

# ### An Example: Ragged Array

We can create a two-dimensional array in which the number of elements in one row is different from the number of elements in another row, as shown in Figure 9.29.

In other words, we can have an array in which the first row has, for example, three elements, and the second row has four elements. This is referred to as a **ragged array**. This is possible, but we cannot allocate the elements in stack memory; they must be created in the heap. In other words, we must think about an array of pointers in which each pointer points to an array of the desired size, as shown in Figure 9.29. This design is more memory efficient than using a two-dimensional array, which leaves some of the elements empty.

# ### EXAMPLE 9.26

Pascal's triangle determines the coefficients of a binomial expansion. When a binomial like $(x + y)$ is raised to a positive integer power, we have:

```
$$(x + y)^n = a_0 x^n + a_1 x^{n-1} y + a_2 x^{n-2} y^2 + ... + a_{n-1} x y^{n-1} + a_n y^n$$
```

The coefficient of each term $(a_0, a_1, a_2, ..., a_{n-1}, a_n)$ can be calculated using a triangle of $n + 1$ rows and $n + 1$ columns. Each cell in the array holds the coefficient for a term. The number of rows is one more than the power value $(n)$. Each element in the triangle is calculated by adding the element in the previous row and the previous column with the element in the previous row and the same column, as shown below (when $n = 4$). It is obvious that to calculate the coefficients for any value of $n$ (beyond 0 and 1), we must know the value of the coefficients for the previous $n$. This justifies the use of a two-dimensional array. We can use an array of pointers to dynamically create the array and calculate the coefficients.

| n | coefficients |
|---|---|
| n = 0 | 1 |
| n = 1 | 1 1 |
| n = 2 | 1 2 1 |
| n = 3 | 1 3 3 1 |
| n = 4 | 1 4 6 4 1 |

# ### EXAMPLE 9.27

Program 9.15 finds the coefficients for any $n$ between 0 and 9. The number of allocated locations for each row is one greater than the row number. For example, when $i = 0$, we must allocate one location from the heap. When $i = 9$, we must allocate 10 locations from the heap.