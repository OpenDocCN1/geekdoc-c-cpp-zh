
would results such as this only if the calculations performed by the query take some time. I cheated a little by spinning the processor. Without this overhead, the parallel version of the query is actually slower than the serial version. In the next exercise, you'll see a LINQ query that joins two arrays in memory. This time, the exercise uses more realistic data volumes, so there's no need to slow down the query artificially.

# To parallelize a LINQ query that joins two collections

- 1. In Solution Explorer, open the Data.cs file in the Code and Text Editor window and locate the CustomersInMemory class. This class contains a public string array called Customers. Each string in the Customers array holds the data for a single customer, with the fields separated by commas. This format is typical of data that an application might read in a text file that uses comma-separated fields. The first field contains the customer ID, the second field contains the name of the company that the customer represents, and the remaining fields hold the address, city, country or postal code.

- 2. Find the OrdersInMemory class. This is similar to the CustomersInMemory class except that it contains a string array called Orders. The first field in each string is the order number, the second field is the customer ID, and the third field is the date that the order was placed.

- 3. Find the OrderInfo class. This class contains four fields: customer ID, company name, order ID, and order date for order. You'll use a LINQ query to populate a collection of OrderInfo objects from the data in the Customers and Orders arrays.

- 4. Display the Program.cs file in the Code and Text Editor window and locate the Test2 method in the Program class. In this method, you'll create a LINQ query that joins the Customers and Orders arrays by using the customer ID to retrieve a list of customers and the orders that each customer has placed for all orders placed in 1997. (This is antique data!) The query will store each row of the result in an OrderInfo object.

- 5. In the try block in this method, after the first // TO DO: comment, add the code shown next in bold:

# Click here to view code image

```c
// TO DO: Create a LINQ query that retrieves customers and
orders from arrays
// Store each row returned in an OrderInfo.As object
var orderInfoQuery =
    from c in CustomersInMemory.Customers.AsParallel()
    join o in OrdersInMemory.Orders.AsParallel()
    on c.Split(',')[0] equals o.Split(',')[1]
    where Convert.ToDateTime(o.Split(',')[2], new
    CultureInfo("en-US"))
    >= new DateTime(1997, 1, 1)
    && Convert.ToDateTime(o.Split(',')[2], new
    CultureInfo("en-US"))
    < new DateTime(1998, 1, 1)
    select new OrderInfo
{
    CustomerID = c.Split(',')[0],
    CompanyName = c.Split(',')[1],
    OrderID = Convert.ToInt32(o.Split(',')[0]),
    OrderDate = Convert.ToDateTime(o.Split(',')[2],
    new CultureInfo("en-US")
};
```

This statement defines the LINQ query. Notice that it uses the Split method of the String class to split each string into an array of strings. The strings are split on the comma character. (The commas are stripped out).

One complication is that the dates in the array are held in United States English format, so the code that converts them into DateTime objects specifies the United States English formatter. If you use the default formatter for your locale, the dates might not parse correctly. All in all, this query performs a significant amount of work to generate the data for each item.

- 6. In the Test2, after the second // TO DO statement, add the following code shown in bold:

# Click here to view code image

```csharp
// TO DO: Run the LINQ query, and save the results in a
List<OrderInfo> object
List<OrderInfo> orderInfo = new List<OrderInfo>
(orderInfoQuery);
```

This statement runs the query and populates the orderInfo collection.

- After the third // TO DO: statement, add the statement shown here in bold:

Click here to view code image

```csharp
// TO DO: Display the results
Console.WriteLine($"{orderInfo.Count} orders");
```

- In the Main menu, comment out the statement that calls Test1 method and uncomment the statement that calls the Test2 method, as shown in the following code in bold:

Click here to view code image

```csharp
static void Main(string[] args)
{
    // Test1();
    Test2();
}
```

- On the Debug menu, select Start Without Debugging.

- Verify Test2 retrieves 3,672 orders and note the duration of the test.

- Run the application several times to obtain an average duration, and then return to Visual Studio.

- In the Test2 method, modify the LINQ query to add the AsParallel extension method to the Customers and Orders arrays, as shown here in bold:

Click here to view code image

```csharp
var orderInfoQuery =
    from c in CustomersInMemory.Customers.AsParallel()
    join o in OrdersInMemory.Orders.AsParallel()
    on c.Split(',')[0] == o.Split(',')[1]
    where Convert.ToDateTime(o.Split(',')[2], new
    CultureInfo("en-US"))
    >= new DateTime(1997, 1, 1)
    && Convert.ToDateTime(o.Split(',')[2], new CultureInfo("en-US"))
    < new DateTime(1998, 1, 1)
    select new OrderInfo
{
  CustomerID = c.Split(',')[0],
  CompanyName = c.Split(',')[1],
  OrderID = Convert.ToInt32(o.Split(',')[0]),
  OrderDate = Convert.ToDateTime(o.Split(',')[2],
  new CultureInfo("en-US")
};
```

# Warning

When you join two data sources in this way, they must both be IEnumerable objects or ParallelQuery objects. This means that if you specify the AsParallel method for one source, you should also specify AsParallel for the other. If you fail to do this, your code will not run; it will stop with an error.

- Run the application several times. Notice that the time taken for Test2 should be significantly less than it was previously. On my system, the time dropped from an average of 440 ms to 250 ms. PLINQ can use multiple threads to optimize join operations by fetching the data for each part of the join in parallel.

- Close the application and return to Visual Studio.
These two simple exercises have shown you the power of the AsParallel extension method and PLINQ. Note that PLINQ is an evolving technology, and the internal implementation is very likely to change over time. Additionally, the volumes of data and the amount of processing you perform in a query affect the usefulness of PLINQ. With small amounts of data, PLINQ can actually impose a significant overhead. Therefore, you should not regard these exercises as defining fixed rules that you should always follow. Rather, they illustrate the point that you should carefully measure and assess the likely performance or other benefits of using PLINQ with your own data, in your own environment.

# Canceling a PLINQ query

Unlike with ordinary LINQ queries, you can cancel a PLINQ query. To do this, you specify a CancellationToken object from a CancellationTokenSource object and use the WithCancellation extension method of the ParallelQuery.

Click here to view code image

```csharp
CancellationToken tok = ...;
...
var orderInfoQuery =
    from c in
    CustomersInMemory.Customers.AsParallel().WithCancellation(tok)
    join o in OrdersInMemory.Orders.AsParallel()
    on ...
```

You specify WithCancellation only once in a query. Cancellation applies to all sources in the query. If the CancellationTokenSource used to generate the CancellationToken is canceled, the query stops with an OperationCanceled exception.

# Synchronizing concurrent access to data

PLINQ is not always the most appropriate technology to use for an application. If you create your own tasks manually, you need to ensure that these tasks coordinate their activities correctly. The .NET class library provides methods with which you can wait for tasks to complete, and you can use these methods to coordinate tasks at a very coarse level. But consider what happens if two tasks attempt to access and modify the same data. If both run at the same time, their overlapping operations might corrupt the data. This situation can lead to bugs that are difficult to correct, primarily because of their unpredictability.

The Task class provides a powerful framework with which you can design and build applications that take advantage of multiple CPU cores to perform tasks in parallel. However, you need to be careful when building solutions perform concurrent operations, especially if those operations are access to data. You have little control over how parallel operations are scheduled or even the degree of parallelism that the operating system might provide to an application constructed by using tasks. These decisions are left to
