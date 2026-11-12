(Max) section, which appears in the Final Value column to the right of objective function value, Maximize Total Profit. This number indicates that the optimal solution to this problem will provide a profit of $1600. Directly below the objective function value are the values of the decision variables at the optimal solution. These are shown as the Final Value column of the Variable Cells section in the answer report. Thus, we have F = 25 tons of fuel additive and S = 20 tons of solvent base as the optimal production quantities. We will discuss the meaning of the Integer column in the Variable Cells section in Chapter 11.

The Constraints section of the answer report provides information about the status of the constraints. Recall that the RMC problem had three less-than-or-equal-to constraints corresponding to the tons available for each of the three raw materials. The information shown in the Slack column provides the value of the slack variable for each of the three constraints. This information is summarized as follows:

| Constraint Number | Constraint Name | Value of Slack Variable |
|---|---|---|
| 1 | Material 1 Amount Used | 0 |
| 2 | Material 2 Amount Used | 1 |
| 3 | Material 3 Amount Used | 0 |

Thus, we see that the binding constraints (the Material 1 Amount Used and Material 3 Amount Used constraints) have zero slack at the optimal solution. The Material 2 Amount Used constraint has 1 ton of slack, or unused capacity.

# 7.5 A Simple Minimization Problem

M&D Chemicals produces two products that are sold as raw materials to companies manufacturing bath soaps and laundry detergents. Based on an analysis of current inventory levels and potential demand for the coming month, M&D's management has specified that the combined production of products A and B must total at least 350 gallons. Specifically, a major customer's order for 125 gallons of product A must also be satisfied. Product A requires 2 hours of processing time per gallon while product B requires 1 hour of processing time per gallon, and for the coming month, 600 hours of processing time are available. M&D's objective is to satisfy these requirements at a minimum total production cost. Production costs are $2 per gallon for product A and $3 per gallon for product B.

To find the minimum-cost production schedule, we will formulate the M&D Chemicals problem as a linear program. Following a procedure similar to the one used for the RMC problem, we first define the decision variables and the objective function for the problem. Let

A = number of gallons of product A
B = number of gallons of product B

Because the production costs are $2 per gallon for product A and $3 per gallon for product B, the objective function that corresponds to the minimization of the total production cost can be written as

Min 2A + 3B

Next, consider the constraints placed on the M&D Chemicals problem. To satisfy the major customer's demand for 125 gallons of product A, we know A must be at least 125. Thus, we write the constraint

1A >= 125