You can order by columns in the ORDER BY statement that are not part of the SELECT statement as shown in this snippet:

```
SELECT Id, Name FROM Genre ORDER BY SortOrder DESC
```

In the next exercise, you will have to perform a number of queries against the sample database, giving you good idea of how different queries affect the results returned from the database.

# TRY OUT Selecting Data from the Sample Database

In this exercise you use the database that you created in an earlier exercise. This database is used only for the samples in this chapter, so don't worry if you miss. Note that all the exercises in this chapter use SQL Server Management Studio to work with your database. In later chapters you will see use VS to connect to your SQL Server database.

+   1. open SQL Server Management Studio if you don't have it anymore and log in to (LocalDB)\v11_0 as shown earlier. Expand the Databases node, then your PlanetWork database and the Tables node. You should see the two tables, Genre and Review, as shown earlier in Figure 12-8.
2. Right-click the Genre table and choose Edit Top 200 Rows. In the Document Window you should now see a list with all the available genres in the Genre table, shown in Figure 12-8.

Note that this is not just a list with all the rows in the Genre table. It's actually the result of a SQL query that is executed when you open the window. To see the query behind this list, ensure that the Query Designer toolbar, shown in Figure 12-9, is displayed on-screen. If the toolbar is not visible, right-click an existing toolbar and choose Query Designer.

![](bbox=[0.142, 0.355, 0.953, 0.9])

Figure 12-9