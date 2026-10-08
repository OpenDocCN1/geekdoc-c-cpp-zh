# Looping Around the Iterator Block 161

```
//PropertyIterator - Demonstrate implementing a class
// property's get accessor as an iterator block.
class PropertyIterator

double[] doubles = { 1.0, 2.0, 3.5, 4.67 };
// DoubleProp - A "get" property with an iterator block
public System.Collections.IEnumerable DoubleProp
{
    get
{
        foreach (double db in doubles)
        {
            yield return db;
        }
    }
}
```

You write the DoubleProp method header in the same way as you write the DescendingEvents(1) method header in the iterator examples. The header returns an IEnumerator interface, but as a property it has no parents after the name and it has a get() accessor — though set(). The get() accessor is implemented as a loop that iterates the collection and uses the standard yield to yield up, in turn, each item in the collection Doubles.

Here's the property is accessed in Main():

```
// Instantiate a PropertyIterator "collection" class.
PropertyIterator prop = new PropertyIterator();
// Iterate: it produces one double at a time.
Console.WriteLine("\name of double values:\n");
foreach (double db in prop.DoubleProp)
{
    Console.WriteLine(db);
}
```

> You can also have a generic iterator. Look up iterators, using in Help. The "Using" topic for C# includes an example of a named iterator that also happens to be generic.

# You can put any your iterator

Hmm, I have to be careful about your phrasing.

In the small-purpose iterator classes in the example, earlier in this chapter, I put the collection inside the iterator class, as in MonthDays. In some cases, that is just right — for instance, when the collection is something like SentenceChunks, which returns bits of text, or something like DescendingEvents, in which the return is calculated on the spot. But you suppose that you want to supply an iterator based on an iterator block for a real collection class, such as LinkedList.