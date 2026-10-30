# Creating numbered lists

By default, the items contained on an Access report are not numbered. They simply appear in the order dictated by the settings in the Group, Sort, and Total pane.

Sometimes it would be useful to have a number assigned to each entry on a report or within a group on a report. You might need a number to count the items in a list or uniquely identify items in the list. For example, an order details report might contain an item number for each item ordered, plus a field for items ordered, showing how many things were ordered.

The Access Running Sum feature provides a way to assign a number to each item in a list on an Access report. For example, the Northwind Traders sales management has asked for a report showing the sum of all purchases by each customer during the month of January, sorted in descending order so that the top purchaser appears at the top. Oh, yes—and they want a number assigned to each line in the report to provide a ranking for the Northwind customers.

The query to implement this request is shown in Figure 21.14 (qryCustomerPurchasesJanuary). This query sums the purchases by each customer for the month of January 2019. Because the Purchases column is sorted in descending order, the customers buying the most product will appear at the top of the query results set. The OrderDate field is not included in the query results and is used only as the query's selection criterion (notice the Where in the Total row).

# FIGURE 21.14

An interesting query that sums data and sorts the query results in descending order of the sum.

![](bbox=[0.18, 0.78, 0.88, 0.93])