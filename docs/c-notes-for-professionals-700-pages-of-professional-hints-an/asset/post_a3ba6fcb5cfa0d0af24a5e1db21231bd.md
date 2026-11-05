
```
var result = list.SkipWhile(i => i == 42);
// Result: 6, 6, 6, 42
```

## Section 66.27: Query Ordering - OrderBy() ThenBy() OrderByDescending() ThenByDescending()

```
string[] names = { "mark", "steve", "adam" };
```

### Ascending:

Query Syntax

```
var sortedNames =
    from name in names
    orderby name
    select name;
```

Method Syntax

```
var sortedNames = names.OrderBy(name => name);
```

sortedNames contains the names in following order: "adam","mark","steve"

### Descending:

Query Syntax

```
var sortedNames =
    from name in names
    orderby name descending
    select name;
```

Method Syntax

```
var sortedNames = names.OrderByDescending(name => name);
```

sortedNames contains the names in following order: "steve","mark","adam"

### Order by several fields

```
Person[] people =
{
    new Person { FirstName = "Steve", LastName = "Collins", Age = 30 },
    new Person { FirstName = "Phil", LastName = "Collins", Age = 28 },
    new Person { FirstName = "Adam", LastName = "Ackerman", Age = 29 },
    new Person { FirstName = "Adam", LastName = "Ackerman", Age = 15 }
};
```

Query Syntax

```
var sortedPeople = from person in people
    orderby person.LastName, person.FirstName, person.Age descending
    select person;
```

Method Syntax

```
sortedPeople = people.OrderBy(person => person.LastName)
    .ThenBy(person => person.FirstName)
    .ThenByDescending(person => person.Age);
```

Result

- 1. Adam Ackerman 29
- 2. Adam Ackerman 15
- 3. Phil Collins 28
- 4. Steve Collins 30

## Section 66.28: Sum

The Enumerable. Sum extension method calculates the sum of numeric values.

In case the collection's elements are themselves numbers, you can calculate the sum directly.

```
int[] numbers = new int[] { 1, 4, 6 };
Console.WriteLine( numbers.Sum() ); //outputs 11
```

In case the type of the elements is a complex type, you can use a lambda expression to specify the value that should be calculated:

```
var totalMonthlySalary = employees.Sum( employee => employee.MonthlySalary );
```

Sum extension method can calculate with the following types:

- Int32
- Int64
- Single
- Double
- Decimal

In case your collection contains nullable types, you can use the null-coalescing operator to set a default value for null elements:

```
int?[] numbers = new int?[] { 1, null, 6 };
Console.WriteLine( numbers.Sum( number => number ?? 0 ) ); //outputs 7
```

## Section 66.29: GroupBy one or multiple fields

Let's assume we have some Film model:

```
public class Film {
    public string Title { get; set; }
    public string Category { get; set; }
    public int Year { get; set; }
}
```

Group by Category property:

```
foreach (var grp in films.GroupBy(f => f.Category)) {
    var groupCategory = grp.Key;
    var numberOfFilmsInCategory = grp.Count();
}
```

Group by Category and Year:

```
foreach (var grp in films.GroupBy(f => new { Category = f.Category, Year = f.Year })) {
    var groupCategory = grp.Key.Category;
    var groupYear = grp.Key.Year;
    var numberOfFilmsInCategory = grp.Count();
}
```

## Section 66.30: OrderBy

> Orders a collection by a specified value.

When the value is an integer, double or float it starts with the minimum value, which means that you get first the negative values, then zero and afterwards the positive values (see Example 1).

When you order by a char the method compares the ascii values of the chars to sort the collection (see Example 2).

When you sort strings the OrderBy method compares them by taking a look at their CultureInfo but normally starting with the first letter in the alphabet (a,b,c...).

This kind of order is called ascending, if you want it the other way round you need descending (see OrderByDescending).

### Example 1:

```
int[] numbers = {2, 1, 0, -1, -2};
IEnumerable<int> ascending = numbers.OrderBy(x => x);
// returns {-2, -1, 0, 1, 2}
```

### Example 2:

```
char[] letters = {' ', '!', '?', '[', '{', '*', '1', '9', 'a', 'A', 'b', 'B', 'y', 'Y', 'z', 'Z'};
IEnumerable<char> ascending = letters.OrderBy(x => x);
// returns { ' ', '!', '*', '1', '9', '?', 'A', 'B', 'Y', 'Z', '[', 'a', 'b', 'y', 'z', '{' }
```

