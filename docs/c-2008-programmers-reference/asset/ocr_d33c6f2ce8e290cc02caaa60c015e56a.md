You can now iterate through the elements in a SpamPhraseList object using the foreach statement:

```
```
SpamPhraseList list = new SpamPhraseList();
foreach (string s in list)
    Console.WriteLine(s);
```
```

# Implementing IEnumerable<T> and IEnumerator<T>

Besides using the iterators feature in your class to allow clients to step through its internal elements with foreach, you can make your class support the foreach statement by implementing the IEnumerable and IEnumerator interfaces. The generic equivalents of these two interfaces are IEnumerable<T> and IEnumerator<T>, respectively.

> Use the generic versions because they are type safe.

In .NET, all classes that enumerate objects must implement the IEnumerable (or the generic IEnumerable<T>) interface. The objects enumerated must implement the IEnumerator (or the generic IEnumerable<T>) interface, which has the following members:

+   - Current — Returns the current element in the collection
+   - MoveNext() — Advances to the next element in the collection
+   - Reset() — Resets the enumerator to its initial position

The IEnumerable interface has one member:

+   - GetEnumerator() — Returns the enumerator that iterates through a collection

> All the discussions from this point onward use the generic versions of the IEnumerable and IEnumerator interfaces because they are type-safe.

To understand how the IEnumerable<T> and IEnumerator<T> interfaces work, modify SpamPhraseList class to implement the IEnumerable<T> interface:

```
```csharp
public class SpamPhraseList : IEnumerable<string>
{
    protected string[] Phrases =
        new string[]{
            "pain relief","paxil","pharmacy","phendimetrazine",
            "phentamine","phentermine","pheromones","pherimones",
            "photos of singles","platinum-celebs","poker-chip",
```
```