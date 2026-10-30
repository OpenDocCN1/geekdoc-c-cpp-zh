Method 2: Right-click the field name and select Properties. The Property Sheet for Field Properties appears. In this dialog box, enter the desired alias in the Caption input, as shown in the following figure.

![](bbox=[0.26, 0.27, 0.5, 0.52])

# CAUTION

Be aware that if you use the Field Properties dialog box to define your alias, there will be no clear indication in either your query’s Design view or your query’s SQL string that you’re using an alias. This may lead to some confusion for anyone using your queries. For this reason, it’s generally better to use the first method to define an alias.

# About aggregate functions

In the example shown in Figure 10.3, you selected the Sum aggregate function from the Total drop-down list. Obviously, you could’ve selected any one of the 12 functions available. Indeed, you’ll undoubtedly come across analyses where you’ll have to use a few of the other functions available to you. So, it’s important to know what each one of these aggregate functions means for your data analysis.

# Group By

The Group By aggregate function aggregates all the records in the specified field into unique groups. Here are a few things to keep in mind when using the Group By aggregate function:

+   - Access performs the Group By function in your aggregate query before any other aggregation. If you’re performing a Group By along with another aggregate function, the Group By function will be performed first. The example shown in Figure 10.4 illustrates this concept. Access groups the Period field before summing the LineTotal field.

+   - Access sorts each group-by field in ascending order. Unless otherwise specified, any field tagged as a group-by field will be sorted in ascending order. If your query has multiple group-by fields, each field will be sorted in ascending order starting with the leftmost field.