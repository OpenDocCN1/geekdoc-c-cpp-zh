
Because the combined production for both products must total at least 350 gallons, we can write the constraint

```
1A + 1B ≥ 350
```

Finally, the limitation on available processing time of 600 hours means that we need to add the constraint

```
2A + 1B ≤ 600
```

After adding the nonnegativity constraints (A, B ≥ 0), we have the following linear program for the M&D Chemicals problem:

```
Min 2A + 3B
s.t.
1A ≥ 125 Demand for product A
1A + 1B ≥ 350 Total production
2A + 1B ≤ 600 Processing time
A, B ≥ 0
```

Because the linear programming model has only two decision variables, the graphical solution procedure can be used to find the optimal production quantities. The graphical method for this problem, just as in the RMC problem, requires us to first graph the constraint lines to find the feasible region. By graphing each constraint line separately and then checking points on either side of the constraint line, the solutions that satisfy each constraint can be identified. By combining the solutions that satisfy each constraint on the same graph, we obtain the feasible region shown in Figure 7.16.

FIGURE 7.16 FEASIBLE REGION FOR THE M&D CHEMICALS PROBLEM

![](img/e2cb94e77057728e7ce105fa1f79ad61_27_0.png)

FIGURE 7.17 GRAPHICAL SOLUTION FOR THE M&D CHEMICALS PROBLEM

![](img/e2cb94e77057728e7ce105fa1f79ad61_28_0.png)

To find the minimum-cost solution, we now draw the objective function line corresponding to a particular total cost value. For example, we might start by drawing the line 2A + 3B = 1200. This line is shown in Figure 7.17. Clearly some points in the feasible region would provide a total cost of $1200. To find the values of A and B that provide smaller total cost values, we move the objective function line in a lower left direction until, if we moved it any farther, it would be entirely outside the feasible region. Note that the objective function line 2A + 3B = 800 intersects the feasible region at the extreme point A = 250 and B = 100. This extreme point provides the minimum-cost solution with an objective function value of $800. From Figures 7.16 and 7.17, we can see that the total production constraint and the processing time constraint are binding. Just as in every linear programming problem, the optimal solution occurs at an extreme point of the feasible region.

Can you use the graphical solution procedure to determine the optimal solution for a minimization problem? Try Problem 31.

## Summary of the Graphical Solution Procedure for Minimization Problems

The steps of the graphical solution procedure for a minimization problem are summarized here:

- 1. Prepare a graph for each constraint that shows the solutions that satisfy the constraint.

- 2. Determine the feasible region by identifying the solutions that satisfy all the constraints simultaneously.

- 3. Draw an objective function line showing the values of the decision variables that yield a specified value of the objective function.

- 4. Move parallel objective function lines toward smaller objective function values until further movement would take the line completely outside the feasible region.

- 5. Any feasible solution on the objective function line with the smallest value is an optimal solution.

## Surplus Variables

The optimal solution to the M&D Chemicals problem shows that the desired total production of A + B = 350 gallons is achieved by using all available processing time of 2A + 1B = 2(250) + 1(100) = 600 hours. In addition, note that the constraint requiring that product A demand be met is satisfied with A = 250 gallons. In fact, the production of product A exceeds its minimum level by 250 – 125 = 125 gallons. This excess production for product A is referred to as surplus. In linear programming terminology, any excess quantity corresponding to a ≥ constraint is referred to as surplus.

> Excel Solver refers to all nonbinding constraints as having positive slack values regardless of whether they are > or ≤ constraints. However, we will use “surplus” when referring to a nonbinding ≥ constraint.

Recall that with a ≤ constraint, a slack variable can be added to the left-hand side of the inequality to convert the constraint to equality form. With a ≥ constraint, a surplus variable can be subtracted from the left-hand side of the inequality to convert the constraint to equality form. Just as with slack variables, surplus variables are given a coefficient of zero in the objective function because they have no effect on its value. After including two surplus variables, S1 and S2, for the ≥ constraints and one slack variable, S3, for the ≤ constraint, the linear programming model of the M&D Chemicals problem becomes

