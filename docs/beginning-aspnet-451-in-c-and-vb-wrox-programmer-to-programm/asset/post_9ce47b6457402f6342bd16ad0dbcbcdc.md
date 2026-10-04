
By calling DataBind() on the GridView you instruct the control to display the individual Review objects on the page. Because the GridView control's AutoGenerateColumns property is True by default, the control creates a column for each property it finds on the Review object. Later you see how to customize the control and the data that is assigned to the DataSource property. Note the call to List at the end of the query. This causes an immediate execution of the query against the database, which results in the variable authorizedReviews pointing to all the reviews that matched the where. You need to do this when you bind the results of a query to the data control as the GridView. However, in many cases you don't need List, as you'll see throughout this chapter.

## INTRODUCING QUERY SYNTAX

The query you saw in the previous example is quite simple; it requests all the reviews from the system and returns them in sorted order. However, the querying capabilities of LINQ are much more powerful than this. In the following section you learn more about LINQ query syntax that you use to query your object. Remember, LINQ syntax is not invented for Entity Framework. Most of the LINQ concepts that follow can also be used in the other LINQ implementations, such as LINQ to Objects and LINQ to ADO.NET.

## Standard Query Operators

LINQ supports a large number of query operators — keywords that enable you to select, order, or filter data that is returned from the query. Although all the examples are discussed in the context of EF, you can easily apply them to the other LINQ implementations as well. In the following section you get an overview of the most important query operators, each followed by an example.

## Select

The Select keyword (select in C#) is used to retrieve objects from the source. In this example you see how to select an object of existing type. Later in the chapter you see how to define new objects on the fly.

```vb.NET
Dim allReviews = From r in myEntities.Reviews
Select r
```

```c#
var allReviews = from r in myEntities.Reviews
select r;
```

## From

Although not considered a standard query operator — because it doesn't operate on data — the From clause (from in C#) is an important element in the LINQ query, because it defines the source that the query must act upon. In the previous example, the From clause indicates that the query must be executed against the Reviews collection that is exposed by the myEntities object in EF.

## Order By

With Order (orderby in C#, VB.NET uses) you can sort the items in the result collection. Order By is followed by an optional Ascending or Descending (ascending and descending in C#) keyword to sort order. You can specify multiple criteria by separating them with a comma. The following query returns a list of genres, first sorted by SortOrder in descending order, then Name in ascending order (the default):

```vb.NET
dim allGenres = From g In myEntities.Genres
Order By g.SortOrder descending, g.Name
Select g
```

```c#
var allGenres = from g in myEntities.Genres
orderby g.SortOrder descending, g.Name
select g;
```

## Where

Just like the WHERE clause in SQL, the Where clause in LINQ (where in C#) enables you to filter the objects returned by the query. The following query returns all authorized reviews:

```vb.NET
Dim authorizedReviews = From r In myEntities.Reviews
Where r.Authorized = True
Select r
```

```c#
var authorizedReviews = from r in myEntities.Reviews
where r.Authorized == true
select r;
```

Note that the Where clause uses the language's standard equality operator: a single equals (=) in VB.NET and two of them in C#.

## Sum, Min, Max, Average, and Count

These aggregation operators enable you to perform mathematical calculations on the objects in the result set. For example, to retrieve the number of reviews, you can execute this query:

```vb.NET
Dim numberOfReviews = (From r in MyEntities.Reviews
Select r).Count()
```

```c#
var numberOfReviews = (from r in myEntities.Reviews
select r).Count();
```

Note that the Count method is applied to the result set. Therefore, you need to wrap the entire statement in parentheses by a call to Count. Without the parentheses you'll get an error. The numberOfReviews variable in this example will be inferred as an integer and contains the number of items in the Review table.

## Take, Skip, TakeWhile, and SkipWhile

Take and Skip enable you to manage sub-sections within the result set. This is ideal for paging scenarios where only the elements for the current page are retrieved. Take gets the requested number of elements from the result set and ignores the rest, whereas Skip ignores the requested number of elements and returns the rest.

Within EF, the Take and Skip operators are translated to SQL statements as well. This greatly enhances the performance of the query, especially with large result sets, because not all elements have to be transferred from the database to the ASP.NET page.

For Skip to work in LINQ to Entities, you must add an Order clause (orderby in C#) to your query to sort the results before the designated number of rows are skipped. Databases may return results in an unpredictable order if you don't add an Order By statement. The following example shows how to retrieve the page, given a size of 10:

```vb.NET
Dim scoreReviews = (From r in MyEntities.Reviews
Order By r.Title
Select r).Skip(10).Take(10)
```

```c#
var scoreReviews = (from r in myEntities.Reviews
orderby r.Title
select r).Skip(10).Take(10);
```

The TakeWhile and SkipWhile operators work in a similar fashion, enable you to take or skip items while a specific condition is true. Unfortunately, they don't work in EF, but you can usually work around that by adding a simple Where clause.

## Single and SingleOrDefault

The Single and SingleOrDefault operators enable you to return a single object as a typed instance. This is useful if you know your query returns exactly one; for example, when you retrieve it by its unique ID. The following example retrieves the review with an Id of 37:

```vb.NET
Dim review37 = (From r In MyEntities.Reviews
Where r.Id = 37
Select r).Single()
```

```c#
var review37 = (from r in myEntities.Reviews
where r.Id == 37
select r).Single();
```

The Single operator raises an exception when the requested item is not found or if the query returns more than one. If you want the method to return null (Nothing in VB.NET) — for example, for a Review or Genre that is not found — the default value for the relevant data type (such as a 0 for Integer, False for a Boolean, and so on), use SingleOrDefault.

## First, FirstOrDefault, Last, and LastOrDefault

These operators enable you to return the first or the last element in a specific sequence of objects. Just as with the Single method, First and Last throw an error when the collection is empty, whereas the other return the default value for the relevant data types.

In contrast to Single, the First, FirstOrDefault, Last, and LastOrDefault operators don't throw an exception when the query returns more than one. They return the first item in the result set.

The Last and LastOrDefault queries are not supported in EF. However, you can easily accomplish the same behavior with First and descending sort order. The following code snippet shows how to retrieve the oldest (the one with the lowest ID) and the most recent review from the database:

```vb.NET
Dim firstReview = (From r In MyEntities.Reviews
                    Order By r.Id
                    Select r.First())
```

```vb.NET
Dim lastReview = (From r In MyEntities.Reviews
                    Order By r.Id Descending
                    Select r.First())
```
