
## Implementing an Outer Join with GroupJoin()

The earlier inner joins are equi-joins because they are based on an equivalent evaluation of the keys. Records appear in the resultant collection only if there are objects in both collections. On occasion, however, it is desirable to create a record even if the corresponding object doesn’t exist. For example, rather than leave the Marketing department out from the final department list simply because it doesn’t have any employees, it would be preferable if we included it with an empty employee list. To accomplish this we perform a left outer join using a combination of both GroupJoin() and SelectMany() along with DefaultIfEmpty(). This is demonstrated in Listing 14.25 and Output 14.12.

### LISTING 14.25: Implementing an Outer Join Using GroupJoin() with SelectMany()

```csharp
using System;
using System.Linq;

// ...

Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;

var items = departments.GroupJoin(
    employees,
    department => department.DepartmentID,
    employee => employee.DepartmentID,
    (department, departmentEmployees) => new
    {
        department.Id,
        department.Name,
        Employees = departmentEmployees
    }).SelectMany(
    departmentRecord => departmentRecord.Employees.DefaultIfEmpty(),
    (departmentRecord, employee) => new
    {
        departmentRecord.Id,
        departmentRecord.Name,
        Employees =
        departmentRecord.Employees
    }).Distinct();

foreach (var item in items)
{
    Console.WriteLine("{0}", item.Name);
    foreach (Employee employee in item.Employees)
    {
        Console.WriteLine("\t" + employee);
    }
}

// ...
```

### OUTPUT 14.12:

```
Corporate
Mark Michaelis (Chief Computer Nerd)
Finance
Jewel Floch (Bookkeeper Extraordinaire)
Engineering
Michael Stokesbary (Senior Computer Wizard)
Brian Jones (Enterprise Integration Guru)
Paul R. Bramsen (Programmer Extraordinaire)
Thomas Heavey (Software Architect)
Information Technology
Robert Stokesbary (Expert Mainframe Engineer)
Research
John Michaelis (Inventor)
Marketing
```

### Calling SelectMany()

On occasion, you may have collections of collections. Listing 14.26 provides an example of such a scenario. The teams array contains two teams, each with a string array of players.

### LISTING 14.26: Calling SelectMany()

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
// ...
var worldCup2006Finalists = new[]
{
    new
    {
        TeamName = "France",
        Players = new string[]
        {
            "Fabien Barthez", "Gregory Coupet",
            "Mickael Landreau", "Eric Abidal",
            "Jean-Alain Boumsong", "Pascal Chimbonda",
            "William Gallas", "Gael Givet",
            "Willy Sagnol", "Mikael Silvestre",
            "Lilian Thuram", "Vikas Dhorasoo",
            "Alou Diarra", "Claude Makelele",
            "Florent Malouda", "Patrick Vieira",
            "Zinedine Zidane", "Djibril Cisse",
            "Thierry Henry", "Franck Ribery",
            "Louis Saha", "David Trezeguet",
            "Sylvain Wiltord",
        },
    },
    new
    {
        TeamName = "Italy",
        Players = new string[]
        {
            "Gianluigi Buffon", "Angelo Peruzzi",
            "Marco Amelia", "Cristian Zaccardo",
            "Alessandro Nesta", "Gianluca Zambrotta",
            "Fabio Cannavaro", "Marco Materazzi",
            "Fabio Grosso", "Massimo Oddo",
            "Andrea Barzagli", "Andrea Pirlo",
            "Gennaro Gattuso", "Daniele De Rossi",
            "Mauro Camoranesi", "Simone Perrotta",
            "Simone Barone", "Luca Toni",
            "Alessandro Del Piero", "Francesco Totti",
            "Alberto Gilardino", "Filippo Inzaghi",
            "Vincenzo Iaquinta",
        }
    }
};

IEnumerable<string> players =
    worldCup2006Finalists.SelectMany(
        team => team.Players);

Print(players);

