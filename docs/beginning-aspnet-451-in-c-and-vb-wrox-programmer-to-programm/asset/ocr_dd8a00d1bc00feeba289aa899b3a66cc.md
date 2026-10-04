Although the type is anonymous and cannot be accessed by name directly, the compiler is still able to infer the type, giving you full IntelliSense for the new properties that were selected in the query. Figure 14-4 shows how you access the properties of the anonymous type in the authorizedReviews variable, using the var keyword in C#.

![](bbox=[0.11, 0.19, 0.58, 0.35])

# FIGURE 14-4

Note that the preceding query accessed the actual Genre property of the Review. Besides its GenreId (defined as a column in the table Review in the database), the Review class also has a strongly typed Genre property, giving you direct access to the genre’s properties, like the Name, as the previous query demonstrates.

Besides directly selecting existing properties — as shown in the query that selected the Id and Title of the Review and the Name of the Genre — you can also make up property values and give them different names as you go. For example, the following query creates a new anonymous type that renames the Id as Number, limits the Title to the first 20 characters, and contains a boolean value that determines whether the item has been updated in the database previously:

# VB.NET

```
Dim allReviews = From myReview In myEntities.Reviews
    Select New With
    {
        .Number = myReview.Id,
        .Title = myReview.Title.Substring(0, 20),
        myReview.Genre.Name,
        .HasBeenUpdated = (myReview.UpdateDateTime > myReview.CreateDateTime)
    }
```

# C#

```
var allReviews = from myReview in myEntities.Reviews
select new
{
    Number = myReview.Id,
    Title = myReview.Title.Substring(0, 20),
    myReview.Genre.Name,
    HasBeenUpdated = (myReview.UpdateDateTime > myReview.CreateDateTime)
};
```