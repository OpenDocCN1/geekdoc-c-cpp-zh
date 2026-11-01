
Now it would be interesting to filter the racers based on a condition. This can be done by using the Where() method of the ObjectQuery<T> class. Where() is one of the Query Builder methods that create Entity SQL. This method requires a predicate as a string, and optional parameters of type ObjectParameter. The predicate shown here specifies that only the racers from Brazil are returned. The it specifies the item of the result and Country is the column. The first parameter of the ObjectParameter constructor references the @Country parameter of the predicate, but doesn't list the @ sign:

```
string country = "Brazil";
ObjectQuery<Racer> racers = data.Racers.Where("it.Country = @Country",
    new ObjectParameter("Country", country));
```

The magic behind it can be seen immediately by accessing the CommandText property of the query. With Entity SQL, SELECT VALUE it declares it to access the columns:

```
SELECT VALUE it
FROM (
[Formula1Entities].[Racers]
) AS it
WHERE
it.Country = @Country
```

The method ToTraceString() shows the generated SQL statement:

```
SELECT
[Extent1].[Id] AS [Id],
[Extent1].[Firstname] AS [Firstname],
[Extent1].[Lastname] AS [Lastname],
[Extent1].[Country] AS [Country],
[Extent1].[Starts] AS [Starts],
[Extent1].[Wins] AS [Wins]
FROM [dbo].[Racers] AS [Extent1]
WHERE [Extent1].[Country] = @Country
```

Of course, you can also specify the complete Entity SQL:

```
string country = "Brazil";
ObjectQuery<Racer> racers = data.CreateQuery<Racer>(
    "SELECT VALUE it FROM [Formula1Entities].[Racers] AS " +
    "it WHERE it.Country = @Country",
    new ObjectParameter("Country", country));
```

The class ObjectQuery<T> offers several Query Builder methods as explained in the following table. Many of these methods are very similar to the LINQ extension methods that you learned about in Chapter 11, “Language Integrated Query.” An important difference with the methods here is that instead of parameters of type delegate or Expression<T>, the parameter type with ObjectQuery<T> is usually of type string.

| OBJECTQUERY<T> QUERY BUILDER METHODS | DESCRIPTION |
|---|---|
| Where() | This method allows you to filter the results based on a condition. |
| Distinct() | This method creates a query with unique results. |
| Except() | This method returns the result without the items that meet the condition with the except filter. |
| GroupBy() | This method creates a new query to group entities based on a specified criteria. |
| Include() | With relations, you saw earlier that related items are delay loaded. It is required to invoke the Load() method of the EntityCollection<T> class to get related entities into the object context. Instead of using the Load() method, you can specify a query with the Include() method to eager-fetch related entities. |
| OfType() | This method specifies to return only those entities of a specific type. This is very helpful with TPH relations. |
| OrderBy() | This method is for defining the sort order of the entities. |
| Select() SelectValue() | These methods return a projection of the results. Select() returns the result items in the form of a DbDataRecord; SelectValue() returns the values as scalars or complex types as defined by the generic parameter TResultType. |
| Skip() Top() | These methods are useful for paging. Skip a number of items with the Skip() method and take a specified number as defined by the Top() method. |
| Intersect() Union() UnionAll() | These methods are used to combine two queries. Intersect() returns a query containing only the results that are available in both of the queries. Union() combines the queries and returns the complete result without duplicates. UnionAll() also includes duplicates. |

Let's get into one example on how to use these Query Builder methods. With the next code snippet, the racers are filtered with the Where() method to return only racers from the USA; the OrderBy() method specifies descending sort order first based on the number of wins and next on the number of starts. Finally, only the first three racers are in the result using the Top() method:

```
using (var data = new Formula1Entities())
{
    string country = "USA";
    ObjectQuery<Racer> racers = data.Racers.Where("it.Country = @Country",
        new ObjectParameter("Country", country))
        .OrderBy("it.Wins DESC, it.Starts DESC")
        .Top("3");
    foreach (var racer in racers)
    {
        Console.WriteLine("{0} {1}, wins: {2}, starts: {3}",
            racer.Firstname, racer.Lastname, racer.Wins, racer.Starts);
    }
}
```

code snippet Formula1Demo/Program.cs

This is the result from this query:

```
Mario Andretti, wins: 12, starts: 128
Dan Gurney, wins: 4, starts: 87
Phil Hill, wins: 3, starts: 48
```

## UPDATES

Reading, searching, and filtering data from the store are just one part of the work that usually needs to be done with data-intensive applications. Writing changed data back to the store is the other part you need to know.

The sections that follow cover these topics:

- Object tracking
- Change information
- Attaching and detaching entities
- Storing entity changes

## Object Tracking

To allow data read from the store to be modified and saved, the entities must be tracked after they are loaded. This also requires that the object context be aware if an entity has already been loaded from the store. If multiple queries are accessing the same records, the object context needs to return already loaded entities.

