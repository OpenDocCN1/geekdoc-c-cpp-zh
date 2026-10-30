# Domain Aggregate Functions

Domain aggregate functions enable you to extract and aggregate statistical information from an entire data set (a domain). These functions differ from aggregate queries in that an aggregate query groups data before evaluating the values, whereas a domain aggregate function evaluates the values for the entire data set; thus, a domain aggregate function will never return more than one value. To get a clear understanding of the difference between an aggregate query and a domain aggregate function, build the query shown in Figure 15.13.

# FIGURE 15.13

This query shows you the difference between an aggregate query and a domain aggregate function.

![](bbox=[0.22, 0.48, 0.78, 0.68])

Run the query to get the results shown in Figure 15.14. You will notice that the Aggregate Sum column contains a different total for each year, whereas the Domain Sum column (the domain aggregate function) contains only one total (for the entire data set).

# FIGURE 15.14

You can clearly see the difference between an aggregate query and a domain aggregate function.

| Year | Aggregate Sum | Domain Sum |
|------|---------------|------------|
| 2011 | $16,402,703 | 16454683.25 |
| 2012 | $45,317,067 | 16454683.25 |
| 2013 | $61,776,367 | 16454683.25 |
| 2014 | $41,068,046 | 16454683.25 |