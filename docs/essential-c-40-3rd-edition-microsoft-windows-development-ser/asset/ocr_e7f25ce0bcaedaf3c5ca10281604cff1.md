Select() may project out a transform from the original type, but the number of items would not change. For example, teams.Select(team => team.Players) will return an IEnumerable<string[]>.

In contrast, SelectMany() iterates across each item identified by the lambda expression (the array selected by Select() earlier) and hoists out each item into a new collection that includes a union of all items within the child collection. Instead of two arrays of players, SelectMany() combines each array selected and produces a single collection of all items.

# More Standard Query Operators

Listing 14.27 shows code that uses some of the simpler APIs enabled by Enumerable; Output 14.13 shows the results.

```
LISTING 14.27: More System.Linq.Enumerable Method Calls

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
    }
}
```