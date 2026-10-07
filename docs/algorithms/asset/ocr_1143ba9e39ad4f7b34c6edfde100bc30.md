Let's investigate the issue by describing what we expect of these three multipliers, call them $y_1, y_2, y_3$.

| Multiplier | Inequality |
| :--- | :--- |
| $y_1$ | $x_1 \ $\le 200$ |
| $y_2$ | $x_2 \ $\le 300$ |
| $y_3$ | $x_1 + x_2 \ $\le 400$ |

To start, these $y_i$'s must be nonnegative, or otherwise they are unqualified to multiply inequalities (multiplying an inequality by a negative number would flip the $\le$ to $\ge$). After the multiplication and addition, we get the bound:

$$(y_1 + y_3)x_1 + (y_2 + y_3)x_2 \ $\le 200y_1 + 300y_2$$

We want the left-hand side to look like our objective function $x_1 + 6x_2$ so the right-hand side is an upper bound on the optimum solution. For this we need $y_1 + y_3$ to be 1 and $y_2 + y_3$ to be 6. Come to think of it, we would find if $y_1 + y_2$ are larger than 1—the resulting certificate would be all the more convincing. Thus, we get an upper bound

$$$x_1 + 6x_2 \ $\le 200y_1 + 300y_2 + 400y_3 \quad \text{if} \begin{cases} y_1 + y_3 \ $\ge 1 \ y_2 + y_3 \ $\ge 6 \end{cases}$$

We can easily find $y$'s that satisfy the inequalities on the right by simply making them large enough, $(y_1, y_2, y_3) = (5, 3, 6)$. But these particular multipliers would tell us that the optimum of the LP is at most $200\cdot5+300\cdot3+400\cdot6=4300$, which is far too loose to be of interest. What we want a bound that is as tight as possible, so we minimize $200y_1 + 300y_2 + 400y_3$ subject to the preceding inequalities. *And this is a new linear program*

Therefore, finding the set of multipliers that give the best upper bound on our original LP is tantamount to solving a new LP:

$$$200y_1 + 300y_2 + 400y_3 \ \begin{cases} y_1 + y_3 \ $\ge 1 \ y_2 + y_3 \ $\ge 6 \ y_1, y_2, y_3 \ $\ge 0 \end{cases}$$

By design, any feasible value of this dual LP is an upper bound on the original *primal*. If we somehow find a pair of primal and dual feasible values that are equal, then they must be optimal. Here is just such a pair:

$$$Primal : (x_1, x_2) = (100, 300); \quad Dual : (y_1, y_2, y_3) = (0, 5, 1).$$$$

They both have value 1900, and therefore they certify each's optimality (Figure 7.9).

Amazingly, this is not just a lucky example, but a general phenomenon. To start with, the preceding construction—creating a multiplier for each primal constraint,