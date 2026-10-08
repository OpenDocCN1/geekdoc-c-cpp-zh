# An indexer program example

The index type isn't limited to int. You may choose to index a collection of houses by their owners' names, by house address, or by any number of indices. In addition, the indexer property can be overloaded with multiple types, so you can index a variety of elements in the same collection.

The following Indexer program generates the virtual array class KeyedArray. This virtual array looks and acts like an array that it uses a string value as the index:

![](bbox=[0.135, 0.313, 0.193, 0.388])

```
// Indexer This program demonstrates the use of the index operator
// to provide an array using a string as an index.
// This version is nongraphic, but see the IndexerGeneric example.
using System;
namespace Indexer
public class KeyedArray
{
    // The following string provides the "key" to the array
    // the key is the string used to identify an element.
    private string[] _keys;

    // The object is the actual data associated with that key.
    private object[] _arrayElements;

// KeyedArray -- Create a fixed-size KeyedArray.
public KeyedArray(int size)
{
    _keys = new string[size];
    _arrayElements = new object[size];
}

// Find -- Find the index of the element corresponding to the
// string targetKey (return a negative if it can't be found).
private int Find(string targetKey)
{
    for(int i = 0; i < _keys.Length; i++)
    {
        if (String.Compare(_keys[i], targetKey) == 0)
        {
            return i;
        }
    }
    return -1;
}

// FindEmpty -- Find room in the array for a new entry.
private int FindEmpty()
{
    for(int i = 0; i < _keys.Length; i++)
    {
        if (_keys[i] == null)
        {
            return i;
        }
    }
}
```