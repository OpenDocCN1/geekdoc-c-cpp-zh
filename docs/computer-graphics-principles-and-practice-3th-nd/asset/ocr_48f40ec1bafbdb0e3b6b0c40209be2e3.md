# 31.4 Method 2: Restricting the Domain

Instead of trying to find a positive real number $x$ satisfying

$50x^{2.1}=13,$ (31.5)

we can ask, “Is there a positive integer satisfying (or nearly satisfying) it?” (See Figure 31.2.) Such a **domain restriction** can simplify things enormously. In the case of this equation, we see that the left-hand side is an increasing function of $x$, and that when $x=1$, its value is already 50. So any integer solution must lie between zero and one. We need only try these two possible solutions to see which one works (or, if none works, which is “best”). We quickly find that $x=0$ gives $50x^{2.1}=0$, which is too small, and $x=1$ gives 50, which is too large.

We then have two choices: We can report the “best” solution in the restricted domain ($x=0$), or we can perhaps say, “The ideal solution lies somewhere between 0 and 1, much closer to 0 than to 1; linear interpolation gives $x=0.26$ as a best-guess answer.” (See Figure 31.3.)

Our use of linear interpolation incorrectly assumes that the values of the left-hand side $F(x)=50x^{2.1}$ vary almost linearly as a function of $x$ between $x=0$ and $x=1$, which is why the estimated answer isn’t very close to the true one. More generally, if the domain of some variable is $D$, and we restrict to a subset $D'\subset D$, then estimating a solution in $D$ from approximate solutions in $D'$ requires that $D'$ “is large enough” that any point $d$ of $D$ lies near enough to points of $D'$ that $F(d)$ can be well inferred from values of $F$ at nearby points of $D'$.

We’ll see an example of domain restriction in rendering when we discuss radiosity. Note that methods 1 and 2 both violate the Approximate the Solution principle: they approximate the problem rather than the solution.

![](bbox=[0.708, 0.109, 0.931, 0.218])

*Figure 31.2:* The graph of $y=50x^{2.1}$, restricted to $x=0,1,2,3,4$, shown as a stem plot with small red circles, atop the graph on the whole real line (shown in gray).

![](bbox=[0.729, 0.407, 0.921, 0.528])

*Figure 31.3:* Because the value at $x=0$ is too small, and at $x=1$ it’s too large, we estimate the solution $x$ by intersecting the connect-the-dots plot (orange) with the line $y=13$ to get $x=0.26$.

# 31.5 Method 3: Using Statistical Estimators

A third approach is to “estimate” the solution statistically, that is, find a way to produce a sequence of values $x_1,x_2,\ldots$ such that each $x_i$ is a possible solution, and such that the average $a_n$ of $x_1,x_2,\ldots,x_n$ gets closer and closer to a solution as $n$ gets large.

In this case, we’re trying to solve

$50x^{2.1}=13,$ (31.6)

whose solution is

$x=\left(\frac{13}{50}\right)^{\frac{1}{2.1}}.$ (31.7)

This can be easily evaluated on a computer, but we’re assuming we lack the ability to compute anything more complicated than an integer power of a real number. (When we look at the rendering equation, the corresponding statement will be, “Suppose we lack the ability to compute anything except an integral number of bounces of a ray of light,” which is very reasonable: It’s hard to imagine what it might mean to compute 2.1 bounces of a light ray!) We can still find a solution using the binomial theorem, which says that