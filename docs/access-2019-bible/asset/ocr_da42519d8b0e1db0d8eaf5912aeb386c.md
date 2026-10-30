The first two methods occur automatically in the query design window. Relationships between tables are displayed in the Query Designer when you add related tables to a query. It also creates an automatic join between two tables that have a common field, as long as that field is a primary key in one of the tables and the Enable AutoJoin choice is selected (by default) in the Options dialog box.

If relationships are set in the Relationships window, you might not see the auto-join line if:

+   - The two tables have a common field, but it isn’t the same name.
+   - A table isn’t related and can’t be logically related to the other table (for example, tblCustomers can’t directly join the tblSalesLineItems table).

If you have two tables that aren’t related and you need to join them in a query, use the query design window. Joining tables in the query design window does not create a permanent relationship between the tables; instead, the join (relationship) applies only to the tables while the query operates.

# Leveraging ad hoc table joins

Figure 8.22 shows a simple query containing tblSales, tblSalesLineItems, tblProducts, and tblCategories. This is an ad hoc join, formed when the Categories table was added to the query.

![](bbox=[0.185, 0.508, 0.881, 0.781])

No direct relationship yet exists between tblProducts and tblCategories. However, Access found the Category field in both tables, determined that the Category data type is the same in both tables, and determined that the Category field in tblCategories is the primary key. Therefore, Access added an ad hoc join between the tables.