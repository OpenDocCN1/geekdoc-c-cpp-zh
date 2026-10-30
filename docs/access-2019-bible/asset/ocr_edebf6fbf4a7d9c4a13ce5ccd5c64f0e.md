# CAUTION

Be aware that values you enter into your parameters must fit into the data type required for the function's argument. For example, if you're using a parameter in a DateDiff function, the variable you assign that parameter must be a date; otherwise, the function won't work.

# NOTE

When you run the query in Figure 13.8, you'll only have to enter the start date and the end date one time, even though they're both used in two places in the query. This is because once you assign a variable to a parameter, the assignment persists to every future instance of that parameter.
If you are prompted more than once for a parameter used more than once in your query, odds are there's a slight variation in how the parameter names were typed. Consider copying your parameters to avoid this.

# Creating a Parameter Prompt That Accepts Multiple Entries

The parameter query in the following figure enables you to filter results dynamically by a variable period that you specify within the parameter. However, this query does not allow you to see results for more than one period at a time.

![](bbox=[0.13, 0.69, 0.88, 0.84])

You could use more than one parameter, as shown in the following figure. Unlike the query in the preceding figure, this query allows you to include more than one period in your query results. However, you would still be limited to the number of parameters built into the query (in this case, three).