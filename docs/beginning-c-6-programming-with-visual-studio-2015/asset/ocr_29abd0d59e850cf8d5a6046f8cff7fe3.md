One other difference between collections based on DictionaryBase and collections based on CollectionBase is that foreach works slightly differently. The collection from the last section allowed you to extract Animal objects directly from the collection. Using foreach with the DictionaryBase derived class gives you DictionaryEntry structs, another type defined in the System.Collections namespace. To get to the Animal objects themselves, you must use the Value member of this struct, or you can use the Key member of the struct to get the associated key. To get code equivalent to the earlier

```
```
foreach (Animal myAnimal in animalCollection)
{
    WriteLine($"New {myAnimal.ToString()} object added to custom " +
        $"collection, Name = {myAnimal.Name}");
}
```
```

you need the following:

```
```
foreach (DictionaryEntry myEntry in animalCollection)
{
    WriteLine($"New {myEntry.Value.ToString()} object added to " +
        $"custom collection, Name = {{(Animal)myEntry.Value).Name}}");
}
```
```

It is possible to override this behavior so that you can access Animal objects directly through foreach. There are several ways to do this, the simplest being to implement an iterator.

# Iterators

Earlier in this chapter, you saw that the IEnumerable interface enables you to use foreach loops. It's often beneficial to use your classes in foreach loops, not just collection classes such as those shown in previous sections.

However, overriding this behavior, or providing your own custom implementation of it, is not always simple. To illustrate this, it's necessary to take a detailed look at foreach loops. The following steps show what actually happens in a foreach loop iterating through a collection called collectionObject:

+   1. collectionObject.GetEnumerator() is called, which returns an IEnumerator reference. This method is available through implementation of the IEnumerable interface, although this is optional.
+   2. The MoveNext() method of the returned IEnumerator interface is called.
+   3. If MoveNext() returns true, then the Current property of the IEnumerator interface is used to get a reference to an object, which is used in the foreach loop.
+   4. The preceding two steps repeat until MoveNext() returns false, at which point the loop terminates.

To enable this behavior in your classes, you must override several methods, keep track of indices, maintain the Current property, and so on. This can be a lot of work to achieve very little.