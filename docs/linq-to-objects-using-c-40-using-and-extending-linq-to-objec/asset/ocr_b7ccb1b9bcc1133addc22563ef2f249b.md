# HOW TO FILTER THE RESULTS (WHERE CLAUSE)

```
foreach (string s in q)
    Console.WriteLine("A {0} can be deadly.", s);

public static bool IsAnimalDeadly(string s)
{
    string[] deadly = new string[] { "Spider", "Snake",
    "Shark", "Sting-Ray", "Jellyfish" };
    return deadly.Contains(s);
}
```

# Output 3-3

A Spider can be deadly.
A Snake can be deadly.
A Shark can be deadly.
A Sting-Ray can be deadly.
A Jellyfish can be deadly.

# Filtering by Index Position

The standard query operators expose a variation of the where operator that surfaces the index position of each collection element as it progresses. The zero-based index position can be passed into a lambda expression predicate by assigning a variable name as the second argument (after the range variable). To surface the index position, a lambda expression must be used, and this can only be achieved using the extension method syntax. List 3-6 demonstrates the simplest usage, in this case returning the first and only even-indexed elements from the source collection, as shown in Output 3-4.

**List 3-6** The index position can be used as part of the Where clause predicate when using lambda expressions—see Output 3-4

```
string[] animals = new string[] { "Koala", "Kangaroo",
"Spider", "Wombat", "Snake", "Emu", "Shark",
"Sting-Ray", "Jellyfish" };

// get the first then every other animal (index is odd)
var q = animals.Where((a, index) => index % 2 == 0);
```