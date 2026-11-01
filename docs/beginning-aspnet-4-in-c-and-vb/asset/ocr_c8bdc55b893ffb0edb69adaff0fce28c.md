The following sections are examples of using these operators.

# Filtering

Have a look at some examples for a query.

With the where clause, you can combine multiple expressions; for example, get only the racers from Brazil and Austria who won more than 15 races. The result type of the expression passed to the where clause just needs to be of type bool:

```
```csharp
var racers = from r in Formula1.GetChampions()
    where r.Wins > 15 &&
        (r.Country == "Brazil" || r.Country == "Austria")
    select r;

foreach (var r in racers)
{
    Console.WriteLine("{0:A}", r);
}
```
```

code snippet Enumerablesample/Program.cs

Starting the program with this LINQ query returns Niki Lauda, Nelson Piquet, and Ayrton Senna as shown:

```
```
Niki Lauda, Austria, Starts: 173, Wins: 25
Nelson Piquet, Brazil, Starts: 204, Wins: 23
Ayrton Senna, Brazil, Starts: 161, Wins: 41
```
```

Not all queries can be done with the LINQ query. Not all extension methods are mapped to LINQ query clauses. Advanced queries require using extension methods. To better understand complex queries with extension methods, it's good to see how simple queries are mapped. Using the extension methods Where() and Select() produces a query very similar to the LINQ query done before:

```
```csharp
var racers = Formula1.GetChampions().
    Where(r => r.Wins > 15 &&
        (r.Country == "Brazil" || r.Country == "Austria")).
    Select(r => r);
```
```

# Filtering with Index

One example where you can't use the LINQ query is an overload of the Where() method. With an overload of the Where() method you can pass a second parameter that is the index. The index is a counter for every result returned from the filter. You can use the index within the expression to do some calculation based on the index. Here the index is used within the code that is called by the Where() extension method to return only racers whose last name starts with A if the index is even:

```
```csharp
var racers = Formula1.GetChampions().
    Where((r, index) => r.LastName.StartsWith("A") && index % 2 != 0);
foreach (var r in racers)
{
    Console.WriteLine("{0:A}", r);
}
```
```

All the racers with last names beginning with the letter A are Alberto Ascari, Mario Andretti, and Fernando Alonso. Because Mario Andretti is positioned within an index that is odd, he is not in the result:

```
```
Alberto Ascari, Italy; starts: 32, wins: 10
Fernando Alonso, Spain; starts: 132, wins: 21
```
```