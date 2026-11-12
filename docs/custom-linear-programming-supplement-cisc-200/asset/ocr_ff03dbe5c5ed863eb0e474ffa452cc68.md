# FIGURE 7.12 FEASIBLE SOLUTIONS FOR THE CONSTRAINT R - T ≥ 0

![](bbox=[0.17, 0.13, 0.9, 0.4])

+   3. Draw an objective function line showing the values of the decision variables that yield a specified value of the objective function.
+   4. Move parallel objective function lines toward larger objective function values until further movement would take the line completely outside the feasible region.
+   5. Any feasible solution on the objective function line with the largest value is an optimal solution.

# Slack Variables

In addition to the optimal solution and its associated profit contribution, the RMC managers will want information about the production requirements for the three materials. We can determine this information by substituting the optimal solution values (F = 25, S = 20) into the constraints of the linear program.

| Constraint | Tons Required for F = 25, S = 20 Tons | Tons Available | Unused Tons |
| :--- | :--- | :--- | :--- |
| Material 1 | 0.4(25) + 0.5(20) = 20 | 20 | 0 |
| Material 2 | 0.2(20) = 4 | 5 | 1 |
| Material 3 | 0.6(25) + 0.3(20) = 21 | 21 | 0 |

Can you identify the slack associated with a constraint? Try Problem 24, part (e).

Thus, the optimal solution tells management that the production of 25 tons of fuel additive and 20 tons of solvent base will require all available material 1 and material 3 but only 4 of the 5 tons of material 2. The 1 ton of unused material 2 is referred to as slack. In linear programming terminology, any unused or idle capacity for a ≤ constraint is referred to as the slack associated with the constraint. Thus, the material 2 constraint has a slack of 1 ton.

Often variables, called slack variables, are added to the formulation of a linear programming problem to represent the slack, or unused capacity, associated with a constraint. Unused capacity makes no contribution to profit, so slack variables have coefficients of zero in the objective function. More generally, slack variables represent the difference between