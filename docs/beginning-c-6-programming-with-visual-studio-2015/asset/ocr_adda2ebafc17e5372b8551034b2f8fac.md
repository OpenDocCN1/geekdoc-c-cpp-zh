In the select clause, you project a new anonymous type whose properties are the total sales (calculated by referencing the cg result set) and the key value of the group, which you reference with the special group Key:

```
select new { TotalSales = cg.Sum(c => c.Sales), Region = cg.Key }
```

The group result set implements the LINQ IGrouping interface, which supports the Key property. You almost always want to reference the Key property in some way in processing group results, because it represents the criteria by which each group in your data was created.

You want to order the result in descending order by TotalSales field so you can see which region has the highest total sales, next highest, and so on. To do that, you create a second query to order the results from the group query:

```
var orderedResults =
    from cg in queryResults
    orderby cg.TotalSales descending
    select cg
;
```

The second query is a standard select query with an orderby clause, as you have seen in previous examples; it does not make use of any LINQ group capabilities except that the data source comes from the previous group query.

Next, you print out the results, with a little bit of formatting code to display the data with column headers and some separation between the totals and the group names:

```
WriteLine("Total\t: By\nSales\t: Region\n---\t---");
foreach (var item in orderedResults)
{
    WriteLine($"{item.TotalSales}\t: {item.Region}*");
};
```

This could be formatted in a more sophisticated way with field widths and by right-justifying the totals, but this is just an example so you don't need to bother — you can see the data clearly enough to understand what the code is doing.

# USING JOINS

A data set such as the customers and orders list you just created, with a shared key field (ID), enables a join query, whereby you can query related data in both lists with a single query, joining the results together with the key field. This is similar to the JOIN operation in the SQL data query language; and as you might expect, LINQ provides a join command in the query syntax, which you will use in the following Try It Out.

TRY IT OUT  Join Query: BegVCSharp_20_11_JoinQuery\Program.cs

Follow these steps to create the example in Visual Studio 2015:

+   1. Create a new console application called BegVCSharp_20_11_JoinQuery in the directory C:\BegVCSharp\Chapter20.