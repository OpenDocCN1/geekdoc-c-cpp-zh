10. Verify that Test2 retrieves 830 orders, and note the duration of the test. Run the application several times to obtain an average duration, and then return to Visual Studio.

11. In the Test2 method, modify the LINQ query and add the AsParallel extension method to the Customers and Orders arrays, as shown here in bold:

Click here to view code image

```
var orderInfoQuery = from c in
CustomersInMemory.Customers.AsParallel()
    join o in OrdersInMemory.Orders.AsParallel()
    on c.Split(',')[0] equals o.Split(',')[1]
    select new OrderInfo
    {
        CustomerID = c.Split(',')[0],
        CompanyName = c.Split(',')[1],
        OrderID = Convert.ToInt32(o.Split(',')
[0]),
        OrderDate =
Convert.ToDateTime(o.Split(',')[2],
            New CultureInfo("en-US"))
    };
```

# Warning

When you join two data sources in this way, they must both be IEnumerable objects or ParallelQuery objects. This means that if you specify the AsParallel method for one source, you should also specify AsParallel for the other. If you fail to do this, your code will not run—it will stop with an error.

12. Run the application several times. Notice that the time taken for Test2 should be significantly less than it was previously. PLINQ can make use of multiple threads to optimize join operations by fetching the data for each part of the join in parallel.

13. Close the application and return to Visual Studio.

These two simple exercises have shown you the power of the AsParallel extension method and PLINQ. Note that PLINQ is an evolving technology, and the internal implementation is very likely to change over time. Additionally, the volumes of data and the amount of processing you perform in a query also have a bearing on the effectiveness of using PLINQ. Therefore, you should not regard these exercises as defining fixed rules that you should always follow. Rather, they illustrate the point that you should carefully measure and assess the likely performance or other benefits of using PLINQ with your own data, in your own