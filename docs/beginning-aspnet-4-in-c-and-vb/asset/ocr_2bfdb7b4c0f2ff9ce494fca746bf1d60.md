The following sections of this book make use of a Formula1 database where you can see the entities created from the designer in Figure 31-7.

![](bbox=[0.13, 0.2, 0.62, 0.48])

# FIGURE 31-7

Queries can be defined with the ObjectQuery<T> class, or the class that derives from it: ObjectSet<T>. Let's start with a simple query to access all Racer entities. The Racers property of the generated Formula1Entities class returns a ObjectSet<Racer>:

```
using (Formula1Entities data = new Formula1Entities(connection))
{
    ObjectSet<Racer> racers = data.Racers;
    Console.WriteLine(racers.CommandText);
    Console.WriteLine(racers.ToTraceString());
}
```

code snippet Formula1Demo/Program.cs

The Entity SQL statement that is returned from the CommandText property is shown here:

```
[Formula1Entities].[Racers]
```

And this is the generated SELECT statement to retrieve the records from the database that is shown by the ToTraceString() method:

```
SELECT
[Extent1].[Id] AS [Id],
[Extent1].[Firstname] AS [Firstname],
[Extent1].[Lastname] AS [Lastname],
[Extent1].[Country] AS [Country],
[Extent1].[Starts] AS [Starts],
[Extent1].[Wins] AS [Wins]
FROM [dbo].[Racers] AS [Extent1]
```

Instead of accessing the Racers property from the object context, you can also create a query with the CreateQuery() method:

```
ObjectQuery<Racer> racers = data.CreateQuery<Racer>("[Formula1Entities].[Racers]");
```

This is similar to using the Racers property.