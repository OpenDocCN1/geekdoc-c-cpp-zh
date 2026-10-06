# HOW TO JOIN WITH DATA IN ANOTHER SEQUENCE 115

equal or a custom IComparer can be supplied to customize this equality comparison in the same way a custom equality comparer was used in the grouping examples in the “Specifying Your Own Key Comparison Function” section earlier in this chapter.

Using the extension method syntax for joins is almost never required (almost never—if you need a custom equality comparer, you have no choice). To demonstrate how a join/into query expression maps to the equivalent extension method syntax code, the following code is function-ally equivalent to that shown in Listing 4-17:

```
var qla = customers
  GroupJoin(
    orders,
    c => c.CustomerID,
    (c, o) => new
    {
      LastName = c.LastName,
      Orders = o
    }
  );
```

# One-to-Many Join Using a Subquery

A subquery in a query's select projection can achieve a one-to-many join. If targeting a single record (or a small number, less than five outer records), this technique performs adequately and is easy to read. Listing 4-18 demonstrates using a subquery for a one-to-many join, and this code produces the Console output shown in Output 4-14.

Listing 4-18 One-to-Many Join using a subquery in the select projection—see Output 4-14

```
var customers = Customer.SampleData();
var orders = Order.SampleData();
```

```
var q2 = from c in customers
  select new
  {
    LastName = c.LastName,
    Orders = from o in orders
      where o.CustomerID == c.CustomerID
    select o
```