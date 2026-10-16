a predicate to retrieve or skip items based on the result of the predicate.

# Aggregate Operators

The aggregate operators such as Count, Sum, Min, Max, Average, and Aggregate do not return a sequence; instead they return a single value.

The Count extension method returns the number of items in the collection. In the following example, the Count method is applied to the Years property of a Racer to filter the racers and return only those who won more than three championships. Because the same count is needed more than once in the same query, a variable numberYears is defined by using the let clause (code file EnumerableSample/Program.cs):

```
var query = from r in Formula1.GetChampions()
    let numberYears = r.Years.Count()
    where numberYears >= 3
    orderby numberYears descending, r.LastName
    select new
    {
        Name = r.FirstName +"" + r.LastName,
        TimesChampion = numberYears
    };

foreach (var r in query)
{
    WriteLine($"{r.Name} {r.TimesChampion}");
}
```

The result is shown here:

```
Michael Schumacher 7
Juan Manuel Fangio 5
Alain Prost 4
Sebastian Vettel 4
Jack Brabham 3
Niki Lauda 3
Nelson Piquet 3
Ayrton Senna 3
Jackie Stewart 3
```

The Sum method summarizes all numbers of a sequence and returns the result. In the next example, Sum is used to calculate the sum of all race wins for a country. First the racers are grouped based on country; then, with the new anonymous type created, the Wins property is assigned to the sum of all wins from a single country:

```
var countries = (from c in
    from r in Formula1.GetChampions()
    group r by r.Country into c
    select new
    {
        Country = c.Key,
        Wins = (from r1 in c
                select r1.Wins).Sum()
    }
    orderby c.Wins descending, c.Country
    select c).Take(5);

foreach (var country in countries)
```