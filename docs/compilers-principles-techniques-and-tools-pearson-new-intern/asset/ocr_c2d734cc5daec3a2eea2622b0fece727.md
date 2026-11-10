has no integer solutions, and thus there is no dependence between the read and write accesses.

To describe when there is a solution to a linear Diophantine equation, we need the concept of the *greatest common divisor* (GCD) of two or more integers. The GCD of integers $a_1, a_2, \ldots, a_n$, denoted $\gcd(a_1, a_2, \ldots, a_n)$, is the largest integer that evenly divides all these integers. GCD’s can be computed efficiently by the well-known Euclidean algorithm (see the box on the subject).

**Example 11.31:** $\gcd(24, 36, 54) = 6$, because $24/6$, $36/6$, and $54/6$ each have remainder 0, yet any integer larger than 6 must leave a nonzero remainder when dividing at least one of 24, 36, and 54. For instance, 12 divides 24 and 36 evenly, but not 54.

The importance of the GCD is in the following theorem.

**Theorem 11.32:** The linear Diophantine equation

$$a_1x_1 + a_2x_2 + \cdots + a_nx_n = c$$

has an integer solution for $x_1, x_2, \ldots, x_n$ if and only if $\gcd(a_1, a_2, \ldots, a_n)$ divides $c$.

**Example 11.33:** We observed in Example 11.30 that the linear Diophantine equation $2i = 2j + 1$ has no solution. We can write this equation as

$$2i - 2j = 1.$$

Now $\gcd(2, -2) = 2$, and 2 does not divide 1 evenly. Thus, there is no solution. For another example, consider the equation

$$24x + 36y + 54z = 30.$$

Since $\gcd(24, 36, 54) = 6$, and $30/6 = 5$, there is a solution in integers for $x$, $y$, and $z$. One solution is $x = -1$, $y = 0$, and $z = 1$, but there are an infinity of other solutions.

The first step to the data dependence problem is to use a standard method such as Gaussian elimination to solve the given equalities. Every time a linear equation is constructed, apply Theorem 11.32 to rule out, if possible, the existence of an integer solution. If we can rule out such solutions, then answer “no”. Otherwise, we use the solution of the equations to reduce the number of variables in the inequalities.

**Example 11.34:** Consider the two equalities

$$\begin{aligned}x - 2y + z &= 0 \\ 3x + 2y + z &= 5\end{aligned}$$