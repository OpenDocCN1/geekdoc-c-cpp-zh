the myEntities variable holds a (scarce) connection to the SQL Server database, it's a good idea to wrap the code that uses it in a Using block, so the object is destroyed at the end of the block and the connection is released. This myEntities object then exposes your data (such as reviews and genres) that you can use in a query:

# VB.NET

```
Using myEntities As New PlanetWroxEntities()
    Dim authorizedReviews = From review In myEntities.Reviews
        Where review.Authorized = True
        Order By review.CreateDateTime Descending
        Select review
    ...
End Using
```

# C#

```
using (PlanetWroxEntities myEntities = new PlanetWroxEntities())
{
    var authorizedReviews = from review in myEntities.Reviews
        where review.Authorized == true
        orderby review.CreateDateTime descending
        select review;
    ...
}
```

Note that this query looks similar to the SQL that you learned in the previous chapters. Under the hood, the run time converts this LINQ query into its SQL counterpart and executes it against the underlying database. Within this query, the variable review in the From clause is used to refer to the review in the other parts of the query (Where, Order By, and Select), enabling you to specify the select, filter, and ordering criteria.

What's important to realize is that EF uses a mechanism called lazy loading, which means sub objects are not loaded until you explicitly tell them to. What this means is that in the previous example the Genre properties of the Review objects you've queried are null in C# and Nothing in VB.NET and don't contain any data. As soon as your code tries to access them, they are loaded by executing another query to the database. This can greatly improve performance if you don't need these sub objects. However, if you're sure you need them in your code beforehand, executing a separate SQL statement for each item results in a lot of overhead. In that case, you can preload the objects with the initial query. To express that you want to include these objects as well, you use the Include method for the types you want to query:

# VB.NET

```
Dim authorizedReviews = From review In myEntities.Reviews.Include("Genre")
    Where review.Authorized = True
    ...
```

# C#

```
var authorizedReviews = from review in myEntities.Reviews.Include("Genre")
    where review.Authorized == true
    ...
```

With this addition to the query, the Review objects now have their Genre property correctly filled with data. Though this may seem a little counterintuitive and counterproductive at first, it's actually quite