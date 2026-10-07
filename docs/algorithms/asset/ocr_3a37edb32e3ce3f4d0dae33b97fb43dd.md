We would be at a bit of a loss interpreting a flow that shifts 0.7 units along the edge Al-Carol, for instance! Unfortunately, the maximum-flow problem has the following

**Property:** if all edge capacities are integers, the optimal flow found by our algorithm is integral. We can see this directly from the algorithm, which in such cases would increase the flow by an integer amount on each iteration.

Integrality comes free in the maximum-flow problem. Unfortunately, this is the exception rather than the rule: as we will see in Chapter 8, it is a very difficult problem to find the optimum solution (or for matter, any solution) of a general linear program, if we also demand that the variables are integers.

# 7.4 Duality

We have seen that in networks, flows are smaller than cuts, but the maximum flow and min cut coincide and is therefore a certificate of the other's optimality. Remarkable as this phenomenon is, we generalize it from maximum flow to *any* problem that can be solved by linear programming! It turns out that every linear maximization problem has a *dual minimization* problem, and they relate to each other in the same way as flows and cuts.

To understand what duality is about, we recall our introductory LP to the two types of chocolate:

```
max x_1 + 6x_2
x_1 \le$ 200
x_2 \le$ 300
x_1 + x_2 \le$ 400
x_1, x_2 \ge$ 0.
```

Simplex declares the optimum solution to be $(x_1, x_2) = (100, 30)$, with objective value 1900. Can this answer be checked somehow? Let's see: suppose we take the first inequality and add it to six times the second inequality: We get

```
x_1 + 6x_2 \le$ 2000.
```

This is interesting, because it tells us that it is impossible to achieve a profit of more than 2000. Can we add together some combination of the LP constraints and bring this upper bound closer to 1900? After a little experimentation, we find that multiplying the three inequalities by 0, 5, and 1, respectively, and adding them up yields

```
x_1 + 6x_2 \le$ 1900.
```

So 1900 must indeed be the best possible value! The multipliers (0, 5, 1) magically constitute a *certificate of optimality*! It is remarkable that such a certificate exists for this LP—and even if we knew there were one, how would we systematically do finding it?