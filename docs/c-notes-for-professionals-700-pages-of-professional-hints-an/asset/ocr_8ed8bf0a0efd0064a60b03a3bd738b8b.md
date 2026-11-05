Group by Category and Year:

```
foreach (var grp in films.GroupBy(f => new { Category = f.Category, Year = f.Year })) {
    var groupCategory = grp.Key.Category;
    var groupYear = grp.Key.Year;
    var numberOfFilmsInCategory = grp.Count();
}
```

# Section 66.30: OrderBy

> Orders a collection by a specified value.

When the value is an integer, double or float it starts with the minimum value, which means that you get first the negative values, than zero and afterwards the positive values (see Example 1).

When you order by a char the method compares the ascii values of the chars to sort the collection (see Example 2).

When you sort strings the OrderBy method compares them by taking a look at their CultureInfo but normaly starting with the first letter in the alphabet (a,b,c...).

This kind of order is called ascending, if you want it the other way round you need descending (see OrderByDescending).

# Example 1:

```
int[] numbers = {2, 1, 0, -1, -2};
IEnumerable<int> ascending = numbers.OrderBy(x => x);
// returns {-2, -1, 0, 1, 2}
```

# Example 2:

```
char[] letters = {' ', '!', '?', '[', '{', '*', '1', '9', 'a', 'A', 'b', 'B', 'y', 'Y', 'z', 'Z'};
IEnumerable<char> ascending = letters.OrderBy(x => x);
// returns { ' ', '!', '+', '1', '9', '?', 'A', 'B', 'Y', 'Z', '[', 'a', 'b', 'y', 'z', '{' }
```

# Example:

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