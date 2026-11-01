```
where c.City == city
select c
);
```

Having a compiled query return an IEnumerable forces any composition done with a compiled query to be done in the application memory after the original query has already been executed instead of modifying the original compiled query before sending it to the database server. If the amount of data returned by the query is small, this approach can yield better performance. On the other hand, if the query returns a large volume of data and requires a lot of post-processing, it might be faster to take a hit on query preparation but let the database server do the heavy lifting instead. You need to measure actual performance to make a good implementation choice.

# Extension Methods

C# and Visual Basic syntax covers only a subset of the query operators supported by the Entity Framework. To take full advantage of its querying capabilities, you might need to use one or more of the LINQ extension methods defined in the static class Queryable from the System.Linq namespace. Here is a typical LINQ query, which should look familiar by now:

```
var customers = from c in context.Customers
where c.City == "London"
select c;
```

.NET CLR has no special IL instructions for LINQ keywords. Instead, the compiler converts the LINQ syntax into lambda expressions and calls to LINQ extension methods. Here is how this code can be rewritten using extension methods explicitly:

```
var customers = context.Customers
    .Where(c => c.City == "London")
    .Select(c => c);
```

Notice how instead of the where keyword, it's the Where extension method.

c => c.City == "London" is a lambda expression that takes c, an instance of the Customer class, as a parameter and returns a Boolean value that indicates whether a particular customer matches the filter criteria. Where is an extension method defined in the Queryable class for the IQueryable interface. In other words, Queryable.Where takes an IQueryable interface as its first parameter and, in essence, extends the IQueryable interface by adding a Where method to it, hence the term "extension method."

```
public static IQueryable<TSource> Where<TSource>(
    this IQueryable<TSource> source,
    Expression<Func<TSource, bool>> predicate)
```

You can think of lambda expressions as a kind of shorthand version of anonymous delegates—a compact way of declaring small functions. However, when used with IQueryable,