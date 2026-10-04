```
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

Of course, that doesn’t exhaust the possibilities for working with dictionaries. Look up generic dictionary in the Help index for all the details.

Dictionary pairs are in no particular order, and you can’t sort a dictionary. It really is just like a bunch of buckets spread around the floor.

# Array and Collection Initializers

In this section, I summarize initialization techniques for both arrays and collections — both old-style and new. You may want to bend the page corner.

# Initializing arrays

As a reminder, given the var syntax covered in the section “Using var for Arrays,” earlier in this chapter, an array declaration can look like either of these examples:

```
int[] numbers = { 1, 2, 3 };          // Shorter form -- can't use var.
var numbers = new [] { 1, 2, 3 };      // Full initializer mandatory with var.
```

# Initializing collections

Meanwhile, the traditional way to initialize a collection, such as a List<T> — or a Queue<T> or Stack<T> — back in the C# 2.0 days (a number of years ago), was this:

```
List<int> numList = new List<int>();      // New empty list.
numbers.Add(1);                           // Add elements one at a time.
numbers.Add(2);
numbers.Add(3);                           // ...tedious!
```

Or, if you had the numbers in an array or another collection already, it went like this:

```
List<int> numList = new List<int>(numbers); // Initializing from an array or...
List<int> numList2 = new List<int>(numList);// from another collection or...
numList.AddRange(numbers);                 // using AddRange
```