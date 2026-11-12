
## FIGURE 18-16 A dictionary entry when separate chaining is used

![](img/288a0c22d14d2450c1e772f228f867b0_586_0.png)

## LISTING 18-5 The class HashedEntry

```cpp
/* A class of entry objects for a hashing implementation of the
   ADT dictionary.
*/
#if !defined HASHED_ENTRY_H
#define HASHED_ENTRY_H

#include "Entry.h"

template<class KeyType, class ItemType>
class HashedEntry : public Entry<KeyType, ItemType>
{
private:
   HashedEntry<KeyType, ItemType>* nextPtr;

public:
   HashedEntry();
   HashedEntry(ItemType newEntry, KeyType searchKey);
   HashedEntry(ItemType newEntry, KeyType searchKey,
               HashedEntry<KeyType, ItemType>* nextEntryPtr);
   void setNext(HashedEntry<KeyType, ItemType>* nextEntryPtr);
   HashedEntry<KeyType, ItemType>* getNext() const;
}; // end HashedEntry

#endif // end HashedEntry.h
```

Now the data members of our dictionary class, HashedDictionary, are

```cpp
HashedEntry<KeyType, ItemType>** hashTable; // Array of pointers to entries
int itemCount; // Count of dictionary entries
int hashTableSize; // Table size must be prime
static const int DEFAULT_SIZE = 101;
```

The array hashTable contains pointers to the itemCount entries in the dictionary. The field hashTableSize is the size of this array. The constructors will set the value of this field, either to DEFAULT_SIZE or to a value given by the client. We note again that this value must be a prime number. Any value given to the constructor will need to be checked to determine whether it is prime and, if not, replaced by a prime number.

The method add. To insert a new entry into the dictionary, you place it at the beginning of the chain that the hash function indicates. Assuming that the initial values of the pointers in the hash table are each nullptr, the following pseudocode describes the algorithm for the add operation:

```
add(newItem: ItemType, searchKey: KeyType): boolean
p = pointer to a new HashedEntry object containing newItem and searchKey
i = h(searchKey)
if (hashTable[i] == nullptr)
    hashTable[i] = p
else
{
    // Add new entry to beginning of chain
    p->setNext(hashTable[i])
    hashTable[i] = p
}
return true
```

Recall we assume that the search key given to add is not already in the dictionary.
The definition of add in the implementation file for HashedDictionary is

```cpp
template <class KeyType, class ItemType>
bool HashedDictionary<KeyType, ItemType>::add(const ItemType& newItem,
                                                        const KeyType& searchKey)
{
    // Create entry to add to dictionary
    HashedEntry<KeyType, ItemType>* entryToAddPtr =
        new HashedEntry<KeyType, ItemType>(newItem, searchKey);

    // Compute the hash index into the array
    int itemHashIndex = getHashIndex(searchKey);

    // Add the entry to the chain at itemHashIndex
    if (hashTable[itemHashIndex] == nullptr)
    {
        hashTable[itemHashIndex] = entryToAddPtr;
    }
    else
    {
        entryToAddPtr->setNext(hashTable[itemHashIndex]);
        hashTable[itemHashIndex] = entryToAddPtr;
    } // end if

    return true;
} // end add
```

The method remove. To remove an entry, given its search key, from the dictionary, you proceed as the following pseudocode indicates:

```
remove(searchKey: KeyType): boolean
i = h(searchKey)
if (hashTable[i] != nullptr)
    Search the chain pointed to by hashTable[i] for searchKey
    if (searchKey is in the first node)
    {
        p = hashTable[i]
        hashTable[i] = hashTable[i]->getNext()
        delete p
        return true
    }
    else
    {
        curPtr = pointer to the entry containing searchKey
        prevPtr = pointer to the previous entry in the chain
        prevPtr->setNext(curPtr->getNext())
        delete curPtr
        return true
    }
else
return false
```

HashedDictionary's definition of remove follows:

