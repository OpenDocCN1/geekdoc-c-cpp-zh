
But again, premature optimizations are typically not a good idea. Measure before you judge whether you have a problem. Just beware of large element counts, in which case an informed decision about the right type of collection is most likely a good idea to avoid too much hassle afterward. And to prepare for when you have to swap out a collection type in favor of another one, use collection interfaces whenever exposing collections to the outside world. This is a general truth in the world of object orientation (OO), but keep your public contract and implementation details separate from one another.

To iterate over a nongeneric collection, you can use the foreach keyword together with a type for the iteration variable that's more specific than System.Object:

```
foreach (int i in lst)
    ...
```

Remember that the foreach statement emits, if needed, a cast expression on the Current property getter call. The following is roughly equivalent to the preceding code:

```
var enumerator = lst.GetEnumerator();
int i;
while (enumerator.MoveNext()) {
    i = (int)enumerator.Current;
    ...
}
```

For heterogeneous nongeneric collections, this can cause an InvalidCastException when the target type specified on the iteration variable conflicts with an item that was retrieved by the Current call. And because the collection is not generic, the var keyword cannot be used to infer the element type (it will instead resolve to System.Object):

```
foreach (var i in lst)
    ...
```

Yet another reason to go for generic collections wherever possible!

## Hash Tables

A hash table provides key/value pairing with support for efficient lookup by key. Being nongeneric, key and value are represented as System.Object. An exploratory example is shown here:

```
var tbl = new Hashtable();
tbl.Add("Bart", 26);
tbl["John"] = 62;
```

```csharp
bool bartIsKnown = tbl.ContainsKey("Bart");
bool someIsAged62 = tbl.ContainsValue(62);
foreach (string name in tbl.Keys)
    Console.WriteLine("Age of {0} is {1}", name, tbl[name]);

tbl.Remove("Bart");
```

Internally, keys are hashed by use of the key type’s GetHashCode implementation. The idea of a hash code is to provide an integer-valued identifier for an object with as good uniqueness properties as possible. Whenever an entry is requested from the table by using a key, the hash code of the supplied key gets computed. Based on that value, a fast lookup in the underlying storage can be made as opposed to a sequential scan of the key/value pairs. Characteristics of a hash code are as follows:

- For two objects that compare equal (by means of `Object.Equals`), the hash code must be the same.
- As long as an object does not mutate its state, the hash code must remain the same. This is important for hash tables to be able to find back an object based on its hash code-based key.
- The more random the distribution of a hash code across all objects of the same type, the better. For hash tables, this allows faster lookup times.

Because hash codes for different objects can be the same (preferably they are not), it’s sometimes necessary to disambiguate between objects with the same hash code. This is done by using the Equals method on the conflicting objects involved. Both Equals and GetHashCode are defined on System.Object and can be overridden by your types:

```csharp
class Person {
    // Name and Age property + a constructor

    public override bool Equals(object obj) {
        var other = obj as Person;
        if (other == null)
            return false;
        return other.Name == Name && other.Age == Age;
    }

    public override int GetHashCode() {
        return (Name ?? "").GetHashCode() ^ Age;
    }
}
```

The Equals method checks to make sure the given object is of the Person type by using the as keyword and a null check. If this is the case, all state is compared on the two instances. For GetHashCode, we leverage the hash code of the Name string and XOR it with the Age value. With those overridden methods in place, you can empirically observe the use of GetHashCode when a Person instance is added to a Hashtable for use as a key. This experiment is shown in Figure 16.1.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_786_0.png)

FIGURE 16.1 GetHashCode being called by the Hashtable's Insert code path.

### WHAT NOT TO USE HASH CODES FOR

Hash codes are used to make object lookup more efficient but don't provide many (or any) guarantees beyond that use. For example, given two equal hash codes, you cannot conclude the two corresponding objects are equal. Don't rely on hash codes to make security decisions, as a replacement for object identity, or to find objects back in a persistent store.

The reason not to use hash codes for persistency purposes (for example, in a database) is that the default hash code implementation, as provided by System.Object, can (and will) change between different releases of the .NET Framework. All that is required from a hash code are the properties outlined earlier on, for the duration of a program's execution. More specifically, it's even valid for an application to produce different hash codes for objects across runs.

Notice how the used Person type is immutable. That's important when dealing with hash tables unless you can make sure by static code analysis that key objects do not change their state while being used in a hash table. The reason should be obvious. During insertion, the hash code of the key object is used to put the object in a certain spot in the storage. When a key is supplied for lookup (for example, through the indexer getter), the hash code is calculated to locate the object in storage. If the recomputed hash code differs, the item will not be found. Figure 16.2 shows such a case where Bart has aged and his shoe size cannot be retrieved.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_787_0.png)

FIGURE 16.2 The indexer returns null if the key is not found.

This concludes our look at the hash table collection. All knowledge you gained in this section will be carried forward to the parallel world of generic collections, in particular the Dictionary<TKey, TValue> type.

## Queue

A queue is a first-in, first-out (FIFO) collection. Basic operations are Enqueue and Dequeue, respectively, to add an element to the end of the queue and to retrieve the first element in the queue. Compare this to a queue in the supermarket: If you're in front, you'll be served first. Figure 16.3 illustrates the principle of a queue's operation.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_787_1.png)

FIGURE 16.3 Dequeue, Peek, and Enqueue operations on a queue data structure.

The following is a real-world example of a queue:

```
var postOffice = new Queue();
postOffice.Enqueue(new Person("Bart", 10));
postOffice.Enqueue(new Person("Homer", 38));
postOffice.Enqueue(new Person("Ned", 60));
var bart = (Person)postOffice.Dequeue();
var homer = (Person)postOffice.Peek(); // D'oh
int twoLeft = postOffice.Count;
```

Because all collection types implement IEnumerable, you can enumerate over a queue, as well, which will produce a head-to-tail enumeration order.

Queues are often used to queue up work items, such as order processing requests. Getting work through Dequeue is a constant time operation, whereas Enqueue is constant time unless the internal storage array has reached its capacity, at which point it becomes linear in the size of the store.

### INITIAL CAPACITY AND GROW FACTOR

Specialized constructor overloads can be used to supply an initial capacity and a grow factor. The latter value, a float, is used to grow the queue's internal storage when its capacity has been reached. The more estimates you have about both the initial capacity and grow factor, the better. Of course, as usual with performance, don't start tweaking things just for the sake of it. Most other collection types have similar knobs to play with when needed.

## Stack

Everyone knows a stack by now, as seen with call stacks and evaluation stacks. Stacks are last-in, first-out (LIFO) collections. Compare it to a stack of books where it's (nearly) impossible to get a book other than the one at the top without popping the books on top of it off the stack first. The basic operations are called Push and Pop, and a Peek method allows looking at the top element without popping it off. Figure 16.4 graphically depicts the operation of a stack.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_788_0.png)

FIGURE 16.4 Operation of a stack data structure.
