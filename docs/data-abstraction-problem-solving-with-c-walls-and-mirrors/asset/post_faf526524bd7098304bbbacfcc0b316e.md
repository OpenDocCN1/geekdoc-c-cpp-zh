
# 534 CHAPTER 18 Dictionaries and Their Implementations

FIGURE 18-5 The data members for a binary search tree implementation of the ADT dictionary for the data in Figure 18-1

![](img/d0cb86b2f18b2db569968ad7c743510e_560_0.png)

We also will consider an important unsorted implementation that uses a technique known as hashing. Although based on an array, this implementation is unlike any one you have seen in this book.

## 18.2.1 A Sorted Array-Based Implementation of the ADT Dictionary

Whether a dictionary organizes its entries in sorted order by search key or leaves them unsorted, an array-based implementation has data members that are similar to those in array-based implementations of other ADTs that you have seen, an array of data items, a count of items, and a maximum number of items. We have already seen that the data items will be entry objects that contain both a search key and some other data.

For a sorted dictionary, the operation traverse should visit the dictionary's data items in order that their search keys are in sorted order. Note that we have specified this behavior in the header file for all dictionaries in Listing 18-3. Notice that this dictionary requires its search keys to be unique. This requirement will simplify our implementation, but Exercises 7 and 8 at the end of this chapter ask you to remove this restriction.

The declaration of class Array contains nothing unusual, but does declare private methods--destroy and findEntry. The former method can be called by both the destructor and the public method clear. The latter method enters the array of items that has a given search key. This method is useful for the public methods remove, getItem, and contains. Note that both private methods perform operations needed more than one public method, enabling us to avoid repetitive code in the definitions of the public methods.

Possible Implementations 535

### LISTING 18-3 A header file for the class ArrayDictionary

```cpp
/** An array-based implementation of the ADT dictionary
that organizes its data items in sorted search-key order.
Search keys in the dictionary are unique.
@file ArrayDictionary.h */

#ifndef ARRAY_DICTIONARY
#define ARRAY_DICTIONARY

#include "DictionaryInterface.h"
#include "Entry.h"
#include "NotFoundException.h"

template <class KeyType, class ItemType>
class ArrayDictionary : public DictionaryInterface<KeyType, ItemType>
{
private:
    static const int DEFAULT_CAPACITY = 21; // Small capacity to test for
    // a full dictionary
    Entry<KeyType, ItemType>* items; // Array of dictionary entries
    int itemCount;
    int maxItems; // Maximum capacity of the dictionary

    void destroyDictionary();
    int findEntryIndex(int firstIndex, int lastIndex,
                       const KeyType& searchKey) const;

public:
    ArrayDictionary();
    ArrayDictionary(int maxNumberOfEntries);
    ArrayDictionary(const ArrayDictionary<const KeyType, ItemType>& dict);
    virtual ~ArrayDictionary();
    bool isEmpty() const;
    int getNumberOfItems() const;
    bool add(const KeyType& searchKey, const KeyType& ItemType& newItem);
    bool remove(const KeyType& searchKey);
    void clear();
    ItemType getItem(const KeyType& searchKey) const
        throw (NotFoundException);
    bool contains(const KeyType& searchKey) const;
    /** Traverses the items in this dictionary in sorted search-key order
       and calls a given function for each item. */
    void traverse(void visit(ItemType&)) const;
};
// end ArrayDictionary
#include "ArrayDictionary.cpp"
#endif
```

The requirement that we traverse the dictionary in sorted search-key order provides one
to sort the array items according to the search key. While we could sort items each time
traverse, maintaining this array in sorted order has advantages avoiding a
sorting. One important advantage of a sorted array is that the private method findEntryIndex
perform a recursive binary search when looking for a particular search key. Notice that the

536 CHAPTER 18 Dictionaries And Their Implementations

declaration of this method in Listing 18-3 provides two indices as parameters to indicate the order of the search.
The public method adds the responsibility for keeping the array items sorted. Let's examine its definition:

```cpp
template <class KeyType, class ItemType>
bool ArrayDictionary<KeyType, ItemType>::add(const KeyType& newItem,
const KeyType& searchKey)
{
    bool ableInsert = (itemCount < maxItems);
    if (ableInsert) {
        // Make room for new entry by shifting all toward the end of the array
        int index = itemCount; // Short-circuit evaluation is important
        while (index > 0 && items[index-1].getKey() > searchKey) {
            items[index] = items[index-1];
            index--;
        }
        // Insert new entry
        items[index] = Entry<KeyType, ItemType>(newItem, searchKey);
        itemCount++; // Increase count of entries
    }
    return ableInsert;
} // end add
```

Programming Problem 1: What is the definition of add for ArrayDictionary?

Question 2: Explain the while loop in the previous definition of add.

Question 3: Why is short-circuit evaluation important in the while loop of add?

Question 4: What does the method need to do after it gets the index of this entry?

Question 5: Mention the remove method locates the entry.

Question 6: What is the definition of traverse for ArrayDictionary?

## 18.2.2 A Binary Search Tree Implementation of the ADT Dictionary

Although linear implementations of the ADT are fine for specific applications, they are not suitable as general-purpose classes. The nonlinear-based implementation uses a binary search tree to represent the items. That is, the dictionary class will use composition and thus have a binary search tree as one of its data members. This dictionary implementation has a binary search tree as a

The header file in Listing 18-4 declares the class TreeDictionary. Like ArrayDictionary, TreeDictionary

### LISTING 18-4 A header file for the class TreeDictionary

```cpp
/** A binary search tree implementation of the ADT dictionary
* organizes its data items in sorted search-key order.
* Search keys in the dictionary are unique.
* @file TreeDictionary.h */

#ifndef _TREE_DICTIONARY
#define _TREE_DICTIONARY

#include "DictionaryInterface.h"
#include "BinarySearchTree.h"
#include "Entry.h"
#include "NotFoundException.h"

template <class KeyType, class ItemType>
class TreeDictionary : public DictionaryInterface<KeyType, ItemType>
{
private:
    // Binary search tree of Entry<KeyType, ItemType> itemTree;
    void traversalHelper(Entry<KeyType, ItemType>& theEntry);
public:
    TreeDictionary();
    TreeDictionary(int numberOfOfEntries);
    TreeDictionary(const TreeDictionary<KeyType, ItemType>& dict);
    virtual ~TreeDictionary();

    // The declarations of the public methods appear here and are the
    // same as in Listing 18-3 for the class ArrayDictionary.
    ...
}; // end TreeDictionary
#include "TreeDictionary.cpp"
#endif
```

The method implementations. Several of the methods in TreeDictionary simply call the analog method in BinarySearchTree. For example, the method adds an entry object from the item and search key passed to it and then passes that object to the add method in BinarySearchTree. The resulting definition follows:

```cpp
template <class KeyType, class ItemType>
bool TreeDictionary<KeyType, ItemType>::add(const KeyType& newItem,
const KeyType& searchKey)
{
    return itemTree.add(Entry<KeyType, ItemType>(newItem, searchKey));
} // end add
```
