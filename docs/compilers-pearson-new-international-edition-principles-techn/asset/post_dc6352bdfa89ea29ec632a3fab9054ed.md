
```text
i = 0;
while (i<100) {
    <some statements not involving i>
    i = i+1;
}
```
(a) A while-loop with obvious limits.

```text
i = 0;
while (1) {
    <some statements>
    i = i+1;
}
```
(b) It is unclear when or if this loop terminates.

```text
i = 0;
while (i<n) {
    <some statements not involving i or n>
    i = i+1;
}
```
(c) We don’t know the value of *n*, so we don’t know when this loop terminates.

Figure 11.9: Some while-loops

two points are in the polyhedron, all points on the line between them are also in the polyhedron. All the iterations in the loop are represented by the points with integer coordinates found within the polyhedron described by the loop-bound inequalities. And conversely, all integer points within the polyhedron represent iterations of the loop nest at some time.

```text
for (i = 0; i <= 5; i++)
    for (j = i; j <= 7; j++)
        Z[j,i] = 0;
```

Figure 11.10: A 2-dimensional loop nest

**Example 11.6:** Consider the 2-dimensional loop nest in Fig. 11.10. We can model this two-deep loop nest by the 2-dimensional polyhedron shown in Fig. 11.11. The two axes represent the values of the loop indexes *i* and *j*. Index *i* can take on any integral value between 0 and 5; index *j* can take on any integral value such that *i* ≤ *j* ≤ 7.

![](img/2a44b9071782fade81f3050c3b718341_795_0.png)

Figure 11.11: The iteration space of Example 11.6

> **Iteration Spaces and Array-Accesses**
>
> In the code of Fig. 11.10, the iteration space is also the portion of the array A that the code accesses. That sort of access, where the array indexes are also loop indexes in some order, is very common. However, we should not confuse the space of iterations, whose dimensions are loop indexes, with the data space. If we had used in Fig. 11.10 an array access like Z[2*i,i+j] instead of Z[j,i], the difference would have been apparent.

### 11.3.2 Execution Order for Loop Nests

