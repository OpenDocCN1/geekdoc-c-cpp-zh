![](bbox=[0.2, 0.12, 0.8, 0.55])

Figure 14-1

> LINQ to Entities is beyond the scope of this book. It was slated to be released later in 2008 and is not part of Visual Studio 2008.

So how does your application view the LINQ-enabled data sources?

+   - In LINQ to Objects, the source data is made visible as an `IEnumerable<T>` or `IQueryable<T>` collection.
+   - In LINQ to XML, the source data is made visible as an `IEnumerable<XElement>`.
+   - In LINQ to DataSet, the source data is made visible as an `IEnumerable<DataRow>`.
+   - In LINQ to SQL, the source data is made visible as an `IEnumerable` or `IQueryable` of whatever custom objects you have defined to represent the data in the SQL table.

# LINQ to Objects

Let's start with LINQ to Objects. It enables you to use LINQ to directly query any `IEnumerable<T>` or `IQueryable<T>` collections (such as `string[]`, `int[]`, and `List<T>`) directly without needing to use an immediate LINQ provider or API such as the LINQ to SQL or LINQ to XML.

Say that you have a collection of data stored in an array, and you want to be able to retrieve a subset of the data quickly. In the old way of doing things, you write a loop and iteratively retrieve all the data that matches your criteria. That's time-consuming because you have to write all the logic to perform the