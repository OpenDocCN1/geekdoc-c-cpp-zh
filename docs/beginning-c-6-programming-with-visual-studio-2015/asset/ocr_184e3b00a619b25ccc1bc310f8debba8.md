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

+   - **Add()** — Takes two parameters, a key and a value, to store together. The dictionary collection has a member called Dictionary inherited from DictionaryBase, which is an IDictionary interface. This interface has its own Add() method, which takes two object parameters. Your implementation takes a string value as a key and an Animal object as the data to store alongside this key.
+   - **Remove()** — Takes a key parameter, rather than an object reference. The item with the key value specified is removed.
+   - **Indexer** — Uses a string key value, rather than an index, which is used to access the stored item via the Dictionary inherited member. Again, casting is necessary here.