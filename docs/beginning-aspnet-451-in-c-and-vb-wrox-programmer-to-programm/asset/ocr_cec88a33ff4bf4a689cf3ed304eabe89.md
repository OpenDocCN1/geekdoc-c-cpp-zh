496 | CHAPTER 14 LINQ AND THE ADO.NET ENTITY FRAMEWORK

The r variable in this example is referred to as a range variable that is only available within the current query. Typically introduce the range variable in the From clause, and use it again in the Where and Select clauses to filter the data and to indicate the data you want to select. Although you can choose any name you like, you often see single-letter variables like the r (for Review) or you see the singular form of the collection you are querying (review instead of r in the preceding examples).

# From

Although not considered a standard query operator — because it doesn't operate on the data points to the data — the From clause (from in C#) is an important element in a LINQ query, because it defines the data or source that the query must act upon. In the previous example, the From clause indicates that the query must be executed against the Reviews collection that is exposed by the myEntities object in EF.

# Order By

With Order (orderby in C#, without the space VB.NET uses) you can sort the items in the result collection. Order By is followed by an optional Ascending or Descending (ascending and descending in C#) keyword to sort order. You can specify multiple criteria by separating them with a comma. The following query returns a list of genres, first sorted by SortOrder in descending order, the following query named Named in ascending order (the default):

```
VB.NET
dim allGenres = From g In myEntities.Genres
Order By g.SortOrder descending, g.Name
Select g
```

```
C#
var allGenres = from g in myEntities.Genres
orderby g.SortOrder descending, g.Name
select g;
```

# Where

Just like the WHERE clause in SQL, the Where clause in LINQ (where in C#) enables you to filter the objects returned by the query. The following query returns all authorized reviews:

```
VB.NET
Dim authorizedReviews = From r In myEntities.Reviews
Where r.Authorized = True
Select r
```

```
C#
var authorizedReviews = from r in myEntities.Reviews
where r.Authorized == true
select r;
```

Note that the Where clause uses the language's standard equality operator: a single equals (=) in VB.NET and two of them in C#.