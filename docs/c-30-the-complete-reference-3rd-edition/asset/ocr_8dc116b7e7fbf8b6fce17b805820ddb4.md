used to query data stored in an array, for example. It is no longer necessary to use SQL or any other non-C# mechanism. The query capability is fully integrated into the C# language.

In addition to using LINQ with SQL, LINQ can be used with XML files and ADO.NET Datasets. Perhaps equally important, it can also be used with C# arrays and collections (described in Chapter 24). Therefore, LINQ gives you a uniform way to access data. This is a powerful, innovative concept. It is not only changing the way that data is accessed, but it also offers a new way to think about and approach old problems. In the future, many programming solutions will be crafted in terms of LINQ. Its effects will not be limited to just database access.

LINQ is supported by a set of interrelated features, including the query syntax added to the C# language, lambda expressions, anonymous types, and extension methods. Lambda expressions are described in Chapter 15. The others are examined here.

# LINQ Fundamentals

At LINQ's core is the query. A query specifies what data will be obtained from a data source. For example, a query on a customer mailing list might request the addresses of all customers that reside in a specific city, such as Chicago or Tokyo. A query on an inventory database might request a list of out-of-stock items. A query on a log of Internet usage could ask for a list of the websites with the highest hit counts. Although these queries differ in their specifics, all can be expressed using the same LINQ syntactic elements.

After a query has been created, it can be executed. One way this is done is by using the query in a foreach loop. Executing a query causes its results to be obtained. Thus, using a query involves two key steps. First, the form of the query is created. Second, the query is executed. Therefore, the query defines what to retrieve from a data source. Executing the query actually obtains the results.

In order for a source of data to be used by LINQ, it must implement the IEnumerable interface. There are two forms of this interface: one generic, one not. In general, it is easier if the data source implements the generic version, IEnumerable<T>, where T specifies the type of data being enumerated. The rest of the chapter assumes that a data source implements IEnumerable<T>. This interface is declared in System.Collections.Generic. A class that implements IEnumerable<T> supports enumeration, which means that its contents can be obtained one at a time, in sequence. All C# arrays support IEnumerable<T>. Thus, arrays can be used to demonstrate the central concepts of LINQ. Understand, however, that LINQ is not limited to arrays.

# A Simple Query

At this point, it will be helpful to work through a simple LINQ example. The following program uses a query to obtain the positive values contained in an array of integers:

```
```csharp
// Create a simple LINQ query.
using System;
using System.Linq;

class SimpQuery {
    static void Main() {

        int[] nums = { 1, -2, 3, 0, -4, 5 };
```
```