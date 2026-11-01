```
if ((this._CustomerID != value))
{
    this.OnCustomerIDChanging(value);
    this.SendPropertyChanging();
    this._CustomerID = value;
    this.SendPropertyChanged("CustomerID");
    this.OnCustomerIDChanged();
}
}
```

Similar to when you built a class for yourself from the earlier example, the properties defined use the Column attribute and some of the properties available to this attribute. You can see that the primary key setting is set using the IsPrimaryKey item.

In addition to the Customer class, you will find that a class inheriting from the DataContext object is also within the created file:

```
[System.Data.Linq.Mapping.DatabaseAttribute(Name="NORTHWND")]
public partial class NorthwindDataContext: System.Data.Linq.DataContext
{
    // Code removed for clarity
}
```

The DataContext object, NorthwindDataContext, allows you to connect to the Northwind database and the Customers table, as was accomplished in the previous examples.

You will find that using the O/R Designer is a process that can make the creation of your database object class files simple and straightforward. However, at the same time, if you want complete control, you can code up everything yourself and get the results you are after.

# QUERYING THE DATABASE

As you've seen, there are a number of ways in which you can query the database from the code of your application. In some of the simplest forms, your queries looked like the following:

```
Table<Product> query = dc.Products;
```

This command was pulling down the entire Products table to your query object instance.

# Using Query Expressions

In addition to pulling a table straight out of the database using dc.Products, you also can use a query expression directly in your code that is strongly typed. An example of this is shown in the following code:

```
using System;
using System.Linq;

namespace ConsoleApplication1
{
    class Class1
    {
        static void Main(string[] args)
        {
            NorthwindDataContext dc = new NorthwindDataContext();

            var query = from p in dc.Products
                        select p;
```