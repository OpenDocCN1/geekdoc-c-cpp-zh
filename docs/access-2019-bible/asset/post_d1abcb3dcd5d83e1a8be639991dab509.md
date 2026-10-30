
## FIGURE 15.9

You're using a subquery as an expression in a calculation.

![](img/1e45673ab6eca9d20e67635ff5b9b318_496_0.png)

This example uses a subquery to get the average units sold for the entire company; that subquery will return a single value. You're then using that value in a calculation to determine the variance between each market's average units sold and the average for the company. The output of this query is shown in Figure 15.10.

## FIGURE 15.10

Your query result.

| Market | Market Avg | Vs Company Avg |
|---|---|---|
| Asia | 1,142 | -612 |
| Australia | 1,119 | -635 |
| Northern Europe | 2,647 | 893 |
| South America | 1,165 | -589 |
| Southern Europe | 1,800 | 46 |
| United Kingdom | 2,591 | 837 |
| United States | 1,814 | 60 |

## Using correlated subqueries

A correlated query is essentially a subquery that refers back to a column that is in the outer query. What makes correlated subqueries unique is that whereas standard subqueries are evaluated one time to get a result, a correlated subquery has to be evaluated multiple times—once for each row processed by the outer query. To illustrate this point, consider the following two SQL statements.

## Uncorrelated subqueries

The following SQL statement is using an uncorrelated subquery. How can you tell? The subquery isn't referencing any column in the outer query. This subquery will be evaluated one time to give you the average revenue for the entire data set.

```
SELECT MainSummary.Branch_Number,
    (SELECT Avg(Revenue) FROM MainSummary)
FROM MainSummary
```

## Correlated subqueries

This following SQL statement is using a correlated subquery. The subquery is reaching back into the outer query and referencing the Branch_Number column, effectively forcing the subquery to be evaluated for every row that is processed by the outer query. The end result of this query will be a data set that shows the average revenue for every branch in the company. Figure 15.11 shows how the following SQL statement is represented in the query editor.

```
SELECT MainSummary.Branch_Number,
(SELECT Avg(Revenue) FROM MainSummary AS M2 WHERE M2.Branch_Number = MainSummary.Branch_Number) AS AvgByBranch
FROM MainSummary
GROUP BY MainSummary.Branch_Number
```

## FIGURE 15.11

A correlated subquery.

![](img/1e45673ab6eca9d20e67635ff5b9b318_497_0.png)

## Using Aliases with Correlated Subqueries

Notice that in the correlated subquery, you're using the AS clause to establish a table alias of M2. The reason for this is that the subquery and the outer query are both utilizing the same table. By giving one of the tables an alias, you allow Access to distinguish exactly which table you're referring to in your SQL statement. Although the alias in this SQL statement is assigned to the subquery, you can just as easily assign an alias to the table in the outer query.

Note that the character M2 holds no significance. In fact, you can use any text string you like, as long as the alias and the table name combined do not exceed 255 characters.

To assign an alias to a table in Design view, simply right-click the field list and select Properties, as shown in the following figure.

## Chapter 15: Subqueries and Domain Aggregate Functions

Next, edit the Alias property to the one you would like to use (see the following figure). You’ll know that it took effect when the name on the Field List changes to your new alias.

## Using a correlated subquery as an expression

The example shown in Figure 15.9 used an uncorrelated subquery to determine the variance between each market’s average units sold and the average units for the company.

You can apply the same type of technique to correlated subqueries. In the query demonstrated in Figure 15.12, a correlation for each branch number allows you to determine the variance between each employee’s annual revenue and the average revenue for that employee’s branch.

## FIGURE 15.12

You can use a correlated subquery as part of an expression.

## Using subqueries within action queries

Action queries can be fitted with subqueries just as easily as select queries can. Here are a few examples of how you would use a subquery in an action query.

## A subquery in a make-table query

This example illustrates how to use a subquery in a make-table query to create a new table containing data for all employees hired before January 1995:

```
SELECT E1.Employee_Number, E1.Last_Name, E1.First_Name
INTO OldSchoolEmployees
FROM Employee_Master AS E1
WHERE E1.Employee_Number IN
    (SELECT E2.Employee_Number
    FROM Employee_Master AS E2
    WHERE E2.Hire_Date <#1/1/1995#)
```

## A subquery in an append query

