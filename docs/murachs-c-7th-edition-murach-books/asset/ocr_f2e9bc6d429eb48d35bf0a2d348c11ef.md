# Additional LINQ methods

| Method | Description |
|---|---|
| Count() | Gets the number of elements in the results of a query. |
| Average() | Calculates the average of an expression in the results of a query. |
| Sum() | Calculates the sum of an expression in the results of a query. |
| Max() | Gets the maximum value of an expression in the results of a query. |
| Min() | Gets the minimum value of an expression in the results of a query. |
| First() | Gets the first element from the results of a query. |
| FirstOrDefault() | Gets the first element from the results of a query or a default value if no element exists. |
| Single() | Gets the only element from the results of a query. Throws an exception if the results don’t contain exactly one element. |
| SingleOrDefault() | Gets the only element from the results of a query or a default value if no element exists. Throws an exception if the results contain more than one element. |
| Skip() | Skips over the specified number of elements in the results of a query and then returns the remaining elements. |
| Take() | Gets the specified number of elements from the beginning of the results of a query. |
| ToList() | Creates a List<T> object from the results of a query. |

# A query that gets a count of the items in the results

```
int invoiceCount = invoiceList
    .Where(i => i.InvoiceTotal > 150)
    .Count();
```

# A query that gets the invoice total for the items in the results

```
decimal invoiceTotal = invoiceList
    .Where(i => i.InvoiceDate >= DateTime.Parse("01/01/2020")
        & i.InvoiceDate <= DateTime.Parse("06/30/2020"))
    .Sum(i => i.InvoiceTotal);
```

# A query that gets a subset of the results

```
int skipCount = 20;
int takeCount = 10;
var invoices = invoiceList
    .Skip(skipCount)
    .Take(takeCount);
```

# Description

+   - LINQ provides other methods in addition to those that are used to implement the query operators. For a complete list of LINQ methods, see the online documentation for the Enumerable and Queryable classes.