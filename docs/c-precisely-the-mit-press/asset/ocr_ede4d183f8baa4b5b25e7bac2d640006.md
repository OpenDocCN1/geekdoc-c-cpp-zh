194 Linq, Language Integrated Query (C# 3.0)

# 28 Linq, Language Integrated Query (C# 3.0)

Linq, or Language Integrated Query, is a framework for declarative processing of collections of data, a general query language embedded in C#. The Linq query syntax (section 28.1) is syntactic sugar for calls to extension methods on appropriate interfaces, such as IEnumerable<T> (section 28.5) and IQueryable<T>. Thus the same Linq expression can be used on in-memory enumerables (and collections), on in-memory XML data, on relational databases, and even on user-defined data types.

# 28.1 Linq Expressions (C# 3.0)

This section focuses on queries for enumerables, so that the streams xs and ys are enumerables or collections. The queries could be made on relational databases, in which case xs and ys would be database tables, the result of previous queries. In any case, the result of a query implements at least IEnumerable<T> for some type T and therefore may be enumerated using the foreach statement (section 13.6.2).

# 28.1.1 Query Expressions

A query-expression must begin with the phrase from x in xs ... which introduces a range variable x that denotes a single item from the stream xs. There are two kinds of Linq query expressions. The first kind of query-expression generates a stream of items, each obtained by evaluating expression e for each combination of range variables. The result has type IEnumerable<>, where t is the type of e:

```
from x in xs
query-body-clauses
select e
```

The second kind of query-expression generates a group of items, where each group of those items (that is, value of e1) that have the same key (value of e2). The result has type IEnumerable<Grouping<t2,t>>, where t1 is the type of e1 and t2 is the type of e2:

```
from x in xs
query-body-clauses
group e1 by e2
let y = e
where b
join y in ys on e1 equals e2
join y in ys on e1 equals e2 into z
orderby e1, e2, ...
```

In both cases, a query-body-clause is one of these possibilities (section 28.1.2):

Moreover, to further process the result of a query-expression, it may be followed by any number of querycontinuations (section 28.1.3).