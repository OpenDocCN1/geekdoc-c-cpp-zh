to store the information or data associated with a key (similar to the word’s definitions in Webster’s).

![](bbox=[0.038, 0.181, 0.142, 0.257])

.NET dictionaries are based on the idea of a hash table. Imagine a group of buckets spread around the floor. When you compute a hash, using a hash function, you get a value that specifies only one of the buckets. That same hash always points to the same bucket. If the hash is computed properly, you should see a good, fairly even distribution of items spread among the buckets. Thus a hash is a key to one of the buckets. Provide the key to retrieve the bucket’s contents — its value.

Using dictionaries is no harder in C# than in high school. The following DictionaryExample program (excerpts) shows a few things you can do with dictionaries. To save a little space, we show just parts of the Main() method.

![](bbox=[0.039, 0.309, 0.142, 0.382])

If you find the going a bit rough here, you may want to circle back later.

![](bbox=[0.039, 0.395, 0.142, 0.472])

The first piece of the code just creates a new Dictionary object that has string keys and string values. You aren’t limited to strings, though. Either the key or the value, or both, can be any type. Note that the Add() method requires both a key and a value.

```
```csharp
Dictionary<string, string> dict = new Dictionary<string, string>();
// Add(key, value)
dict.Add("Nick", "cool");
dict.Add("C#", "like writing Sanskrit poetry in Morse code");
dict.Add("VB", "a simple but wordy language");
dict.Add("Java", "good, but not C#");
dict.Add("Fortran", "ANCIENT"); // 6-letters-a? variable name for "ancient "
dict.Add("Cobol", "even more wordy, or is it wordier, and verbose than VB");
```
```

The ContainsKey() method tells you whether the dictionary contains a particular key. There’s a corresponding ContainsValue() method too:

```
```csharp
// See if the dictionary contains a particular key.
Console.WriteLine("Contains key C# " + dict.ContainsKey("C#"));    // True
Console.WriteLine("Contains key Ruby " + dict.ContainsKey("Ruby")); // False
```
```

You can, of course, iterate the dictionary in a loop just as you can in any collection. But keep in mind that the dictionary is like a list of pairs of items — think of each pair as an object that contains both the key and the value. So to iterate the whole dictionary with foreach, you need to retrieve one of the pairs each time through the loop. The pairs are objects of type KeyValuePair<TKey, TValue>. In the WriteLine() call, I use the pair’s Key and Value properties to extract the items. Here’s what it looks like:

```
```csharp
// Iterate the dictionary's contents with foreach.
// Note that you're iterating pairs of keys and values.
Console.WriteLine("Contents of the dictionary:");
foreach (KeyValuePair<string, string> pair in dict)
```
```

# Book 1 — Chapter 6

# Lining Up Your Collections with Collections