# Figure 4.11 Initial Bayesian Decision Tree for Oil Exploration

![](bbox=[0.06, 0.08, 0.88, 0.33])

# Table 4.9 Payoff Table for the Oil Exploration Problem

| Item | Value |
|---|---|
| Oil lease, if successful | $1,000,000 |
| Drilling expense | –$200,000 |
| Seismic survey | –$50,000 |

In order for the prospector to make the best decision, the **expected payoff** must be calculated at event node A. The expected payoff is the amount the prospector can make by following the best course of action. To compute the expected payoff at the start, A, we must work backwards from the leaves. In probability theory, this process is called **backward induction**. That is, in order to achieve the expected payoff or goal that we want, we must reason backwards to find the causes that will lead us to the goal.

The expected payoff from an event node is the sum of the payoffs times the probabilities leading to the payoffs:

```
Expected payoff at node C
$673,077 = ($750,000) (12/13) – ($250,000) (1/13)
```

```
Expected payoff at node B
$0 = ($750,000) (1/4) – ($250,000) (3/4)
```

At the action node E, we must decide between an expected payroll of –$50,000 by quitting or $846,153 by drilling. Since $846,153 is greater than –$50,000, we will induce that this is the better action and write it over node E. The path to quitting will be **pruned** or **poisoned** by breaking it with a "=" symbol to indicate this path will not be followed, as in Figure 4.12. Likewise at action node D, the best choice between a payoff of –$50,000 and a payoff of –$500,000 is –$50,000 and so this is written at D.