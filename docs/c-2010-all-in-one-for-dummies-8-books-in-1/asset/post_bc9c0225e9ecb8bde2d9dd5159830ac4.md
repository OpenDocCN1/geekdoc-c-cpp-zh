
# Array and Collection Initializers

## Initializing collections

Meanwhile, the traditional way to initialize a collection, such as a List<T> or a Queue<T> or Stack<T> — back in the C# 2.0 days (a number of years ago), was:

```csharp
List<int> numList = new List<int>();
numbers.Add(1);
numbers.Add(2);
numbers.Add(3);
// Empty list.
// Add elements one at a time.
// ... tedious!
```

Or, if you had the numbers in an array or other collection already, it went like this:

```csharp
List<int> numList = new List<int>(numbers); // Initializing from an array...
List<int> numList2 = new List<int>(numList); // from another collection...
numList.AddRange(numbers); // using AddRange
```

When initializing lists, queues, or stacks as shown, you can pass in any array or list-like collection, including lists, queues, stacks, and the new sets, which you could in the next section (but not dictionaries) — their shape is wrong. The MoreCollections example on the Web site illustrates several cases of initializing one collection from another.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_154_0.png)

Since C# 3.0, collection initializers resemble the array initializers and are much easier to use than most of the early forms. The new initializers look like:

```csharp
List<int> numList = new List<int> { 1, 2, 3 }; // List
int[] array = { 1, 2, 3 }; // Array
```

The key difference between the array and collection initializers is that you must still out the type for collections — which means giving List<int> after the new keyword (see the bold in the preceding example).

Of course, you can use the var keyword with collections:

```csharp
var list = new List<string> { "Head", "Heart", "Hands", "Health" };
```

You can also use the dynamic keyword:

```csharp
dynamic list = new List<string> { "Head", "Heart", "Hands", "Health" };
```

Initializing dictionaries with the new syntax looks like:

```csharp
Dictionary<int, string> dict =
new Dictionary<int, string> { { 1, "Sam" }, { 2, "Joe" } };
```

Outwardly, this example looks same as for List<T>, but inside the outer curly braces, you have a second level of curly-brace-enclosed items, one entry in the dictionary. Because this dictionary dict has integer keys and string values, each inner pair of curly braces contains one of each, separated by a comma. The key/value pairs are separated by commas as well.

Initializing sets<int> (see the next section) is much like initializing lists:

```csharp
HashSet<int> biggerPrimes = new HashSet<int> { 19, 23, 29, 31, 37, 41 };
```

The UsingVarWithArraysAndCollections example on this book's Web demonstrates the var keyword used with arrays and collections.

# Using Sets

C# 3.0 added the new collection type HashSet<T>. A set is an unordered collection with no duplicate items.

The concept comes from mathematics. Think of the set of genders (female and male), the set of days in a week, or the set of variations on the triangle (isosceles, equilateral, right, obtuse). Unlike math sets, C# sets can't be infinite, though they can be as large as available memory.

You can do things to a set with other collections, such as add, delete and find items. You can also perform several set-like operations, such as union and intersection. Union joins the members of two sets into one. Intersection finds the overlap between two sets and results in a set containing only the overlapping members. Sets are good for combining and eliminating items.

Like dictionaries, sets are implemented using hash tables. Sets resemble dictionaries with keys but no values, making them listike in shape. See the earlier section "Using Dictionaries" for details.

To create a HashSet<T>, you can do this:

```csharp
HashSet<int> smallPrimeNumbers = new HashSet<int>();
smallPrimeNumbers.Add(2);
smallPrimeNumbers.Add(3);
```

Or, more conveniently, you can use a collection initializer:

```csharp
HashSet<int> smallPrimeNumbers = new HashSet<int> { 2, 3, 5, 7, 11, 13 };
```

Or create the set from an existing collection of any list-like kind, including arrays:

```csharp
List<int> intList = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7 };
HashSet<int> numbers = new HashSet<int>(intList);
```

If you attempt to add to a hash item that the set already contains, as in this example:

```csharp
smallPrimeNumbers.Add(2);
```

the compiler doesn't treat the duplication as an error (and doesn't change the hash set, which can't have duplicates). Actually, Add() returns true if the addition occurred and false if it didn't. You don't have to use that fact, but it can be useful if you want to do something when an attempt is made to add a duplicate:

```csharp
bool successful = smallPrimeNumbers.Add(2);
if(successful)
{
    // was added, now something useful.
}
// If successful is false, not added because it was already there
```

The example — the HashSetExample on the Web site — shows off several HashSet<T> methods, more importantly, demonstrates using a HashSet<T> as a tool for working with other collections. You can directly mathematical operations with HashSet<T>, but find its ability to combine collections in various ways kinda

The first segment of this code starts with a List<string> and an array. Each contains color names. Though you could combine the two by simply calling the list's AddRange() method:

```csharp
colors.AddRange(moreColors);
```

the resulting list contains some duplicates (yellow, orange). Using a HashSet<T> and the UnionWith() method, on the other hand, you can combine two collections and eliminate all duplicates in one shot, of the following examples:

Here's the beginning of the HashSetExample on your book's website:

```csharp
Console.WriteLine("Combining two collections with no duplicates:");
List<string> colors = new List<string> {"red", "orange", "yellow"};
string[] moreColors = {"orange", "blue", "violet"};
// Want to combine without duplicates.
HashSet<string> combined = new HashSet<string>(colors);
// The next segment shows how to create a List<T>
// containing those colors, not a HashSet<T>.
// Initialize a List from the combined set:
List<string> spectrum = new List<string>(combined);
// The first stage uses the UnionWith() method to add to the set
combined.UnionWith(moreColors);
foreach (string color in combined)
{
    Console.WriteLine(color);
}
```

The result is "red", "orange", "yellow", and "blue". The first stage uses the UnionWith() method to add to the set — but only those that ![](img/36596fb11aa4233d5cab0d6ddd1d82e8_154_0.png)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_156_0.png)

# 132 Using Sets

Back when these examples were written, the 2008 U.S. presidential campaign was in full swing, with ten early candidates in each party. A good many of those candidates were members of the U.S. Senate. How can you produce a list of candidates who are also in the Senate? The HashSet<T> IntersectWith() method gives you the overlap between the candidate list and the Senate list — items in both, but only those:

```csharp
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

```csharp
Console.WriteLine("Excluding items from a list:");
Queue<int> queue = new Queue<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 17 };
HashSet<int> unique = new HashSet<int> { 1, 3, 5, 7, 9, 11, 13, 15 };
// ExcludeWith removes items in unique that are (also) in queue: 1, 3, 5, 7.
unique.ExcludeWith(queue);
foreach (int n in unique)
{
    Console.WriteLine(n.ToString());
}
```

*
