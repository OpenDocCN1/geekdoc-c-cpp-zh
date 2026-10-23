# Two-Dimensional Penalized Shubert Function

![](bbox=[0.07, 0.14, 0.48, 0.38])

Fig. 3. Numerical experiment for Problem 4. The black circles mark the convergent points at the non-diffusion step.

# Two-Dimensional Penalized Shubert Function with β=0.5

![](bbox=[0.07, 0.5, 0.48, 0.74])

Fig. 4. Numerical experiment for Problem 5. The black circles mark the convergent points at the non-diffusion step.

where β > 0 is a constant. The point (x,y) = (6.0835, −5.8581) is a global minimizer of g with β = 0. The function behaves roughly the same with the function considered in Problem 2, but has only one unique global minimizer at (x,y) = (6.0853, −5.8581) as shown in Fig. 4. We show the results of convergent points (circled points) of an arbitrary ID realization. Similar to the previous problems, the ID method is able to find the global minima.

![](bbox=[0.55, 0.1, 0.88, 0.38])

Fig. 5. The projection plot of the graph of y = g(x1,x2,x3) on the space x3 = 1 for Problem 6.

# Problem 4. A Multi-Dimensional Function. Let

```
g(x) = (π/n) { k sin²(π y1) + Σ_{i=1}^{n-1} (y_i - A)²[1 + k sin²(π y_{i+1})] + (y_n - A)² }, (48)
```

where

```
x = (x1, ..., xn) ∈ ℝⁿ, y_i = 1 + (x_i - 1)/4, i = 1, ..., n, k = 10, A = 1.
```

The function has roughly 5ⁿ local minima in the region {(x,y) : |x| < 10, |y| < 10} and a unique global minimum located at

```
x_i = 1, i = 1, ..., n.
```

For n = 3, Fig. 5 is the projection plot of the graph of y = g(x1,x2,x3) on the space x3 = 1, which illustrates the global minimizers is surrounded by many local minimizers. The 10 convergent points visited in a sequential order by an arbitrary ID realization for n = 3 and n = 4 are given in Table 1 respectively.

The ID method finds the global minima for both cases. And the frequencies of visiting the global minimum are obviously higher than that of any other local minima.