```cpp
template <class KeyType, class ItemType>
bool HashedDictionary<KeyType, ItemType>::remove(const KeyType& searchKey)
{
   bool itemFound = false;

   // Compute the hashed index into the array
   int itemHashIndex = getHashIndex(searchKey);
   if (hashTable[itemHashIndex] != nullptr)
   {
      // Special case - first node has target
      if (searchKey == hashTable[itemHashIndex]->getKey())
      {
         HashedEntry<KeyType, ItemType>* entryToRemovePtr =
         hashTable[itemHashIndex];
         hashTable[itemHashIndex] = hashTable[itemHashIndex]->getNext();
         delete entryToRemovePtr;
         entryToRemovePtr = nullptr; // For safety
         itemFound = true;
      } // end if
      else // Search the rest of the chain
      {
         HashedEntry<KeyType, ItemType>* prevPtr = hashTable[itemHashIndex];
         HashedEntry<KeyType, ItemType>* curPtr = prevPtr->getNext();
         while ((curPtr != nullptr) && !itemFound)
         {
            // Found item in chain so remove that node
            if (searchKey == curPtr->getKey())
            {
               prevPtr->setNext(curPtr->getNext());
               delete curPtr;
               curPtr = nullptr; // For safety
               itemFound = true;
            } // end if
            else // Look at next entry in chain
            {
               prevPtr = curPtr;
               curPtr = curPtr->getNext();
            } // end if
         } // end while
      } // end if
   } // end if
   return itemFound;
} // end remove
```

The rest of the implementation of the class HashedDictionary is left as an exercise.

## SUMMARY

- 1. The ADT dictionary supports value-oriented operations, such as “Retrieve all the information about John Smith.”
- 2. The linear implementations (array-based and link-based) of a dictionary are adequate only in limited situations, such as when the dictionary is small or for certain operations. In those situations, the simplicity of a linear implementation may be an advantage. A linear implementation of a dictionary, however, is not suitable as a general-purpose, reusable class.
- 3. A nonlinear link-based (binary search tree) implementation of the ADT dictionary provides the best aspects of the two linear implementations. The link-based implementation allows the dictionary to grow dynamically and allows insertions and removals of data to occur through pointer changes instead of data movement. In addition, the binary search tree allows you to use a binary-search-like algorithm when searching for an item with a specified value. These characteristics make a nonlinear dictionary implementation far superior to the linear implementations in many applications.
- 4. Hashing as a dictionary implementation calculates where a data item should be rather than searching for it. Hashing allows for very efficient retrievals, insertions, and removals.
- 5. The hash function should be extremely easy to compute—it should require only a few operations—and it should scatter the search keys evenly throughout the hash table.
- 6. A collision occurs when two different search keys hash into the same array location. Two ways to resolve collisions are through probing and chaining.
- 7. Separate chaining is the most time-efficient collision-resolution scheme.
- 8. Hashing does not efficiently support operations that require the table items to be ordered—for example, traversing the table in sorted order.
- 9. When dictionary operations such as traversal are not important to a particular application, if you know the maximum number of dictionary items, and if you have ample storage, hashing is an implementation for a dictionary that is simpler and faster than balanced search tree implementations. Tree implementations, however, are dynamic and do not require you to estimate the maximum number of table items.

## EXERCISES

- 1. Implement the class Entry, as given in Listing 18-2, and then complete the sorted array-based implementation of the ADT dictionary.
- 2. Consider an operation replace(replacementItem, searchKey) that locates, if possible, the item in a dictionary with the given search key. If the dictionary contains such an item, the method replaces it with replacementItem.
  - a. Write implementations of replace for the classes ArrayDictionary, TreeDictionary, and HashedDictionary, as described in this chapter.
  - b. For TreeDictionary, under what circumstances can replace replace an item without altering the structure of the binary search tree? (See Exercise 6 in Chapter 16.)
- 3. Imagine an application program that behaves like an English dictionary. The user types a word and the program provides the word’s definition. Thus, the dictionary needs only a retrieval operation. Which implementation of the ADT dictionary would be most efficient as an English dictionary?
- 4. When you use a word processor’s spell checker, it compares the words in your document with words in a dictionary. You can add new words to the dictionary as necessary. Thus, this dictionary needs frequent retrievals and occasional insertions. Which implementation of the ADT dictionary would be most efficient as a spell checker’s dictionary?
