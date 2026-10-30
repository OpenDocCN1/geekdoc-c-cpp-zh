# ## Specifying the type of join

If Access hasn’t auto-joined tblProducts and tblCategories (perhaps because the Category field was named differently in the tables), you can easily add an ad hoc join by dragging the Category field from one table and dropping it on the corresponding field in the other table.

The problem with most joins is that, by default, they exhibit inner join behavior as the query executes. In the case of the query in Figure 8.22, if a product record exists that doesn’t have an assigned category (for example, a car that was never assigned to a category), the query doesn’t return any records where a product record isn’t matched by a category.

The problem is that you can’t even tell records are missing. The only way you’d ever determine that there should be more records returned by this query is by carefully examining the sales records, by composing another query that counts all sales, or by performing some other audit operation.

You must modify the join characteristics between tblProducts and tblCategories to get an accurate picture of sales. Carefully right-click the thin join line between tblProducts and tblCategories, and select the Join Properties command from the shortcut menu. This action opens the Join Properties dialog box (see Figure 8.23), enabling you to specify an alternate join between the tables.

# FIGURE 8.23

![](bbox=[0.168, 0.63, 0.524, 0.795])

Selecting an outer join for the query.

In Figure 8.23, the third option (Include ALL Records from ‘tblProducts’...) has been selected (the first option is the default). Options 2 and 3 are left outer join and right outer join, respectively. These options direct Access to retrieve all records from the left (or right) table involved in the join, regardless of whether those records are matched on the other side of the join.