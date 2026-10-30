# Chapter 15: Subqueries and Domain Aggregate Functions

Next, edit the Alias property to the one you would like to use (see the following figure). You’ll know that it took effect when the name on the Field List changes to your new alias.

# Using a correlated subquery as an expression

The example shown in Figure 15.9 used an uncorrelated subquery to determine the variance between each market’s average units sold and the average units for the company.

You can apply the same type of technique to correlated subqueries. In the query demonstrated in Figure 15.12, a correlation for each branch number allows you to determine the variance between each employee’s annual revenue and the average revenue for that employee’s branch.

# FIGURE 15.12

You can use a correlated subquery as part of an expression.