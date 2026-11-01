```
}
    Console.ReadLine();
}
}
```

code download ConsoleApplication1.sln

This example is pulling from the Customers table and joining on the Orders table where the CustomerID columns match. This is done through the join statement:

```
join o in dc.Orders on c.CustomerID equals o.CustomerID
```

From here, a new object is created with the select new statement and this new object comprises of the CustomerID, CompanyName, and Country columns from the Customer table as well as the OrderID and OrderDate columns from the Orders table.

When it comes to iterating through the collection of this new object, the interesting part is that the foreach statement also uses the var keyword because the type is not known at this point in time:

```
foreach (var item in query)
{
    Console.WriteLine(item.CustomerID + " | " + item.CompanyName
        + " | " + item.Country + " | " + item.OrderID
        + " | " + item.OrderDate);
}
```

Regardless, the item object here has access to all the properties that you specified. When you run this example, you will get results similar to what is presented in this partial result:

```
WILMK | Wilman Kala | Finland | 10695 | 10/7/1997 12:00:00 AM
WILMK | Wilman Kala | Finland | 10615 | 7/30/1997 12:00:00 AM
WILMK | Wilman Kala | Finland | 10673 | 9/18/1997 12:00:00 AM
WILMK | Wilman Kala | Finland | 11005 | 4/7/1998 12:00:00 AM
WILMK | Wilman Kala | Finland | 10870 | 2/10/1998 12:00:00 AM
WILMK | Wilman Kala | Finland | 10873 | 2/6/1998 12:00:00 AM
WILMK | Wilman Kala | Finland | 10910 | 2/26/1998 12:00:00 AM
```

# Grouping Items

You are also easily able to group items with your queries. In the Northwind.dbml example that you are working with, drag and drop the Categories table onto the design surface and you will see that there is a relation with this table and the Products table from earlier. The following example shows you how to group products by categories:

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
                        orderby p.Category.CategoryName ascending
                        group by p.Category.CategoryName into g
                        select new { Category = g.Key, Products = g};

            foreach (var item in query)
            {
```