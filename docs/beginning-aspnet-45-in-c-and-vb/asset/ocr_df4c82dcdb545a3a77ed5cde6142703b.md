a nice feature. If you don't need the extra Genre property in a specific page, you don't take the performance hit of selecting and returning these objects. If you do need them, all you need to add is a single call to Include.

Besides the Reviews collection the model also contains a Genres collection. When you want to select all the genres in the database, you can use this query:

```
VB.NET
Dim allGenres = From genre In myEntities.Genres
                Order By genre.Name
                Select genre
```

```
C#
var allGenres = from genre in myEntities.Genres
                orderby genre.Name
                select genre;
```

In addition to these two separate objects and their collections, both objects have properties that refer to each other's type. For example, a Review instance has a Genre property that provides additional information about the genre to which the review was assigned. A Genre instance in turn has a Reviews collection property, giving you access to all reviews posted in that genre. You see later how to make use of these properties.

From the keywords used in the first query in this Try It Out, it's probably easy to see what the query does: It gets a list of all the reviews in the system that have been authorized and orders them in descending order on their creation date. The result of the query is then assigned to the authorizedReviews variable. Notice that in both languages you can spread out the query over multiple lines to improve readability. This is not required, but you're encouraged to do it anyway because it makes your queries a lot easier to understand and maintain.

You may notice some strange syntax in the query. The VB.NET example doesn't use an As clause to define the type of the variable. Similarly, the C# snippet uses the var keyword, also without a type name. Although you may not conclude it from these code snippets, in both languages the variable authorizedReviews is still strongly typed and not just a variable with an undefined type.

> NOTE Strongly typed refers to the fact that the variable's type is explicitly defined when it's declared. Once you've defined the type for a variable (using Dim in VB or the type's name in C#) you cannot change it at run time. Strongly typed languages — such as C# and VB.NET — bring many advantages, including the ability to check the types being used at compile time, something that a weakly typed programming language cannot do.

Because the code didn't state the type for authorizedReviews (the example used Dim or var instead), .NET needs a different solution to determine the type. This is done by a concept called type inference, where the compiler is able to infer the type for a variable by looking at the right side of the assignment. In this case, the compiler sees that a list of Review objects will be returned from the query,