Instead, you can use the query from Microsoft.FSharp.Linq.Query, found in the Microsoft.FSharp.PowerPack.dll assembly, and replace the previous query as follows:

```
query @seq {
  for o in db.Orders do
    if o.OrderDate = System.DateTime.Today
      && o.Customer.State = "CA" then
      yield o
  |> Seq.map (fun o -> o.Customer.LastName)
  |> Seq.sort @
```

Here, you used a sequence expression to build a sequence of orders that come from today in customers in CA, mapped and sorted this sequence using the standard Seq members. Above all, you wrapped this computation in a quotation and passed it to the query function.

The key part here is the use of the query function. This takes the quotation that describes what you want to do with the database — in this case, query for some orders, filter those that are interesting, translate that entire quotation into .NET 4.0 expression trees, and pass it to the LINQ run-time for SQL generation and execution.

As with direct LINQ queries in C# or VB, there is a possibility that the run-time conversion from expression trees to SQL queries fails, most often because you are using primitives that are not supported inside database queries.

# TABLE 25-19: Available Members in Database Queries

| MEMBER | MEMBER | MEMBER |
|---|---|--|
| Query.contains | Seq.filter | Seq.toArray |
| Query.groupBy | Seq.find | Seq.toList |
| Query.groupJoin | Seq.forall | |
| Query.join | Seq.head | |
| Query.max | Seq.length | |
| Query.minBy | Seq.map | |
| Seq.append | Seq.max | |
| Seq.average | Seq.min | |
| Seq.averageBy | Seq.sort | |
| Seq.collect | Seq.sortBy | |
| Seq.distinct | Seq.sum | |
| Seq.empty | Seq.sumBy | |
| Seq.exists | Seq.take | |