# Chapter 11: Generating Reports and Using Search 277

For example, if you want to associate the same schema name for all the tables in the relational model, start the Search operation for the relational model wanted, * in the search field, and select Oracle Database 12c (or whatever the RDBMS site is) in Filter. Then click Properties, go to Property Name User, and click the list to select the value for a schema name. Click Apply.

![](bbox=[0.095, 0.237, 0.167, 0.273])

TIP
If you want to replace an existing value with an empty value, click the left-pointing arrow at the end of the property name setting and select Empty String.

# Summary

You can generate reports by choosing File | Reports or using the search functionality. You can also print a diagram by choosing File | Print Diagram. You can generate reports from Data Modeler designs that are open at the time, or they can be generated from the Data Modeler reporting repository. A user can create standard and custom templates to get the reports to look like they need to and include the information wanted. Customer reports can be generated in Microsoft Excel format, and the changed information can be imported into Data Modeler to either a logical or relational model. Reports can be generated in different formats for different needs.

The reporting repository is a database that can be accessed with SQL. A user can have read-only access to the reporting repository to be able to query it with SQL. The reporting repository is a read-only repository, and all changes to the content must be done with Data Modeler.

Data Modeler has strong search features to find any possible detail in a design. A search can be performed in simple or advanced mode. Also, regular expressions can be used in searches. The search functionality can be used not only for searching but also for reporting and setting common properties in the result set.