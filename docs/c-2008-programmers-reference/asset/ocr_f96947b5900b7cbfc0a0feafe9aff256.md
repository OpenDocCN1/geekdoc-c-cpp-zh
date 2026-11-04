# Part I: C# Fundamentals

As evident from the query, the Customers table is related to the Orders table via the CustomerID field, and the Orders table is related to the Order Details table via the OrderID field.

Figure 14-9 shows the result of the query.

![](bbox=[0.15, 0.3, 0.85, 0.65])

Figure 14-9

# Typed DataSet

So far you've used the Field() extension method to access the field of a DataTable object. For example, the following program uses LINQ to DataSet to query all the customers living in the USA. The result is then reshaped using an anonymous type:

```
SqlConnection conn;
SqlCommand comm;
SqlDataAdapter adapter;
DataSet ds = new DataSet();

conn = new SqlConnection(@"Data Source=.\SQLEXPRESS;" +
    "Initial Catalog=Northwind;Integrated Security=True");
comm = new SqlCommand("SELECT * FROM Customers", conn);
adapter = new SqlDataAdapter(comm);
adapter.Fill(ds, "Customers");

var query1 =
    (from customer in ds.Tables[0].AsEnumerable()
     where customer.Field<string>("Country") == "USA"
     select new
     {
         CustomerID = customer.Field<string>("CustomerID"),
         CompanyName = customer.Field<string>("CompanyName"),
         ContactName = customer.Field<string>("ContactName"),
         ContactTitle = customer.Field<string>("ContactTitle")
     }).ToList();

dataGridView1.DataSource = query1;
```