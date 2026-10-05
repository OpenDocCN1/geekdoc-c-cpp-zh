# Click here to view code image

```
// TO DO: Create a LINQ query that retrieves customers and
orders from arrays
// Store each row returned in an OrderInfo.As object
var orderInfoQuery =
    from c in CustomersInMemory.Customers.AsParallel()
    join o in OrdersInMemory.Orders.AsParallel()
    on c.Split(',')[0] equals o.Split(',')[1]
    where Convert.ToDateTime(o.Split(',')[2], new
    CultureInfo("en-US")
    >= new DateTime(1997, 1, 1)
    && Convert.ToDateTime(o.Split(',')[2], new
    CultureInfo("en-US")
    < new DateTime(1998, 1
{
    CustomerID = c.Split(',')[0],
    CompanyName = c.Split(',')[1],
    OrderID = Convert.ToInt32(o.Split(',')[0]),
    OrderDate = Convert.ToDateTime(o.Split(',')[2],
    new CultureInfo("en-US")
}
```

This statement defines the LINQ query. Notice that it uses the Split
method of the String class to split each string into an array of strings. The
strings are split on the comma character. (The commas are stripped out).

One complication is that the dates in the array are held in United States
English format, so the code that converts them into DateTime objects
specifies the United States English formatter. If you use the default
formatter for your locale, the dates might not parse correctly. All in all,
this query performs a significant amount of work to generate the data for
each item.

+   6. In the Test2, after the second // TO DO statement, add the
following code shown in bold:

# Click here to view code image

```
// TO DO: Run the LINQ query, and save the results in a
List<OrderInfo> object
List<OrderInfo> orderInfo = new List<OrderInfo>
(orderInfoQuery);
```