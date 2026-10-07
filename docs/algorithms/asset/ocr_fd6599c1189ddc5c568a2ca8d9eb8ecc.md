# 212

# 7.5 Zero-sum games

for fixed $x_1$ and $x_2$ the following are equivalent:

$$\max z$$
$$z = \min[3x_1 - 2x_2, -x_1 + x_2]$$
$$Z \le 3x_1 - 2x_2$$\n$$Z \le -x_1 + x_2$$

And Row needs to choose $x_1$ and $x_2$ to maximize this $z$.

$$\max z$$
$$-3x_1 + 2x_2 + z \le 0$$\n$$x_1 - x_2 + z \le 0$$\n$$x_1 + x_2 \ge 0$$

Symmetrically, if Column has to announce her strategy first, her best is to choose the mixed strategy that minimizes under Row's best response, in other words,

Pick $(y_1, y_2)$ \text{ that minimizes} \max(3y_1 - y_2, -2y_1 + y_2)$$
$$$\text{outcome of Row's best response to } y$$

In LP form, this is

$$\min w$$\n$$-3y_1 + y_2 + w \ge 0$$\n$$2y_1 - y_2 + w \ge 0$$\n$$y_1 + y_2 = 1$$\n$$$$y_1 + y_2 \ge 0$$

The crucial observation is that these two LPs are dual to each other (see Figure 7.11)! They have the same optimum, call it V.

Let us summarize. By solving LP, Row (the maximizer) can determine a strategy for herself that guarantees an expected outcome of at least $V$ no matter what Column does. And by solving the dual LP, Column (the minimizer) can guarantee an expected outcome of at most $V$, no matter what Row does. It follows that this is the uniquely defined optimal play: a priori it wasn't even certain that such a player exists. $V$ is known as the value of the game. In our example, it is $1/7$ and is realized when Row plays her optimal mixed strategy $(3/7, 4/7)$ and Column plays her optimum mixed strategy $(2/7, 5/7)$.

This example easily generalizes to arbitrary games and shows the existence of mixed strategies that are optimal for both players and achieve the same value—a fundamental result of game theory called the min-max theorem. It can be written in equation form as follows:

$$\max_{x} \sum_{i,j} G_{ij}x_i y_j = \min_{y} \sum_{i,j} G_{ij}x_i y_j$$