the DataSet, to update. The table contains a list of records that have been modified and the Insert, Update, and Delete properties of the SqlDataAdapter contain the SQL statements used to make database modifications.

# 6. DataSet Object

+   - DataSet is **tabular representation** of data into rows and columns. The dataset represents a subset of the database. It does not have a continuous connection to the database. To update the database a reconnection is required. The DataSet contains DataTable objects and DataRelation objects. The DataRelation objects represent the relationship between two tables.
+   
+   - The **ADO.NET** DataSet contains DataTableCollection and their DataRelationCollection. It represents a collection of data retrieved from the Data Source. Dataset can be used in combination with **DataAdapter** class. The DataSet object offers a disconnected data source architecture. The Dataset can work with the data it contain, without knowing the source of the data coming from. That is, the Dataset can work with a disconnected mode from its Data Source. It gives a better advantage over **DataReader**, because the DataReader is working only with the connection oriented Data Sources.
+   
+   - Some important properties of the DataSet class

| Properties | Description |
|---|---|
| CaseSensitive | Indicates whether string comparisons within the data tables are case-sensitive. |
| Container | Gets the container for the component. |
| DataSetName | Gets or sets the name of the current data set. |
| DefaultViewManager | Returns a view of data in the data set. |
| DesignMode | Indicates whether the component is currently in design mode. |
| EnforceConstraints | Indicates whether constraint rules are followed when attempting any update operation. |
| Events | Gets the list of event handlers that are attached to this component. |
| ExtendedProperties | Gets the collection of customized user information associated with the DataSet. |
| HasErrors | Indicates if there are any errors. |
| IsInitialized | Indicates whether the DataSet is initialized. |