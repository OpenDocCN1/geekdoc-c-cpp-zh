
trouble trying to add first an integer and then a Student. The list was instantiated for strings, so the compiler rejects both attempts.

The next code fragment instantiates a completely new list for type int and then adds two int values to the list. Afterward, the foreach loop iterates the int list, printing out the ints:

```
// Instantiate for int.
List<int> intList = new List<int>();
intList.Add(3);          // Fine.
intList.Add(4);
Console.WriteLine("Printing intList:");
foreach (int i in intList)  // foreach just works for all collections.
{
    Console.WriteLine("int i = " + i);
}
```

The following bit of code instantiates a new list to hold Students and adds two students with its Add() method. But then notice the array of Students, which I add to the student list using its AddRange() method. AddRange() lets you add a whole array or (almost) any other collection to the list, all at once:

```
// Instantiate for Student.
List<Student> studentList = new List<Student>();
Student student1 = new Student("Vigil");
Student student2 = new Student("Finch");
studentList.Add(student1);
studentList.Add(student2);
Student[] students = { new Student("Mox"), new Student("Fox") };
studentList.AddRange(students); // Add whole array to List.
Console.WriteLine("Num students in studentList = " + studentList.Count);
```

(Don't worry about the "new Student" stuff. I get to that topic in Book II.)

![](img/80ff26f06fc9ab951e1cd4257b867366_148_0.png)

You can easily convert lists to arrays and vice versa. To put an array into a list, use the list's AddRange() method as just described. To convert a list to an array, call the list's ToArray() method:

```
Student[] students = studentList.ToArray();  // studentList is a List<Student>.
```

List<T> also has a number of other methods for adding items, including methods to insert one or more items anywhere in the list and methods to remove items or clear the list. Note that List<T> also has a Count property. (This single nit can trip you up if you're used to the Length property on arrays and strings. For collections, it's Count.)

The next snippet demonstrates several ways to search a list: IndexOf() returns the array-style index of an item within the list, if found, or -1 if not found. The code also demonstrates accessing an item with array-style indexing and via the Contains() method. Other searching methods include BinarySearch(), not shown:

```
// Search with IndexOf().
Console.WriteLine("Student2 at " + studentList.IndexOf(student2));
string name = studentList[3].Name; // Access list by index.
if (studentList.Contains(student1)) // student1 is a Student object.
{
    Console.WriteLine(student1.Name + " contained in list");
}
```

The final code segment demonstrates several more List<T> operations, including sorting, inserting, and removing items.

```
studentList.Sort(); // Assumes Student implements IComparable interface (Ch 14).
studentList.Insert(3, new Student("Ross"));
studentList.RemoveAt(3); // Deletes the third element.
Console.WriteLine("removed " + name); // Name defined above
```

That's only a sampling of the List<T> methods. You can look up the full list in Help.

![](img/80ff26f06fc9ab951e1cd4257b867366_149_0.png)

To look up generic collections you have to look in the Help index for the term List<T>. If you try searching for just List, you'll be lost in a list of lists of lists. If you want to see information about the whole set of collection classes (well, the generic ones), search the index for generic collections.

## Using Dictionaries

You've no doubt used Webster's or another dictionary. It's organized as a bunch of words in alphabetical order. Associated with each word is a body of information including pronunciations, definitions, and other information. To use a dictionary, you look up a word and retrieve its information.

In C#, the dictionary "shape" differs from the list shape. Dictionaries are represented by the Dictionary<TKey, TValue> class. TKey represents the data type used for the dictionary's keys (similar to the words in a standard dictionary or the terms you look up). TValue represents the data type used to store the information or data associated with a key (similar to the word's definitions in Webster's).

![](img/80ff26f06fc9ab951e1cd4257b867366_149_1.png)

.NET dictionaries are based on the idea of a hash table. Imagine a group of buckets spread around the floor. When you compute a hash, using a hash function, you get a value that specifies only one of the buckets. That same hash always points to the same bucket. If the hash is computed properly, you should see a good, fairly even distribution of items spread among the buckets. Thus the hash is a key to one of the buckets. Provide the key to retrieve the bucket's contents — its value.

![](img/80ff26f06fc9ab951e1cd4257b867366_149_2.png)

Using dictionaries is no harder in C# than in high school. The following DictionaryExample program (excerpts) shows a few things you can do with dictionaries. To save a little space, I show just parts of the Main() method.

![](img/80ff26f06fc9ab951e1cd4257b867366_150_0.png)

If you find the going a bit rough here, you may want to circle back later.

The first piece of the code just creates a new Dictionary object that has string keys and string values. You aren't limited to strings, though. Either the key or the value, or both, can be any type. Note that the Add() method requires both a key and a value.

```
Dictionary<string, string> dict = new Dictionary<string, string>();
// Add(key, value).
dict.Add("C#", "cool");
dict.Add("C++", "like writing Sanskrit poetry in Morse code");
dict.Add("VB", "a simple but wordy language");
dict.Add("Java", "good, but not C#");
dict.Add("Fortran", "ANCNT"); // 6-letters-max variable name for "ancient."
dict.Add("Cobol", "even more wordy, or is it wordier, and verbose than VB");
```

The ContainsKey() method tells you whether the dictionary contains a particular key. There's a corresponding ContainsValue() method, too:

```
// See if the dictionary contains a particular key.
Console.WriteLine("Contains key C# " + dict.ContainsKey("C#")); // True
Console.WriteLine("Contains key Ruby " + dict.ContainsKey("Ruby")); // False
```

You can, of course, iterate the dictionary in a loop just as you can in any collection. But keep in mind that the dictionary is like a list of pairs of items — think of each pair as an object that contains both the key and the value. So to iterate the whole dictionary with foreach, you need to retrieve one of the pairs each time through the loop. The pairs are objects of type KeyValuePair<TKey, TValue>. In the WriteLine() call, I use the pair's Key and Value properties to extract the items. Here's what it looks like:

```
// Iterate the dictionary's contents with foreach.
// Note that you're iterating pairs of keys and values.
Console.WriteLine("\nContents of the dictionary:");
foreach (KeyValuePair<string, string> pair in dict)
{
    // Because the key happens to be a string, we can call string methods on it.
    Console.WriteLine("Key: " + pair.Key.PadRight(8) + "Value: " + pair.Value);
}
```

In the final segment of the example program, you can see how to iterate just the keys or just the values. The dictionary's Keys property returns another collection: a list-shaped collection of type Dictionary<TKey, TValue>.KeyCollection. Because the keys happen to be strings, you can iterate the keys as strings and call string methods on them. The Values property is similar. The final bit of code uses the dictionary's Count property to see how many key/value pairs it contains.

```
// List the keys, which are in no particular order.
Console.WriteLine("\nJust the keys:");
// Dictionary<TKey, TValue>.KeyCollection is a collection of just the keys,
// in this case strings. So here's how to retrieve the keys:
Dictionary<string, string>.KeyCollection keys = dict.Keys;
foreach (string key in keys)
{
    Console.WriteLine("Key: " + key);
}
// List the values, which are in same order as key collection above.
Console.WriteLine("\nJust the values:");
Dictionary<string, string>.ValueCollection values = dict.Values;
foreach (string value in values)
{
    Console.WriteLine("Value: " + value);
}
Console.Write("\nNumber of items in the dictionary: " + dict.Count);
```

Of course, that doesn't exhaust the possibilities for working with dictionaries. Look up generic dictionary in the Help index for all the details.

![](img/80ff26f06fc9ab951e1cd4257b867366_151_0.png)

Dictionary pairs are in no particular order, and you can't sort a dictionary. It really is just like a bunch of buckets spread around the floor.

## Array and Collection Initializers

In this section, I summarize initialization techniques for both arrays and collections — both old-style and new. You may want to bend the page corner.

### Initializing arrays

As a reminder, given the var syntax covered in the section "Using var for Arrays," earlier in this chapter, an array declaration can look like either of these examples:

```
int[] numbers = { 1, 2, 3 };      // Shorter form -- can't use var.
var numbers = new[] { 1, 2, 3 };  // Full initializer mandatory with var.
```

![](img/80ff26f06fc9ab951e1cd4257b867366_151_1.png)

### Initializing collections
