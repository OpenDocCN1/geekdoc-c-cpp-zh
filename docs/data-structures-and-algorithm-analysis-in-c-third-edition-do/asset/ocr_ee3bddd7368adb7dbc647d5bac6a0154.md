# 17.2 Hard Problems

strategy is to replace any clause $C_i$, that does not have exactly three literals with a set of clauses each exactly three literals. (Recall that a literal can be a variable such as $x_i$ or the negation of a variable such as $\overline{x}_i$.) Let $C_i = x_1 + x_2 + \dots + x_j$ where $x_1, \dots, x_j$ are literals.

+   1. $j=1$, so $C_i = x_1$. Replace $C_i$ with $C_i'$;

where $y$ and $z$ are variables not appearing in $E$. $C_i'$ is satisfiable if and only if $(x_1)$ is satisfiable, meaning that $x_1$ is **true**. Replace $C_i'$ with $C_i$

+   2. $j=2$, so $C_i = (x_1 + x_2)$.

```
$(x_1 + y) \cdot (x_1 + z) \cdot (x_1 + y + \overline{z}) \cdot (x_1 + \overline{y} + \overline{z})$
```

where $z$ is a new variable not appearing in $E$. This new pair of clauses is satisfiable if only if $(x_1 + x_2)$ is satisfiable, that is, either $x_1$ or $x_2$ must be true.

+   3. $j>3$. Replace $C_i = (x_1 + x_2 + \dots + x_j)$ with

```
$(x_1 + x_2) \cdot (x_3 + \overline{z}_1) \cdot (x_4 + \overline{z}_2 + z_3) \cdot \dots$
$(x_{j-2} + \overline{z}_{j-4} + z_{j-3}) \cdot (x_{j-1} + x_j + \overline{z}_{j-3})$
```

where $z_1, \dots, z_{j-3}$ are new variables.

After appropriate replacements have been made for each $C_i$, a Boolean expression results that is an instance of 3 SAT. satisfiable if and only if the original clause is satisfiable. The reduction is clearly polynomial time.

For the first two it is easy to see that the original clause is satisfiable if only if the resulting clauses are satisfiable. For the case where we replaced a clause with more than three literals, consider the following:

+   1. If $E$ is satisfiable, $E'$ is satisfiable: Assume $x_m$ is assigned **true**. Assign $z_i \le m-2$ as **true** and $z_k, l \ge m-1$ as **false**. All clauses in $E'$ are (3) satisfied.

+   2. If $x_1, x_2, \dots, x_j$ are all **false**, then $z_1, z_2, \dots, z_{j-3}$ are all **true**. But $(x_{j-1} + x_{j-2} + \overline{z}_{j-3})$ is **false**.

Next we define the VERTEX COVER for in further examples.

VERTEX COVER:

**Input:** A graph **G** and an integer $k$.

**Output:** YES if there is a subset **S** of the vertices in **G** of size $k$ or less that every edge of **G** has at least one of its endpoints in **S**, and NO otherwise.