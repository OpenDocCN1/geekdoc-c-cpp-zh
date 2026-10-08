# Using Sets 131

smallPrimeNumbers.Add(2);

the compiler doesn't treat the duplication as an error (and doesn't change the hash set, which can't have duplicates). Actually, Add() returns true if the addition occurred and false if it didn't. You don't have to use that fact, but it can be useful if you want to do something when an attempt is made to add a duplicate:

```
bool successful = smallPrimeNumbers.Add(2);
if(successful)
{
    // was added, now something useful.
}
// If successful is false, not added because it was already there
```

The example — the HashSetExample on the Web site — shows off several HashSet<T> methods, more importantly, demonstrates using a HashSet<T> as a tool for working with other collections. You can directly mathematical operations with HashSet<T>, but find its ability to combine collections in various ways kinda

The first segment of this code starts with a List-string> and an array. Each contains color names. Though you could combine the two by simply calling the list's AddRange() method):

```
colors.AddRange(moreColors);
```

the resulting list contains some duplicates (yellow, orange). Using a HashSet<T> and the UnionWith() method, on the other hand, you can combine two collections and eliminate all duplicates in one shot, of the following examples:

Here's the beginning of the HashSetExample on your book's website:

```
Console.WriteLine("Combining two collections with no duplicates:");
List<string> colors = new List<string> {"red", "orange", "yellow"};
string[] moreColors = {"orange", "yellow", "blue", "violet" };
// Want to combine without any duplicates.
// Following is the first stage -
HashSet<string> combined = new HashSet<string>(colors);
// ... now for the second stage.
UnionWith() collects items in lists that aren't duplicated,
// resulting in a collection whose members are all unique.
combined.UnionWith(moreColors);
foreach (string color in combined)
{
    Console.WriteLine(color);
}
```

The result given here contains "red", "orange", "yellow", "blue", and "violet". The first stage uses the list to initialize a new HashSet<T>. The second stage then calls the UnionWith() method to add to the moreColors array — but only the ones that not

![](bbox=[0.125, 0.365, 0.193, 0.433])

![](bbox=[0.125, 0.585, 0.193, 0.653])

Book I
Chapter 6

REMEMBER
Lining Up
Ducks With
Your