# 132 Using Sets

already in the set ends up containing the colors in both original lists. Green, blue, and violet come from the second list; red, orange, and yellow come from the first. The moreColors array's orange and yellow duplicate the ones already in the set, they're screened out.

But suppose you want to end up with a List<T> containing those colors, not a HashSet<T>. The next segment shows how to create a new List<T> initialized with the combined set:

```
Console.WriteLine("Converting the combined set to a list:");
// Initialize a new List from the combined set above.
List<string> spectrum = new List<string>(combined);
foreach(string color in spectrum)
{
    Console.WriteLine(color);
}
```

Back when these examples were written, the 2008 U.S. presidential campaign was in full swing, with ten early candidates in each party. A good many of those candidates were also members of the U.S. Senate. How can you produce a list of candidates who are also in the Senate? The HashSet<T> IntersectWith() method gives you the overlapping items between the candidate list and the Senate list — items in both, but only those items:

```
Console.WriteLine("Finding the overlap in two lists:");
List<string> presidentialCandidates = new List<string> { "Clinton", "Edwards", "Giuliani", "McCain", "Kennedy" };
List<string> senators = new List<string> { "Alexander", "Boxer", "Clinton", "McCain", "Obama" };
HashSet<string> senatorsRunning = new HashSet<string>(presidentialCandidates);
// IntersectWith collects items that appear in both lists, eliminates others.
senatorsRunning.IntersectWith(senators);
foreach (string senator in senatorsRunning)
{
    Console.WriteLine(senator);
}
```

The result is "Clinton", "McCain", "Obama" because those are the only ones in both of two lists. The opposite trick is to remove any items that appear so you end up with just the items in your target list that aren't duplicated in the other list. This is how the HashSet<T> ExcludeWith():

```
Console.WriteLine("Excluding items from a list:");
Queue<int> queue = new Queue<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 17 };
HashSet<int> unique = new HashSet<int> { 1, 3, 5, 7, 9, 11, 13, 15 };
// ExcludeWith removes items in unique that are (also) in queue: 1, 3, 5, 7.
unique.ExcludeWith(unique);
{
    Console.WriteLine(n.ToString());
}
```

*