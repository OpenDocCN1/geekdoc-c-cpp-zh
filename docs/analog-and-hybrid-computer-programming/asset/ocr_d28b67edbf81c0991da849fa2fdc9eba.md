![](bbox=[0.15, 0.1, 0.9, 0.36])

Fig. 6.75. Unsuitable direct approach of solving a system of linear equations on an analog computer

It is assumed that the matrix **A** is non-singular. The task at hand is now to solve a system of linear equations such as

$$\mathbf{A}\vec{x}=\vec{b}\tag{6.62}$$

for given **A** and $\vec{b}$, i. e.

$$\sum_{j=1}^{n} a_{ij}x_j - b_i = 0 \text{ with } 1 \le i \le n.$$

A direct approach would transform such a system of linear equations into a corresponding analog computer setup, which will be demonstrated using a simple example of two coupled equations:

$$a_{11}x_1 + a_{12}x_2 - b_1 = 0\tag{6.63}$$ $$a_{21}x_1 + a_{22}x_2 - b_2 = 0\tag{6.64}$$

Solving (6.63) and (6.64) for $x_1$ and $x_2$ respectively yields