### Example:

```
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

var people = new[]
{
    new Person {Name = "Alice", Age = 25},
    new Person {Name = "Bob", Age = 21},
    new Person {Name = "Carol", Age = 43}
};
var youngestPerson = people.OrderBy(x => x.Age).First();
var name = youngestPerson.Name; // Bob
```

## Section 66.31: Any and First(OrDefault) - best practice

I won't explain what Any and FirstOrDefault does because there are already two good examples about them. See Any and First, FirstOrDefault, Last, LastOrDefault, Single, and SingleOrDefault for more information.

A pattern I often see in code which should be avoided is

```
if (myEnumerable.Any(t=>t.Foo == "Bob"))
{
    var myFoo = myEnumerable.First(t=>t.Foo == "Bob");
    //Do stuff
}
```

It could be written more efficiently like this

```
var myFoo = myEnumerable.FirstOrDefault(t=>t.Foo == "Bob");
if (myFoo != null)
{
    //Do stuff
}
```

By using the second example, the collection is searched only once and gives the same result as the first one. The same idea can be applied to Single.

## Section 66.32: GroupBy Sum and Count

Let's take a sample class:

```
public class Transaction
{
    public string Category { get; set; }
    public DateTime Date { get; set; }
    public decimal Amount { get; set; }
}
```

Now, let us consider a list of transactions:

```
var transactions = new List<Transaction>
{
    new Transaction { Category = "Saving Account", Amount = 56, Date = DateTime.Today.AddDays(1) },
    new Transaction { Category = "Saving Account", Amount = 16, Date = DateTime.Today.AddDays(-10) },
    new Transaction { Category = "Credit Card", Amount = 15, Date = DateTime.Today.AddDays(1) },
    new Transaction { Category = "Credit Card", Amount = 56, Date = DateTime.Today },
    new Transaction { Category = "Current Account", Amount = 100, Date = DateTime.Today.AddDays(5) },
};
```

If you want to calculate category wise sum of amount and count, you can use GroupBy as follows:

```
var summaryApproach1 = transactions.GroupBy(t => t.Category)
    .Select(t => new
    {
        Category = t.Key,
        Count = t.Count(),
        Amount = t.Sum(ta => ta.Amount),
    }).ToList();
```

```csharp
Console.WriteLine("-- Summary: Approach 1 --");
summaryApproach1.ForEach(
    row => Console.WriteLine($"Category: {row.Category}, Amount: {row.Amount}, Count: {row.Count}"));
```

Alternatively, you can do this in one step:

```csharp
var summaryApproach2 = transactions.GroupBy(t => t.Category, (key, t) =>
{
    var transactionArray = t as Transaction[] ?? t.ToArray();
    return new
    {
        Category = key,
        Count = transactionArray.Length,
        Amount = transactionArray.Sum(ta => ta.Amount),
    };
}).ToList();

Console.WriteLine("-- Summary: Approach 2 --");
summaryApproach2.ForEach(
    row => Console.WriteLine($"Category: {row.Category}, Amount: {row.Amount}, Count: {row.Count}"));
```

Output for both the above queries would be same:

> Category: Saving Account, Amount: 66, Count: 2
>
> Category: Credit Card, Amount: 71, Count: 2
>
> Category: Current Account, Amount: 100, Count: 1

[Live Demo in .NET Fiddle](https://dotnetfiddle.net/)

## Section 66.33: SequenceEqual

SequenceEqual is used to compare two IEnumerable<T> sequences with each other.

```csharp
int[] a = new int[] { 1, 2, 3 };
int[] b = new int[] { 1, 2, 3 };
int[] c = new int[] { 1, 3, 2 };

bool returnsTrue = a.SequenceEqual(b);
bool returnsFalse = a.SequenceEqual(c);
```

## Section 66.34: ElementAt and ElementAtOrDefault

ElementAt will return the item at index n. If n is not within the range of the enumerable, throws an ArgumentOutOfRangeException.

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
numbers.ElementAt(2); // 3
numbers.ElementAt(10); // throws ArgumentOutOfRangeException
```

ElementAtOrDefault will return the item at index n. If n is not within the range of the enumerable, returns a default(T).
