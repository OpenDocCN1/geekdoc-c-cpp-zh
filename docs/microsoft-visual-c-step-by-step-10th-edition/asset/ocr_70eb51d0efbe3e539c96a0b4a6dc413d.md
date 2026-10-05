```
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

+   Run the application several times. Notice that the time taken for Test2 should be significantly less than it was previously. On my system, the time dropped from an average of 440 ms to 250 ms. PLINQ can use multiple threads to optimize join operations by fetching the data for each part of the join in parallel.

+   Close the application and return to Visual Studio.
These two simple exercises have shown you the power of the AsParallel extension method and PLINQ. Note that PLINQ is an evolving technology, and the internal implementation is very likely to change over time. Additionally, the volumes of data and the amount of processing you perform in a query affect the usefulness of PLINQ. With small amounts of data, PLINQ can actually impose a significant overhead. Therefore, you should not regard these exercises as defining fixed rules that you should always follow. Rather, they illustrate the point that you should carefully measure and assess the likely performance or other benefits of using PLINQ with your own data, in your own environment.

# Canceling a PLINQ query