The ObjectStateManager is used by the object context to keep track of entities that are loaded into the context.

The following example demonstrates that indeed if two different queries are done that return the same record from the database, the state manager is aware of that and does not create a new entity. Instead, the same entity is returned. The ObjectStateManager instance that is associated with the object context can be accessed with the ObjectStateManager property. The ObjectStateManager class defines an event named ObjectStateManagerChanged that is invoked every time a new object is added or removed from the object context. Here, the method ObjectStateManager_ObjectStateManagerChanged is assigned to the event to get information about changes.

Two different queries are used to return an entity object. The first query gets the first racer from the country Austria with the last name Lauda. The second query asks for the racers from Austria, sorts the racers by the number of races won, and gets the first result. As a matter of fact, that's the same racer. To verify that the same entity object is returned, the method Object.ReferenceEquals() is used to verify whether the two object references indeed reference the same instance:

```
private static void TrackingDemo()
{
    using (var data = new Formula1Entities())
    {
        data.ObjectStateManager.ObjectStateManagerChanged +=
            ObjectStateManager_ObjectStateManagerChanged;

        Racer niki1 = data.Racers.Where("it.Country='Austria' && it.Lastname='Lauda'").First();

        Racer niki2 = data.Racers.Where("it.Country='Austria'").OrderBy("it.Wins DESC").First();
        if (Object.ReferenceEquals(niki1, niki2))
        {
            Console.WriteLine("the same object");
        }
    }
}

static void ObjectStateManager_ObjectStateManagerChanged(object sender,
    CollectionChangeEventArgs e)
{
    Console.WriteLine("Object State change - action: {0}", e.Action);
    Racer r = e.Element as Racer;
    if (r != null)
        Console.WriteLine("Racer {0}", r.Lastname);
}
```

code snippet Formula1Demo/Program.cs

Running the application, you can see that the event of the ObjectStateManagerChanged of the ObjectStateManager occurs only once, and the references niki1 and niki2 are indeed the same:

```
Object State change – action: Add
Racer Lauda
The same object
```

## Change Information

The object context is also aware of changes with the entities. The following example adds and modifies a racer from the object context and gets information about the change. First, a new racer is added with the AddObject() method of the ObjectSet<T> class. This method adds a new entity with the EntityState.Added information. Next, a racer with the Lastname Alonso is queried. With this entity class, the Starts property is incremented and thus the entity is marked with the information EntityState.Modified. Behind the scenes, the ObjectStateManager is informed about a state change in the object based on the interface implementations INotifyPropertyChanged. This interface is implemented in the entity base class StructuralObject. The ObjectStateManager is attached to the PropertyChanged event, and this event is fired with every property change.

To get all added or modified entity objects, you can invoke the GetObjectStateEntries() method of the ObjectStateManager and pass an EntityState enumeration value as it is done here. This method returns a collection of ObjectStateEntry objects that keeps information about the entities. The helper method DisplayState through this collection to give detail information.

You can also get state information about a single entity passing the EntityKey to the GetObjectStateEntry() method. The EntityKey property is available with entity objects implementing the interface IEntityWithKey, which is the case with the base class EntityObject. The ObjectStateEntry object returned offers the method GetModifiedProperties() where you can read all property values that have been changed, and also access the original and the current information about the properties with the OriginalValues and CurrentValues indexers:

```
```csharp
private static void ChangeInformation()
{
    using (var data = new Formula1Entities())
    {
        var jaime = new Racer
        {
            Firstname = "Jaime",
            Lastname = "Alguersuari",
            Country = "Spain",
            Starts = 0
        };
        data.Racers.AddObject(jaime);
        Racer fernando = data.Racers.Where("it.Lastname='Alonso'").First();
        fernando.Starts++;
        DisplayState(EntityState.Added.ToString(),
            data.ObjectStateManager.GetObjectStateEntries(EntityState.Added));
        DisplayState(EntityState.Modified.ToString(),
            data.ObjectStateManager.GetObjectStateEntries(EntityState.Modified));
        ObjectStateEntry stateOfFernando =
            data.ObjectStateManager.GetObjectStateEntry(fernando.EntityKey);
        Console.WriteLine("state of Fernando: {0}",
            stateOfFernando.State.ToString());
        foreach (string modifiedProp in stateOfFernando.GetModifiedProperties())
        {
            Console.WriteLine("modified: {0}", modifiedProp);
            Console.WriteLine("original: {0}",
                stateOfFernando.OriginalValues[modifiedProp]);
            Console.WriteLine("current: {0}",
                stateOfFernando.CurrentValues[modifiedProp]);
        }
    }
}
static void DisplayState(string state, IEnumerable<ObjectStateEntry> entries)
{
    foreach (var entry in entries)
    {
```
