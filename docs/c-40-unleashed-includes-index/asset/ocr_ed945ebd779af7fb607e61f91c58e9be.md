```
public static IQueryable<T> Where<T>(this IQueryable<T> source,
    Expression<Func<T, bool>> predicate)
{
    var where =
        Expression.Call(
            MethodInfo.GetCurrentMethod(), // in reality more complex
            source.Expression, // ask the source for its expression tree
            predicate
        );
    return source.Provider.CreateQuery<T>(where);
}
```

Other operators are implemented in a similar way. The essence of this code is to stitch together the expression tree that represents the source used for the operator (which by itself can be the result of a query operator call preceding it) and all the arguments passed to the operator. In this case, the only argument is a predicate lambda expression, which gets passed in from the compiled query expression code that generates an expression tree. After Queryable has stitched together all those expression trees into a bigger one, representing the method call to the operator method, it hands over the new tree to the IQueryProvider object exposed on the IQueryable source object:

```
public interface IQueryProvider
{
    IQueryable<TElement> CreateQuery<TElement>(Expression expression);
    ...
}
```

Figure 20.22 illustrates all the steps involved in constructing the expression tree for a where clause in an IQueryable-based query expression.

This process continues until all query operators have been called at the declaration site of a query. The end result is a single IQueryable object with an expression tree inside it, capturing the whole query expression with all the used operators in the right order and with information about the passed (potentially functional) arguments. Figure 20.23 illustrates the result of this runtime tree stitching on a whole query, assuming the source object is an IQueryable<T> and the Queryable extension methods are getting called as a result.

Because every IQueryable object is also IEnumerable, the GetEnumerator method used by a request to iterate over the results of the query (for example, using foreach) can inspect this big expression tree and turn it into the query language targeted by the query provider. How precisely this translation works requires deeper coverage of expression trees and is beyond the scope of this book. For more information about the subject of writing your own LINQ providers, search the Web on the topic.