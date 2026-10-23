# Entering Responses

To enter responses, follow the steps in Figure 12.5.

# Figure 12.5  Entering Responses

![](bbox=[0.132, 0.157, 0.892, 0.434])

**Tip:** To quickly enter multiple responses, click the **N Responses** button and enter the number of responses you want.

# Specifying Goal Types and Lower and Upper Limits

When entering responses, you can tell JMP that your goal is to obtain the maximum or minimum value possible, to match a specific value, or that there is no goal.

The following description explains the relationship between the goal type (step 3 in Figure 12.5) and the lower and upper limits (step 4 in Figure 12.5):

+   - For responses such as strength or yield, the best value is usually the largest possible. A goal of **Maximize** supports this objective.
+   - The **Minimize** goal supports an objective of having the best objective be the smallest value, such as when the response is impurity or defects.
+   - The **Match Target** goal supports the objective when the best value for a response is a specific target value, such as with part dimensions. The default target value is assumed to be midway between the lower and upper limits.

**Note:** If your target range is not symmetric around the target value, you can alter the default target after you make a table from the design. In the data table, open the response’s Column Info dialog by double-clicking the column name, and enter an asymmetric target value.