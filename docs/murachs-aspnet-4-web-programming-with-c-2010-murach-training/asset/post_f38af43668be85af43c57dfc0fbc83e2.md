
## How to create a select method

Figure 17-8 shows how to design and code a select method that can be used with an ObjectDataSource control. The table at the top of this figure lists the four different types of values that a select method can return. The simplest is the IEnumerable interface, which can return a data reader or a data view since the DataReader and DataView classes implement the IEnumerable interface. Also, the IEnumerable object can be a strongly-typed collection that’s created by using the generics feature of C#.

The select method can also return a DataTable or DataSet object. Because a dataset can contain more than one table, the ObjectDataSource control simply uses the first table in the dataset. As a result, you must design the select method so the first table in the dataset contains the data you want to access.

The main advantage of returning a dataset rather than a data table or data view is that the object data source can cache a dataset. Then, to enable caching, you can set the EnableCaching attribute to True for the ObjectDataSource control. In that case, the select method will be called only the first time the data is requested. For more information on caching, which works the same as it does for a SqlDataSource control, please refer back to chapter 13.

You can also pass parameters to the select method. In that case, the ObjectDataSource control must include a SelectParameters element. This element is added automatically if you use the Data Source Configuration Wizard to create the control. Then, you can create a ControlParameter element that binds a parameter to a control such as a drop-down list. You saw an example of this in figure 17-5.

### Allowable return types for a select method

| Return type | Description |
| --- | --- |
| IEnumerable | A collection such as an ArrayList or HashTable or a strongly-typed collection such as System.Collections.Generic.List. (Because the DataReader and DataView classes implement IEnumerable, the select method can also return a data reader or a data view.) |
| DataTable | If the select method returns a data table, the ObjectDataSource control automatically extracts a data view from the table and uses the view for data binding. |
| DataSet | If the select method returns a dataset, the ObjectDataSource control extracts a data view from the first data table in the dataset and uses the view for data binding. |
| Object | If the select method returns an object, the ObjectDataSource control wraps the object in an IEnumerable collection with just one item, then does the data binding as if the method returned an IEnumerable object. |

### A select method that returns a data reader

```
public static IEnumerable GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlCommand cmd = new SqlCommand(sel, con);
    con.Open();
    SqlDataReader dr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
    return dr;
}
```

### A select method that returns a dataset

```
public static DataSet GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlDataAdapter da = new SqlDataAdapter(sel, con);
    DataSet ds = new DataSet();
    da.Fill(ds, "Categories");
    return ds;
}
```

### Description

- The select method returns data retrieved from the underlying database. It can return the data in several forms, including a data reader or a dataset.
- If the select method returns a dataset, the object data source can cache the data.
- The select method can also return a strongly-typed collection using C#’s generics feature. See figure 17-15 for an example.
- If the select method accepts parameters, the parameters must be declared within the SelectParameters element of the ObjectDataSource control. Within this element, you can use the ControlParameter element to declare a parameter that’s bound to another control on the page.

## How to create update, delete, and insert methods

Besides select methods, the data access class used by an object data source can provide methods that update, delete, and insert data in the underlying database. Before you can code these methods, you need to determine what parameters are required. Figure 17-9 summarizes how an object data source generates these parameters.

Any insert or delete method you create requires a single business object as its parameter. This business object must contain all the values required by the method, and you can give it any name you choose. If an update method doesn’t provide for optimistic concurrency checking, it too requires a single business object as its parameter.

If an update method provides for optimistic concurrency checking, it requires two parameters as shown in the code at the top of this figure. One of the parameters must be a business object that provides the original values for the row to be updated, and the other parameter must be a business object that provides the new values for the row. Note that the name of the parameter for the business object that contains the new values can have any name you choose. However, the name of the parameter for the business object that contains the original values must be the same as the name of the parameter for the business object with the new values, preceded by the value of the OldValuesParameterFormatString attribute. In this example, the value of this attribute is original_, which is the default.

Two parameters are also required if the key column for a table is updatable. In that case, though, the object data source won’t automatically generate two parameters. Because of that, you will need to set the ConflictDetection property of the object data source to CompareAllValues even if the update method doesn’t provide for optimistic concurrency checking, and you will need to set the OldValuesParameterFormatString property accordingly. Then, you can use the property that contains the value for the key column of the object that contains the original values to identify the row to be updated.

This figure also lists the requirements for a business class that you can use to create the business objects.

- First, the class must provide a parameterless constructor. Since C# provides a parameterless constructor by default if a class isn’t defined with any constructors, you may be able to omit this constructor. However, I prefer to include it for completeness.
- Second, the class must define a public property for each bound field that’s passed from the bound control to the object data source. If the object data source is bound to a GridView or DetailsView control that uses BoundField elements, the names of these properties must be the same as the names specified for the DataField attributes of those elements. In contrast, if the object data source is bound to a GridView or DetailsView control that uses TemplateField elements, or if the object data source is bound to a FormView or ListView control, the names of these properties must be the same as the names in the Eval and Bind methods of the bound controls.
- Third, the property for each bound field must include both a get and a set accessor. The object data source uses the set accessors to set the values of the properties based on the values passed to it from the bound control. And the insert, update, and delete methods in the data access class use the get accessors to assign the values of the properties to parameters of command objects.

Once the ObjectDataSource control has determined what parameters need to be passed, it uses reflection to determine whether the data access class has a method that accepts the required parameters. If so, the method is called using these parameters. If not, an exception is thrown.

Before I go on, I want to point out that you don’t have to use business objects as the parameters of insert, update, and delete methods. Instead, you can use a parameter for each bound field that’s required by a method. This technique can be cumbersome, though, if more than just a few fields are required. In addition, it’s more difficult to determine what parameters the object data source will generate. It’s also more difficult to work with bound controls like the GridView control because you have to manually enter the name of each field you want to bind. That’s because the fields are defined in the data access class and not directly in the data source. (When you use business objects, the business class is identified in the data source, and the properties of that class are made available to bound controls.) For these reasons, I recommend that you use business objects whenever possible.

## How to use attributes to mark a data access class

Figure 17-10 shows how you can use C# attributes to identify a data access class and its methods. In case you haven’t worked with attributes before, they are simply a way to provide declarative information for classes, methods, properties, and so on. Although some of these attributes have meaning at runtime, the attributes in this figure are used at design time. In particular, the Data Source Configuration Wizard uses these attributes to determine which classes in the App_Code folder are data access classes and which methods in the data access class are select, insert, update, and delete methods.

Note, however, that you don’t need to use these attributes. The only reason to use them is to help the Data Source Configuration Wizard recognize the data access classes and methods. If you haven’t marked your data access classes with these attributes, you can still access them from the wizard by clearing the Show Only Data Components check box in the Choose a Business Object step of the wizard (see figure 17-3).
