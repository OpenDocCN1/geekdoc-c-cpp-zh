continued

# 4. This next part is a little tricky. You need to perform the following edits on the SQL statement in order to make it work for this situation:

+   - Because this subquery is a criteria for the Branch_Number field, you only need to select Branch_Number in the SQL statement; so, you can remove the line Sum(MainSummary .Revenue) AS SumOfRevenue.
+   - Delete all carriage returns.
+   - Place parentheses around the subquery and put the NOT IN operator in front of it all.

At this point, your Zoom dialog box should look like the one shown in the following figure.

![](bbox=[0.22, 0.44, 0.85, 0.65])

# 5. Switch to Design view. If all went well, your query should look similar to the following figure.

![](bbox=[0.22, 0.72, 0.95, 0.84])

There you have it. Running this query will return the second quartile in the data set. To get the third quartile, simply replace TOP 25 PERCENT in the subquery with TOP 50 PERCENT; to get the fourth quartile, use TOP 75 PERCENT.

# NOTE

Be sure to check this chapter's sample file to get the completed queries seen here.