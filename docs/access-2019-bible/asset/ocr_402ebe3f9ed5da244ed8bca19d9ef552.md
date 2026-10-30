calculated results in your tables, but using tables to store calculated results is problematic for several reasons:

+   - Stored calculations take up valuable storage space.
+   - Stored calculations require constant maintenance as the data in your table changes.
+   - Stored calculations generally tie your data to one analytical path.

Instead of storing the calculated results as hard data, it’s a better practice to perform calculations in real time, at the precise moment when they’re needed. This ensures the most current and accurate results and doesn’t tie your data to one particular analysis.

# Common calculation scenarios

In Access, calculations are performed using expressions. An expression is a combination of values, operators, or functions that are evaluated to return a separate value to be used in a subsequent process. For example, 2+2 is an expression that returns the integer 4, which can be used in a subsequent analysis. Expressions can be used almost anywhere in Access to accomplish various tasks: in queries, forms, reports, data access pages, and even tables to a certain degree. In this section, you’ll learn how to expand your analysis by building real-time calculations using expressions.

# Using constants in calculations

Most calculations typically consist of hard-coded numbers or constants. A constant is a static value that doesn’t change. For example, in the expression [List_Price]*1.1, 1.1 is a constant; the value of 1.1 will never change. Figure 12.1 demonstrates how a constant can be used in an expression within a query.

In this example, you’re building a query that will analyze how the current price for each product compares to the same price with a 10 percent increase. The expression, entered under the alias "Increase" will multiply the List_Price field of each record with a constant value of 1.1, calculating a price that is 10 percent over the original value in the List_Price field.

# FIGURE 12.1

In this query, you’re using a constant to calculate a 10 percent price increase.

![](bbox=[0.17, 0.00122, 0.55, 0.00188])