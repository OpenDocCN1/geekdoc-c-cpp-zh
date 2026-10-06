# 560 CHAPTER 18 Dictionaries And Their Implementations

FIGURE 18-16 A dictionary entry when separate chaining is used

![](bbox=[0.423, 0.142, 0.663, 0.168])

# LISTING 18-5 The class HashedEntry

```
/** A class of entry objects for a hashing implementation of the ADT dictionary.
@file HashedEntry.h */

#ifndef _HASHED_ENTRY
#define _HASHED_ENTRY

#include "Entry.h"

template<class KeyType, class ItemType>
class HashedEntry : public Entry<KeyType, ItemType> {
private:
    HashedEntry<KeyType, ItemType>* nextPtr;
public:
    HashedEntry();
    HashedEntry(ItemType newEntry, KeyType searchQuery);
    HashedEntry(ItemType newEntry, KeyType searchQuery,
    HashedEntry<KeyType, ItemType>* nextPtr);
    void setNext(HashedEntry<KeyType, ItemType>* nextPtr);
    HashedEntry<KeyType, ItemType>* get() const;
};
// end HashedEntry
```

```
#include "HashedEntry.cpp"
#endif
```

Now the data members of our dictionary class, HashedDictionary, are
HashedEntry<KeyType, ItemType>** hashTable; // Array of pointers to entries
int itemCount;\ // Count of dictionary entries
int hashTableSize;
static const DEFAULT_SIZE = 101;

The array hashTable contains pointers to the itemCount entries in the dictionary. The hashTableSize is the size of this array. The constructors will set the value of this field, either to DEFAULT_SIZE or a value given by the client. Note again that this value must be a prime number. Any value given to the constructor will need to be checked to determine whether it is prime and, if not, replaced by a prime number.

The method add to insert a new entry into the dictionary, puts it at the beginning of the chain that the hash function indicates. Assuming the initial values of the pointers in the hash table are each nullPtr, the following pseudocode describes the algorithm for the add operation:

```
add(newItem: ItemType, searchQuery: KeyType): boolean
    p = pointer to a new HashedEntry object containing newItem and searchQuery
```