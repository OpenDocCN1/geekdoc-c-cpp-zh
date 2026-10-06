```
var q4 = from o in orders
from c in customers
where c.CustomerID == o.CustomerID
select new
{
    o.OrderNumber,
    c.LastName
};
```

```
foreach (var order in q4)
Console.WriteLine(
  "Customer: {0} Order Number: {1}",n  order.LastName.PadRight(9, ' '),
  order.OrderNumber);
```

# Output 4-12

Customer: Gottshall Order Number: Order 1
Customer: Gottshall Order Number: Order 2
Customer: Deane Order Number: Order 3
Customer: Deane Order Number: Order 4
Customer: Zeeman Order Number: Order 5

# One-to-One Join Performance Comparisons

Choosing the most appropriate join technique will yield large performance gains as collection size grows. To have some guidance on which technique makes sense, a simple experiment is necessary (results of such an analysis are summarized in Table 4-1). As mentioned earlier, a database management system (such as SQL Server, MySQL, and Oracle) should be used when joining large amounts of data, and although you can join in-memory using LINQ to Objects, you should exhaust other opportunities first if high performance on larger data sets is a requirement.

One-to one join performance is primarily dependent on how many different elements will need to be looked up from the inner sequence and how often that is necessary. The Join operator builds a lookup list of all inner sequence keys ahead of. If many of these keys are used in the outer sequence, this step aids performance; if only a few of the inner elements will ever be eventually looked up (because there are only a few