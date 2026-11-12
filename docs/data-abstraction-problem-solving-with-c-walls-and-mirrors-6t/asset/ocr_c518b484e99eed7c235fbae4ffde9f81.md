```
LISTING 18-2 A header file for a class of dictionary entries
/* A class of entry objects for an array-based implementation of the
ADT dictionary.
@file Entry.h */
#ifndef _ENTRY
#define _ENTRY
template <class KeyType, class ItemType>
class Entry
{
private:
   ItemType item;
   KeyType searchKey;
protected:
   void setKey(const KeyType& searchKey);
public:
   Entry();
   Entry(const ItemType newEntry, KeyType searchKey);
   ItemType getItem() const;
   KeyType getKey() const;
   void setItem(const ItemType& newEntry);
   bool operator==(const Entry<KeyType, ItemType>& rightHandItem) const;
   bool operator>(const Entry<KeyType, ItemType>& rightHandItem) const;
}; // end Entry
#include "Entry.cpp"
#endif
```

> **Note: Observations about the class Entry**
> The class Entry has two data members, a dictionary item and an associated search key. It
> also has a set method and a get method for the item portion, but only a public get method
> for the search key. This design prevents us from accidentally changing an Entry object's
> search key, as doing so would destroy the integrity of the dictionary. However, Entry
> does have a protected method setKey. This method is necessary so that the constructor
> of any derived class of Entry can initialize the search key.
> Notice that the class overloads the operators == and >. While we will not need these
> overloaded operators for the array-based dictionary, we will use them when we store the
> dictionary's entries in a binary search tree.

At this point in your study of ADTs, you have other choices for a dictionary implementation. For
instance, you can implement the ADT dictionary by using the ADT list, sorted list, or binary search
tree. The binary search tree implementation, as illustrated in Figure 18-5, is an example of a nonlinear
implementation and offers several advantages over linear implementations. Among these advantages
is the opportunity to reuse the implementation of the ADT binary search tree discussed in
Chapter 16. Implementations based on the ADTs list and sorted list also share this advantage, and
they are left for you to consider as exercises.

A binary search tree implementation is nonlinear