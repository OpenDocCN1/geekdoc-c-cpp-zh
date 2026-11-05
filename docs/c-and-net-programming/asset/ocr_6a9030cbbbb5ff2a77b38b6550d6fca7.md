![](bbox=[0.35, 0.07, 0.68, 0.36])

Fig. 16.5.1 Data set

# 16.6 Working with Data

# 16.6.1 ADO .NET - Handling Data though Data Manipulation Classes

+   - While working with database following hierarchy is instantiated in a sequence.

![](bbox=[0.15, 0.67, 0.98, 0.8])

Fig. 16.6.1 Database object creation

# 1. Creating a SqlConnection Object

+   - A SqlConnection is an object, just like any other C# object which is declared and instantiated as follows,

```
SqlConnection conn = new SqlConnection(
"Data Source=(local);Initial Catalog=Northwind;Integrated Security=SSPI");
```

The SqlConnection object instantiated above uses a constructor with a single argument of type string. This argument is called a connection string.

+   - Common parts of a connection string

ADO.NET Connection Strings contain certain key/value pairs for specifying how to make a database connection. They include the location, name of the database, and security parameters.