# CHAPTER 3 Array-Based Implementations

```
template<class ItemType>
class ArrayBag : public IInterface<ItemType>
{
private:
    static const int DEFAULT_CAPACITY = 6; // Small size to test for a full bag
    ItemType items[DEFAULT_CAPACITY]; // Array of bag items
    int itemCount; // Current count of bag items
    int maxItems; // Max capacity of the bag
    // Returns either the index of the element in the array that
    // contains the given target or -1, if the array does not contain
    // the target
    int getIndexOf(const ItemType& target) const;
public:
    ArrayBag();
    bool getCurrentSize() const;
    bool isEmpty() const;
    bool add(const ItemType& anEntry);
    bool remove(const ItemType& anEntry);
    void clear();
    bool contains(const ItemType& anEntry) const;
    int getFrequency(const ItemType& anEntry) const;
    vector<ItemType> toVector() const;
};\ // end ArrayBag
#include "ArrayBag.cpp"
#endif
```

> Programming Tip: When a method does not alter the class's data members, make it a const method as a safeguard against an implementation error.

# 3.2.2 Defining the Core Methods

Section 3.1.1 suggests that we consider the methods add and toVector as core methods and define them first. Since we want to check that each correctly increments the count of the bag's entries, we should also implement getCurrentSize and isEmpty. we add these two to our core group, with appropriate constructors.

As we define the methods for the class ArrayBag, we place them into the file ArrayBag.cpp, which begins as follows:

```
/* Implementation file for the class ArrayBag.
@file ArrayBag.cpp */

#include "ArrayBag.h"
```

The constructor. The following default constructor initializes the current number of items in the bag to zero, as well as the bag's capacity:

```
template<class ItemType>
ArrayBag<ItemType>::ArrayBag()
```