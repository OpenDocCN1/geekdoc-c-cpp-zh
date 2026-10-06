
Console.WriteLine("Number of Rectangles = {0}",
q.Count());

## ToArray Operator

The ToArray operator returns an array (<T>) of a given type from any IEnumerable<T> sequence. The most common reason to use this operator is to force the immediate execution of a query in order to capture the resulting data as a snapshot (forcing the execution of the query that is waiting to be enumerated by deferred execution).

ToArray has a single overload with the following method signature:

```csharp
// Returns an array of type T from a
// System.Collections.Generic.IEnumerable<T>.
public static TSource[] ToArray<TSource>(
    this IEnumerable<TSource> source);
```

To demonstrate the use of the ToArray operator, Listing 5-9 executes a query over an IEnumerable<int> sequence and captures the results in any int[] array.

### Listing 5-9 The ToArray operator enumerates an IEnumerable<T> sequence and returns the results in an array

```csharp
IEnumerable<int> data = Enumerable.Range(1, 5);

int[] q = (from i in data
    where i < 3
    select i).ToArray();

Console.WriteLine("Returns {0}, {1}",
q[0], q[1]);
```

## ToDictionary Operator

The ToDictionary operator converts an IEnumerable<TValue> sequence into a Dictionary<TKey, TValue> collection. The System.Collections.Generic.Dictionary<TKey, TValue> collection type keeps a list of key pairs and ensures that each key value is unique. A System.ArgumentException is thrown if a duplicate key insert is attempted during the conversion process.

A Dictionary collection allows efficient access to elements based on key value, and converting a sequence to a dictionary is a way of improving lookup performance if code frequently needs to find elements by key value.

There are four method overloads of the ToDictionary operator. The simplest overload takes only a delegate for determining the key selection function, and the most complex takes a delegate for key selection, selection, and an IComparer that is used for determining if key values are equal. When the element selector function is not passed, the element type itself is used, and when an IComparer<TSource>.Default is used. The method signatures available:

```csharp
// Creates a Dictionary of elements in a sequence
// Key values returned by the key selector
// function must be unique, otherwise a
// System.ArgumentException will be thrown.
// Uses EqualityComparer<TSource>.Default
// to compare keys for uniqueness.
public static Dictionary<TKey, TSource> ToDictionary<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector);
```

```csharp
// Creates a Dictionary of elements in a sequence
// and projects the elements to a new type.
// Key values returned by the key selector
// function must be unique, otherwise a
// System.ArgumentException will be thrown.
// Uses EqualityComparer<TSource>.Default
// to compare keys for uniqueness.
public static Dictionary<TKey, TElement> ToDictionary<TSource, TElement>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    Func<TSource, TElement> elementSelector);
```

```csharp
// Creates a Dictionary of elements in a sequence
// Key values returned by the key selector
// function must be unique, otherwise a
// System.ArgumentException will be thrown.
// Uses the comparer to test for key uniqueness.
public static Dictionary<TKey, TSource> ToDictionary<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IComparer<TKey> comparer);
```

```csharp
// Creates a Dictionary of elements in a sequence
// and projects the returned elements to a new type.
// Key values returned by the key selector
// function must be unique, otherwise a
// System.ArgumentException will be thrown.
// Uses the comparator to test for key uniqueness.
public static Dictionary<TKey, TElement> ToDictionary<TSource, TElement>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    Func<TSource, TElement> elementSelector,
    IComparer<TKey> comparer);
```

To demonstrate the use of ToDictionary operator, Listing 5-10 creates a Dictionary of sample contacts based on the key of last name concatenated with first name, allowing efficient lookup of a contact by name. The sample demonstrates this by looking up a contact from the resulting dictionary by key value.

### Listing 5-10 The ToDictionary operator creates a dictionary of elements in a sequence

```csharp
List<Contact> contacts = Contact.SampleData();

// materialize results into a Dictionary
Dictionary<string, Contact> conDictionary = 
contacts.ToDictionary<Contact, string>(
    c => c.LastName + c.FirstName);

// all contact records now in Dictionary
// find record by key = very efficient
Contact record = conDictionary["Kamph" + "Mack"];

Console.WriteLine("Kamph DOB = {0}", record.DateOfBirth);
```

## ToList Operator

The ToList operator returns a System.Collections.Generic.List<T> from any IEnumerable<T> sequence. The most common reason to use this operator is to force the immediate execution of a query in order to capture the resulting data as a snapshot (forcing the execution of the query that is waiting to be enumerated by deferred execution).

ToList has a single overload with the following method signature:

```csharp
// Returns a System.Collections.Generic.List<T>
// from a System.Collections.Generic.IEnumerable<T>.
public static List<TSource> ToList<TSource>(
    this IEnumerable<TSource> source);
```

To demonstrate the use of the ToList operator, Listing 5-12 executes a query over an IEnumerable<int> sequence and then uses the ForEach method to write the results in a List<T> and the results to the Console window.

### Listing 5-12 The ToList operator enumerates an IEnumerable<T> sequence and returns the results in a List<T>

```csharp
IEnumerable<int> data = Enumerable.Range(1, 5);

// Query and capture results in List<int>
List<int> q = (from i in data
    where i < 3
    select i).ToList();

// ForEach is a method on List<T>
q.ForEach(j => Console.WriteLine(j));

## ToLookup Operator

The ToLookup operator was first covered in Chapter 4, "Grouping and Joining Data," and it was used to facilitate very efficient one-to-many joins between two sequences. ToLookup creates subsequences based on elements that share a common key value. ToLookup is similar in size and behavior to ToDictionary, the difference being how they handle duplicate elements with the same key value. ToLookup allows multiple elements for a given key value, whereas ToDictionary throws an exception if this ever occurs.
