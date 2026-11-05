```
int[] numbers = { 1, 2, 3, 4, 5 };
numbers.ElementAtOrDefault(2); // 3
numbers.ElementAtOrDefault(10); // 0 = default(int)
```

Both ElementAt and ElementAtOrDefault are optimized for when the source is an IList<T> and normal indexing will be used in those cases.

Note that for ElementAt, if the provided index is greater than the size of the IList<T>, the list should (but is technically not guaranteed to) throw an ArgumentOutOfRangeException.

# Section 66.35: DefaultIfEmpty

DefaultIfEmpty is used to return a Default Element if the Sequence contains no elements. This Element can be the Default of the Type or a user defined instance of that Type. Example:

```
var chars = new List<string>() { "a", "b", "c", "d" };

chars.DefaultIfEmpty("N/A").FirstOrDefault(); // returns "a";

chars.Where(str => str.Length > 1)
    .DefaultIfEmpty("N/A").FirstOrDefault(); // return "N/A"

chars.Where(str => str.Length > 1)
    .DefaultIfEmpty().First(); // returns null;
```

# Usage in Left Joins:

With DefaultIfEmpty the traditional Linq Join can return a default object if no match was found. Thus acting as a SQL's Left Join. Example:

```
var leftSequence = new List<int>() { 99, 100, 5, 20, 102, 105 };
var rightSequence = new List<char>() { 'a', 'b', 'c', 'i', 'd' };

var numbersAsChars = from l in leftSequence
    join r in rightSequence
    on 1 equals (int)r into leftJoin
    from result in leftJoin.DefaultIfEmpty('?')
    select new
    {
        Number = l,
        Character = result
    };

foreach(var item in numbersAsChars)
{
    Console.WriteLine("Num = {0} ** Char = {1}", item.Number, item.Character);
}
```

```
output:

Num = 99    Char = c
Num = 100   Char = d
Num = 5     Char = ?
Num = 20    Char = ?
Num = 102   Char = ?
Num = 105   Char = i
```

In the case where a DefaultIfEmpty is used (without specifying a default value) and that will result will no matching