```
Min 2A + 3B + 0S1 + 0S2 + 0S3
s.t.
1A - 1S1 = 125
1A + 1B - 1S2 = 350
2A + 1B + 1S3 = 600
A, B, S1, S2, S3 ≥ 0
```

> Try Problem 35 to test your ability to use slack and surplus variables to write a linear program in standard form.

All the constraints are now equalities. Hence, the preceding formulation is the standard form representation of the M&D Chemicals problem. At the optimal solution of A = 250 and B = 100, the values of the surplus and slack variables are as follows:

| Constraint | Value of Surplus or Slack Variable |
| :--- | :--- |
| Demand for product A | S1 = 125 |
| Total production | S2 = 0 |
| Processing time | S3 = 0 |

Refer to Figures 7.16 and 7.17. Note that the zero surplus and slack variables are associated with the constraints that are binding at the optimal solution—that is, the total production and processing time constraints. The surplus of 125 units is associated with the nonbinding constraint on the demand for product A.

In the RMC problem all the constraints were of the ≤ type, and in the M&D Chemicals problem the constraints were a mixture of ≥ and ≤ types. The number and types of constraints encountered in a particular linear programming problem depend on the specific conditions existing in the problem. Linear programming problems may have some ≤ constraints, some ≥ constraints, and some = constraints. For an equality constraint, feasible solutions must lie directly on the constraint line.

Try Problem 34 to practice solving a linear program with all three constraint forms.

An example of a linear program with two decision variables, G and H, and all three constraint forms is given here:

```
Min 2G + 2H
s.t.
1G + 3H <= 12
3G + 1H >= 13
1G - 1H = 3
G, H >= 0
```

The standard-form representation of this problem is

```
Min 2G + 2H + 0S1 + 0S2
s.t.
1G + 3H + 1S1 = 12
3G + 1H - 1S2 = 13
1G - 1H = 3
G, H, S1, S2 >= 0
```

The standard form requires a slack variable for the <= constraint and a surplus variable for the >= constraint. However, neither a slack nor a surplus variable is required for the third constraint because it is already in equality form.

When solving linear programs graphically, it is not necessary to write the problem in its standard form. Nevertheless, it is helpful to be able to compute the values of the slack and surplus variables and understand what they mean. A final point: The standard form of the linear programming problem is equivalent to the original formulation of the problem. That is, the optimal solution to any linear programming problem is the same as the optimal solution to the standard form of the problem. The standard form does not change the basic problem; it only changes how we write the constraints for the problem.

## Computer Solution of the M&D Chemicals Problem

The answer report for the M&D Chemicals Problem is presented in Figure 7.18. The answer report shows that the minimum-cost solution yields an objective function value of $800. The

FIGURE 7.18 ANSWER REPORT FOR THE M&D CHEMICALS PROBLEM

![](img/e2cb94e77057728e7ce105fa1f79ad61_30_0.png)

### Objective Cells (Min)
| Name | Original Value | Final Value |
| --- | --- | --- |
| Minimize Total Cost Product A | 0.000 | 800.000 |

### Variable Cells
| Model Variable | Name | Original Value | Final Value | Integer |
| --- | --- | --- | --- | --- |
| A | Gallons Produced Product A | 0.000 | 250.000 | Continuous |
| B | Gallons Produced Product B | 0.000 | 100.000 | Continuous |

### Constraints
| Constraint Number | Name | Cell Value | Status | Slack |
| --- | --- | --- | --- | --- |
| 1 | Demand for Product A | 250.000 | Not Binding | 125.000 |
| 2 | Total Production | 350.000 | Binding | 0.000 |
| 3 | Processing Time | 600.000 | Binding | 0.000 |
