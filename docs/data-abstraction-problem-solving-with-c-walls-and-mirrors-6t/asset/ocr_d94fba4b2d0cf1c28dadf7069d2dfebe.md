The header file. The header file in Listing 18-4 declares the class TreeDictionary. Like ArrayDictionary, TreeDictionary stores Entry objects that encapsulate data items with their corresponding search keys. Much of this class is the same as or is similar to ArrayDictionary, except for the private section. It is worth that we declare the binary search tree, itemTree, along with a method to help with the traversal operation.

# LISTING 18-4 A header file for the class TreeDictionary

```
/** A binary search tree implementation of the ADT dictionary
   that organizes its data items in sorted search-key order.
   Search keys in the dictionary are unique.
   @file TreeDictionary.h */

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
   // Binary search tree of dictionary entries
   BinarySearchTree<Entry<KeyType, ItemType> > itemTree;

   void traversalHelper(Entry<KeyType, ItemType>& theEntry);

public:
   TreeDictionary();
   TreeDictionary(int maxNumberOfEntries);
   TreeDictionary(const TreeDictionary<KeyType, ItemType>& dict);
   virtual ~TreeDictionary();

   // The declarations of the public methods appear here and are the
   // same as given in Listing 18-3 for the class ArrayDictionary.
   ...
}; // end TreeDictionary

#include "TreeDictionary.cpp"
#endif
```

The method implementations. Several of the methods in TreeDictionary simply call the analogous method in BinarySearchTree. For example, the method add creates an Entry object from the item and search key passed to it and then attempts that passes to the add method in BinarySearchTree. The resulting definition follows:

```
template <class KeyType, class ItemType>
bool TreeDictionary<KeyType, ItemType>::add(const ItemType& newItem,
                                           const KeyType& searchKey)
{
   return itemTree.add(Entry<KeyType, ItemType>(newItem, searchKey));
} // end add
```