A sequential execution of a loop nest sweeps through iterations in its iteration space in an ascending lexicographic order. A vector i = [i_0, i_1, ..., i_n] is *lexicographically less than* another vector i' = [i'_0, i'_1, ..., i'_n], written i < i', if and only if there exists an m < min(n,n') such that [i_0, i_1, ..., i_m] = [i'_0, i'_1, ..., i'_m] and i_{m+1} < i'_{m+1}. Note that m = 0 is possible, and in fact common.

**Example 11.7:** With i as the outer loop, the iterations in the loop nest in Example 11.6 are executed in the order shown in Fig. 11.12. □

![](img/2a44b9071782fade81f3050c3b718341_796_0.png)

Figure 11.12: Iteration order for loop nest of Fig. 11.10

### 11.3.3 Matrix Formulation of Inequalities

The iterations in a d-deep loop can be represented mathematically as

\[
\{i \in \mathbb{Z}^d \mid Bi + b \ge 0\} \qquad (11.1)
\]

Here,

- 1. **Z**, as is conventional in mathematics, represents the set of integers — positive, negative, and zero.
- 2. **B** is a $d \times d$ integer matrix,
- 3. **b** is an integer vector of length $d$, and
- 4. **0** is a vector of $d$ 0’s.

**Example 11.8:** We can write the inequalities of Example 11.6 as in Fig. 11.13. That is, the range of $i$ is described by $i \ge 0$ and $i \le 5$; the range of $j$ is described by $j \ge i$ and $j \le 7$. We need to put each of these inequalities in the form $u i + v j + w \ge 0$. Then, $[u,v]$ becomes a row of the matrix **B** in inequality (11.1), and $w$ becomes the corresponding component of the vector **b**. For instance, $i \ge 0$ is of this form, with $u=1$, $v=0$, and $w=0$. This inequality is represented by the first row of **B** and top element of **b** in Fig. 11.13.

![](img/2a44b9071782fade81f3050c3b718341_796_1.png)

Figure 11.13: Matrix-vector multiplication and a vector inequality represents the inequalities defining an iteration space

As another example, the inequality $i \le 5$ is equivalent to $(-1)i+(0)j+5 \ge 0$, and is represented by the second row of **B** and **b** in Fig. 11.13. Also, $j \ge i$ becomes $(-1)i+(1)j+0 \ge 0$ and is represented by the third row. Finally, $j \le 7$ becomes $(0)i+(-1)j+7 \ge 0$ and is the last row of the matrix and vector.

## Manipulating Inequalities

To convert inequalities, as in Example 11.8, we can perform transformations much as we do for equalities, e.g., adding or subtracting from both sides, or multiplying both sides by a constant. The only special rule we must remember is that when we multiply both sides by a negative number, we have to reverse the direction of the inequality. Thus, \(i \le 5\), multiplied by \(-1\), becomes \(-i \ge -5\). Adding 5 to both sides gives \(-i + 5 \ge 0\), which is essentially the second row of Fig. 11.13.

### 11.3.4 Incorporating Symbolic Constants

Sometimes, we need to optimize a loop nest that involves certain variables that are loop-invariant for all loops in the nest. We call such variables *symbolic constants*, but to describe the boundaries of an iteration space we need to treat them as variables and create an entry for them in the vector of loop indexes, i.e., the vector **i** in the general formulation of inequalities (11.1).

**Example 11.9:** Consider the simple loop:

```text
for (i = 0; i <= n; i++) {
    ...
}
```

This loop defines a one-dimensional iteration space, with index \(i\), bounded by \(i \ge 0\) and \(i \le n\). Since \(n\) is a symbolic constant, we need to include it as a variable, giving us a vector of loop indexes [i, n]. In matrix-vector form, this iteration space is defined by

\[
\left\{ [i,n] \in \mathbb{Z}^2 \mid
\begin{bmatrix}-1 & 1 \\ 1 & 0\end{bmatrix}
\begin{bmatrix}i \\ n\end{bmatrix}
\ge
\begin{bmatrix}0 \\ 0\end{bmatrix}
\right\}.
\]

Notice that, although the vector of array indexes has two dimensions, only the first of these, representing \(i\), is part of the output — the set of points lying within the iteration space. □

### 11.3.5 Controlling the Order of Execution

The linear inequalities extracted from the lower and upper bounds of a loop body define a set of iterations over a convex polyhedron. As such, the representation assumes no execution ordering between iterations within the iteration space. The original program imposes one sequential order on the iterations, which is the lexicographic order with respect to the loop index variables ordered from the outermost to the innermost. However, the iterations in the space can be executed in any order as long as their data dependences are honored (i.e., the order in which writes and reads of any array element are performed by the various assignment statements inside the loop are not changed).

The problem of how we choose an ordering that honors the data dependences and optimizes for data locality and parallelism is hard and is dealt with later starting from Section 11.7. Here we assume that a legal and desirable ordering is given, and show how to generate code that enforces the ordering. Let us start by showing an alternative ordering for Example 11.6.

**Example 11.10:** There are no dependences between iterations in the program in Example 11.6. We can therefore execute the iterations in arbitrary order, sequentially or concurrently. Since iteration $[i,j]$ accesses element $Z[j,i]$ in the code, the original program visits the array in the order of Fig. 11.14(a). To improve spatial locality, we prefer to visit contiguous words in the array consecutively, as in Fig. 11.14(b).

This access pattern is obtained if we execute the iterations in the order shown in Fig. 11.14(c). That is, instead of sweeping the iteration space in Fig. 11.11 horizontally, we sweep the iteration space vertically, so $j$ becomes the index of the outer loop. The code that executes the iterations in the above order is

```text
for (j = 0; j <= 7; j++)
    for (i = 0; i <= min(5,j); i++)
        Z[j,i] = 0;
```

Given a convex polyhedron and an ordering of the index variables, how do we generate the loop bounds that sweep through the space in lexicographic order of the variables? In the example above, the constraint $i \leq j$ shows up as a lower bound for index $j$ in the inner loop in the original program, but as an upper bound for index $i$, again in the inner loop, in the transformed program.

The bounds of the outermost loop, expressed as linear combinations of symbolic constants and constants, define the range of all the possible values it can take on. The bounds for inner loop variables are expressed as linear combinations of outer loop index variables, symbolic constants and constants. They define the range the variable can take on for each combination of values in outer loop variables.

## Projection

Geometrically speaking, we can find the loop bounds of the outer loop index in a two-deep loop nest by *projecting* the convex polyhedron representing the iteration space onto the outer dimension of the space. The projection of a polyhedron on a lower-dimensional space is intuitively the shadow cast by the object onto that space. The projection of the two-dimensional iteration space in Fig. 11.11 onto the $i$ axis is the vertical line from 0 to 5; and the projection onto
