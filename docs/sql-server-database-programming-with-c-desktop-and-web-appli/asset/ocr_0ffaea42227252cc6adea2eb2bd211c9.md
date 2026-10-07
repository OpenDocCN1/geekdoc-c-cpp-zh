# Introduction to Language Integrated Query (LINQ)

# Data Source

![](bbox=[0.299, 0.116, 0.712, 0.413])

# Query

# Query Execution

**FIGURE 4.19** The running process of a LINQ query.

```
from [identifier] in [data source]
let [expression]
where [boolean expression]
order by [[expression]([ascending/descending)],[optionally repeat]
select [expression]
group [expression] into [expression]
```

**FIGURE 4.20** A typical query expression of LINQ query.

The query used in this example returns all the even numbers from the integer array. The query expression contains three clauses: **from**, **where** and **select**. If you are familiar with SQL, you will have noticed that the ordering of the clauses is reversed in SQL. The **from** clause specifies the data source, the **where** clause applies the filter, and the **select** clause specifies the type of returned elements. It returns no data. Now, the point is that in LINQ, the query variable itself takes no action and returns no data. It stores the information that is required to produce the results when the query is executed at some later point.

**The Query Execution** in this example is a deferred execution since all operator methods in this query are deferred operators (refer to Figure 4.4).

The **foreach** statement with an iteration variable `num` is used to fetch each item from the data source and assign it to the variable `num`. A Console.WriteLine() method is executed to display each received data item, and this query process will continue until all data items have been retrieved from the data source.

Because the query variable itself never holds the query results, you can execute it as often as you like. For example, you may have a database that is being updated continually by a separate application. In your application, you could create one query that retrieves the latest data, and you could execute repeatedly at some interval to retrieve different results every time.