This example uses a subquery in an append query to add new customers to the CustomerMaster table from the LeadList:

```
INSERT INTO CustomerMaster (Customer_Number, Customer_Name, State )
SELECT CompanyNumber,CompanyName,State
FROM LeadList
WHERE CompanyNumber Not In
    (SELECT Customer_Number from CustomerMaster)
```

## A subquery in an update query

This example uses a subquery in an update query to increase all prices in the PriceMaster table by 10% for only those branches in the South region:

```
UPDATE PriceMaster SET Price = [Price]*1.1
WHERE Branch_Number In
    (SELECT Branch_Number from LocationMaster WHERE Region = "South")
```

## A subquery in a delete query

This example uses a subquery in a delete query to delete customers from the LeadList table if they already exist in the CustomerMaster table:

```
DELETE *
FROM LeadList
WHERE CompanyNumber In
    (SELECT Customer_Number from CustomerMaster)
```

## Getting the Second Quartile of a Data Set with One Query

You can easily pull out the second quartile of a data set by using a top values subquery:

- 1. **Create a top values query that returns the top 25 percent of your data set.** You can specify that a query is a top values query by right-clicking the gray area above the white query grid and selecting Properties. In the Property Sheet dialog box, adjust the Top Values property to return the top nth value you need, as demonstrated in the following figure. For this example, use 25 percent.

![](img/1e45673ab6eca9d20e67635ff5b9b318_500_0.png)

- 2. **Switch to SQL view (shown in the following figure), and copy the SQL string.**

```
SELECT TOP 25 PERCENT MainSummary.Branch_Number
FROM MainSummary
GROUP BY MainSummary.Branch_Number
ORDER BY MainSummary.Branch_Number, Sum(MainSummary.Revenue) DESC;
```

- 3. **Switch back to Design view and paste the SQL statement you just copied into the Criteria row of the Branch_Number field.** To do this, right-click inside the Criteria row of the Branch_Number field and select Zoom. Then paste the SQL statement inside the Zoom dialog box, as shown in the following figure.

![](img/1e45673ab6eca9d20e67635ff5b9b318_500_1.png)

continued

## 4. This next part is a little tricky. You need to perform the following edits on the SQL statement in order to make it work for this situation:

- Because this subquery is a criteria for the Branch_Number field, you only need to select Branch_Number in the SQL statement; so, you can remove the line Sum(MainSummary .Revenue) AS SumOfRevenue.
- Delete all carriage returns.
- Place parentheses around the subquery and put the NOT IN operator in front of it all.

At this point, your Zoom dialog box should look like the one shown in the following figure.

![](img/1e45673ab6eca9d20e67635ff5b9b318_501_0.png)

## 5. Switch to Design view. If all went well, your query should look similar to the following figure.

![](img/1e45673ab6eca9d20e67635ff5b9b318_501_1.png)

There you have it. Running this query will return the second quartile in the data set. To get the third quartile, simply replace TOP 25 PERCENT in the subquery with TOP 50 PERCENT; to get the fourth quartile, use TOP 75 PERCENT.

## NOTE

Be sure to check this chapter's sample file to get the completed queries seen here.

## Domain Aggregate Functions

Domain aggregate functions enable you to extract and aggregate statistical information from an entire data set (a domain). These functions differ from aggregate queries in that an aggregate query groups data before evaluating the values, whereas a domain aggregate function evaluates the values for the entire data set; thus, a domain aggregate function will never return more than one value. To get a clear understanding of the difference between an aggregate query and a domain aggregate function, build the query shown in Figure 15.13.

## FIGURE 15.13

This query shows you the difference between an aggregate query and a domain aggregate function.

![](img/1e45673ab6eca9d20e67635ff5b9b318_502_0.png)

Run the query to get the results shown in Figure 15.14. You will notice that the Aggregate Sum column contains a different total for each year, whereas the Domain Sum column (the domain aggregate function) contains only one total (for the entire data set).

## FIGURE 15.14

You can clearly see the difference between an aggregate query and a domain aggregate function.

| Year | Aggregate Sum | Domain Sum |
|------|---------------|------------|
| 2011 | $16,402,703 | 16454683.25 |
| 2012 | $45,317,067 | 16454683.25 |
| 2013 | $61,776,367 | 16454683.25 |
| 2014 | $41,068,046 | 16454683.25 |
