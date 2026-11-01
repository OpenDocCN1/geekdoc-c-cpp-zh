
6. Modify the code in Animals.cs as follows:

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace Ch11Ex02
{
    public class Animals : CollectionBase
    {
        public void Add(Animal newAnimal)
        {
            List.Add(newAnimal);
        }
        public void Remove(Animal newAnimal)
        {
            List.Remove(newAnimal);
        }
        public Animal this[int animalIndex]
        {
            get { return (Animal)List[animalIndex]; }
            set { List[animalIndex] = value; }
        }
    }
}
```

7. Modify Program.cs as follows:

```csharp
static void Main(string[] args)
{
    Animals animalCollection = new Animals();
    animalCollection.Add(new Cow("Donna"));
    animalCollection.Add(new Chicken("Kevin"));
    foreach (Animal myAnimal in animalCollection)
    {
        myAnimal.Feed();
    }
    ReadKey();
}
```

8. Execute the application. The result is shown in Figure 11-2.

![](img/cf72ea860016d2d680fc085fc06f265a_288_0.png)

FIGURE 11-2

used is a key associated with a stored item, rather than an int index, which can make the collection a lot more user-friendly.

As with indexed collections, there is a base class you can use to simplify implementation of the IDictionary interface: DictionaryBase. This class also implements IEnumerable and ICollection, providing the basic collection-manipulation capabilities that are the same for any collection.

DictionaryBase, like CollectionBase, implements some (but not all) of the members obtained through its supported interfaces. Like CollectionBase, the Clear and Count members are implemented, although RemoveAt() isn't because it's a method on the IList interface and doesn't appear on the IDictionary interface. IDictionary does, however, have a Remove() method, which is one of the methods you should implement in a custom collection class based on DictionaryBase.

The following code shows an alternative version of the Animals class, this time derived from DictionaryBase. Implementations are included for Add(), Remove(), and a key-accessed indexer:

```
public class Animals : DictionaryBase
{
    public void Add(string newID, Animal newAnimal)
    {
        Dictionary.Add(newID, newAnimal);
    }
    public void Remove(string animalID)
    {
        Dictionary.Remove(animalID);
    }
    public Animals() {}
    public Animal this[string animalID]
    {
        get { return (Animal)Dictionary[animalID]; }
        set { Dictionary[animalID] = value; }
    }
}
```

The differences in these members are as follows:

- **Add()** — Takes two parameters, a key and a value, to store together. The dictionary collection has a member called Dictionary inherited from DictionaryBase, which is an IDictionary interface. This interface has its own Add() method, which takes two object parameters. Your implementation takes a string value as a key and an Animal object as the data to store alongside this key.
- **Remove()** — Takes a key parameter, rather than an object reference. The item with the key value specified is removed.
- **Indexer** — Uses a string key value, rather than an index, which is used to access the stored item via the Dictionary inherited member. Again, casting is necessary here.

One other difference between collections based on DictionaryBase and collections based on CollectionBase is that foreach works slightly differently. The collection from the last section allowed you to extract Animal objects directly from the collection. Using foreach with the DictionaryBase derived class gives you DictionaryEntry structs, another type defined in the System.Collections namespace. To get to the Animal objects themselves, you must use the Value member of this struct, or you can use the Key member of the struct to get the associated key. To get code equivalent to the earlier

```
foreach (Animal myAnimal in animalCollection)
{
    WriteLine($"New {myAnimal.ToString()} object added to custom " +
        $"collection, Name = {myAnimal.Name}");
}
```

you need the following:

```
foreach (DictionaryEntry myEntry in animalCollection)
{
    WriteLine($"New {myEntry.Value.ToString()} object added to " +
        $"custom collection, Name = {{(Animal)myEntry.Value).Name}}");
}
```

It is possible to override this behavior so that you can access Animal objects directly through foreach. There are several ways to do this, the simplest being to implement an iterator.

## Iterators

Earlier in this chapter, you saw that the IEnumerable interface enables you to use foreach loops. It's often beneficial to use your classes in foreach loops, not just collection classes such as those shown in previous sections.

However, overriding this behavior, or providing your own custom implementation of it, is not always simple. To illustrate this, it's necessary to take a detailed look at foreach loops. The following steps show what actually happens in a foreach loop iterating through a collection called collectionObject:

+   1. collectionObject.GetEnumerator() is called, which returns an IEnumerator reference. This method is available through implementation of the IEnumerable interface, although this is optional.
+   2. The MoveNext() method of the returned IEnumerator interface is called.
+   3. If MoveNext() returns true, then the Current property of the IEnumerator interface is used to get a reference to an object, which is used in the foreach loop.
+   4. The preceding two steps repeat until MoveNext() returns false, at which point the loop terminates.

To enable this behavior in your classes, you must override several methods, keep track of indices, maintain the Current property, and so on. This can be a lot of work to achieve very little.

A simpler alternative is to use an iterator. Effectively, using iterators generates a lot of the code for you behind the scenes and hooks it all up correctly. Moreover, the syntax for using iterators is much easier to get a grip on.

A good definition of an iterator is a block of code that supplies all the values to be used in a foreach block in sequence. Typically, this block of code is a method, although you can also use property accessors and other blocks of code as iterators. To keep things simple, you'll just look at methods here.

Whatever the block of code is, its return type is restricted. Perhaps contrary to expectations, this return type isn't the same as the type of object being enumerated. For example, in a class that represents a collection of Animal objects, the return type of the iterator block can't be Animal. Two possible return types are the interface types mentioned earlier, IEnumerable or IEnumerator. You use these types as follows:

- To iterate over a class, use a method called `GetEnumerator()` with a return type of `IEnumerator`.
- To iterate over a class member, such as a method, use `IEnumerable`.

Within an iterator block, you select the values to be used in the foreach loop by using the yield keyword. The syntax for doing this is as follows:

```
yield return <value>;
```

That information is all you need to build a very simple example, as follows (you can find this code in SimpleIterators\Program.cs):

```
public static IEnumerable SimpleList()
{
    yield return "string 1";
    yield return "string 2";
    yield return "string 3";
}
static void Main(string[] args)
{
    foreach (string item in SimpleList())
        WriteLine(item);
    ReadKey();
}
```

Here, the static method SimpleList() is the iterator block. Because it is a method, you use a return type of IEnumerable. SimpleList() uses the yield keyword to supply three values to the foreach block that uses it, each of which is written to the screen. The result is shown in Figure 11-3.

![](img/cf72ea860016d2d680fc085fc06f265a_294_0.png)

# FIGURE 11-3
