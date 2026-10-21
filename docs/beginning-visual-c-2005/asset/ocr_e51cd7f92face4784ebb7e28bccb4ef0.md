# Products Table

# Orders Table

![](bbox=[0.15, 0.18, 0.52, 0.32])

![](bbox=[0.52, 0.18, 0.92, 0.32])

![](bbox=[0.25, 0.35, 0.92, 0.78])

# Result of Join Operation

# Figure 19-4

The recordset produced by the SELECT statement has nine records that are produced by combining each record from the Products table with every record from the Orders table, so all possible combinations are included. This may not be exactly what is required or what you expected. Arbitrarily including all combinations of records from one table with another is of limited value. The meaning of a record containing details of the bread product and an order for cake is hard to fathom. You could also end up with an incredibly big table in a real situation. If you combine a table containing 100 products with one containing 500 orders and you do not constrain the join operation, the resulting table will contain 50,000 records!

To get a useful join, you usually need to add a WHERE clause to the SELECT statement. With the tables we have been using, one condition that would make sense would be to only allow records where the Product