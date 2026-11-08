# Chapter 19

In Listing 19.9, the maximum value from the set of odd numbers is retrieved using the Max() method. This method is applied on a query variable that holds the query to get the list of odd numbers. Therefore, the Max() method gets the maximum odd value by iterating over the values of the odd numbers retrieved by the LINQ query.

Another approach that leads to an immediate execution of the query is by enforcing the query to be cached to an Array or List by using the ToArray() or ToList() method, respectively. Listing 19.10 shows an example of immediate execution by using the ToArray() method:

Listing 19.10: Showing an Example of Immediate Execution

```
```csharp
using System;
using System.Linq;

class Program
{
    public static void Main()
    {
        //Initializing data source
        int[] list = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

        //Query holds an object of type int[]
        var query = (from num in list
                     where num % 2 != 0
                     select num).ToArray();

        Console.WriteLine("The odd numbers are...");
        //Executing the query
        for (int i = 0; i < query.Length; i++)
        {
            Console.WriteLine(query[i]);
        }
    }
}
```
```

The preceding code is the modification of Listing 19.7 where we have executed the query immediately with the help of the ToArray() method. The output of the preceding example is given as follows:

```
```text
The odd numbers are...
1
3
5
7
9
```
```

Now, let’s discuss the area of usage of LINQ.

# Usage of LINQ

Microsoft has categorized LINQ into three distinct fields according to the area of implementation. These three fields are given as follows:

+   - LINQ to Object, where LINQ is used to query a set of objects or classes
+   - LINQ to XML, where LINQ is used to query XML
+   - LINQ to ADO.NET, where LINQ is used to query relational databases

In this section, we discuss all the three categories of LINQ implementation, in detail.