// ...
```

The output from this listing has each player's name displayed on its own line in the order in which it appears in the code. The difference between Select() and SelectMany() is the fact that Select() would return two items, one corresponding to each item in the original collection.

Select() may project out a transform from the original type, but the number of items would not change. For example, teams.Select(team => team.Players) will return an IEnumerable<string[]>.

In contrast, SelectMany() iterates across each item identified by the lambda expression (the array selected by Select() earlier) and hoists out each item into a new collection that includes a union of all items within the child collection. Instead of two arrays of players, SelectMany() combines each array selected and produces a single collection of all items.

## More Standard Query Operators

Listing 14.27 shows code that uses some of the simpler APIs enabled by Enumerable; Output 14.13 shows the results.

### LISTING 14.27: More System.Linq.Enumerable Method Calls

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

class Program
{
    static void Main()
    {
        IEnumerable<object> stuff =
            new object[] { new object(), 1, 3, 5, 7, 9,
                "thing", new GuildWars() };
        Print("Stuff: {0}", stuff);

        IEnumerable<int> even = new int[] { 0, 2, 4, 6, 8 };
        Print("Even integers: {0}", even);

        IEnumerable<int> odd = stuff.OfType<int>();
        Print("Odd integers: {0}", odd);

        IEnumerable<int> numbers = even.Union(odd);
        Print("Union of odd and even: {0}", numbers);

        Print("Union with even: {0}", numbers.Union(even));
        Print("Concat with odd: {0}", numbers.Concat(odd));
        Print("Intersect with even: {0}",
            numbers.Intersect(even));
        Print("Distinct: {0}", numbers.Concat(odd).Distinct());
        if (numbers.SequenceEqual(
            numbers.Concat(odd).Distinct()))
        {
            throw new Exception("Unexpectedly unequal");
        }

        Console.WriteLine(
            @"Collection ""SequenceEquals"" + collection.Concat(odd.Distinct()));
        Print("Reverse: {0}", numbers.Reverse());
        Print("Average: {0}", numbers.Average());
        Print("Sum: {0}", numbers.Sum());
        Print("Max: {0}", numbers.Max());
        Print("Min: {0}", numbers.Min());
    }
}

private static void Print<T>(
    string format, IEnumerable<T> items)
{
    StringBuilder text = new StringBuilder();
    foreach (T item in items.Take(items.Count() - 1))
    {
        text.Append(item + ", ");
    }
    text.Append(items.Last());
    Console.WriteLine(format, text);
}

private static void Print<T>(string format, T item)
{
    Console.WriteLine(format, item);
}
```

### OUTPUT 14.13:

```
Stuff: System.Object: 1, 3, 5, 7, 9, "thing", 24c24f41-ee05-41b9-958e-304d1e3e-Mbfe
Even integers: 2, 4, 6, 8
Odd integers: 3, 5, 7, 9
Union of odd and even: 2, 4, 6, 8, 1, 3, 5, 7, 9
Union with even: 2, 4, 6, 8, 1, 3, 5, 7, 9
Concat with odd: 2, 4, 6, 8, 1, 3, 5, 7, 9, 1, 3, 5, 7, 9
Intersection with even: 2, 4, 6, 8
Distinct: 2, 4, 6, 8, 1, 3, 5, 7, 9
Collection "SequenceEquals" collection.Concat(odd.Distinct())
Reverse: 9, 7, 5, 3, 1, 8, 6, 4, 2, 0
Average: 4.5
Sum: 95
Max: 9
Min: 0
```

None of the API calls in Listing 14.20 require a lambda expression. Table 14.1 and Table 14.2 describe each method and provide an example.

### TABLE 14.1: Simpler Standard Query Operators

| Method | Description |
| :--- | :--- |
| OfType<T>() | Forms a query over a collection that returns only the items of a particular type, where the type is identified in the type parameter of the OfType<T>() method call. |
| Union() | Combines two collections to form a superset of all the items in both collections. The final collection does not include duplicate items even if the same item existed in both collections to start. |
| Concat() | Combines two collections together to form a superset of both collections. Duplicate items are not removed from the resultant collection. Concat() will preserve the ordering. That is, concatenating {A, B} with {C, D} will produce {A, B, C, D}. |
| Intersect() | Extracts the collection of items that exist in both original collections. |
| Distinct() | Filters out duplicate items from a collection so that each item within the resultant collection is unique. |
| SequenceEquals() | Compares two collections and returns a Boolean indicating whether the collections are identical, including the order of items within the collection. (This is a very helpful message when testing expected results.) |
| Reverse() | Reverses the items within a collection so that they occur in reverse order when iterating over the collection. |

Included in System.Linq.Enumerable is a collection of aggregate functions that enumerate the collection and calculate a result. Count is one example of an aggregate function already shown within the chapter.
