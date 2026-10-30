![](bbox=[0.07, 0.12, 0.78, 0.38])

# FIGURE 7.1: Payoff Polygon with Nash Equilibrium

When the results are mixed strategies, the implication is that the game is repeated many times in order to achieve that outcome in the long run.

# Example 7.3. A 3 × 3 Nonzero Sum Game.

Rose and Colin each have three strategies with payoffs shown in Table 7.6.

# TABLE 7.6: Rose and Colin Strategies

|       | Colin |   |   |
|       | C1    | C2 | C3 |
| Rose  |       |    |    |
| R1    | (-1,1) | (0,2) | (0,2) |
| R2    | (2,1) | (1,-1) | (0,0) |
| R3    | (0,0) | (1,1) | (1,2) |

First, we use a movement diagram to find two Nash equilibrium points. They are R2C1 = (2,1) and R3C3 = (1,2). These pure strategy solutions are not equivalent and trying to achieve them might lead to other results. We might employ the nonlinear method described earlier to look for other equilibrium solutions, if they exist. We find the nonlinear method does produce another solution when p = q = 0.667 when x1 = 0, x2 = 0.667, x3 = 0.333, y1 = 0.333, y2 = 0, and y3 = 0.667. The Maple statements to obtain this solution are:

```
> with(Optimization):
> M := Matrix([[-1,0,0],[2,1,0],[0,1,1]]):
> N := Matrix([[1,2,2],[1,-1,0],[0,1,2]]):
```