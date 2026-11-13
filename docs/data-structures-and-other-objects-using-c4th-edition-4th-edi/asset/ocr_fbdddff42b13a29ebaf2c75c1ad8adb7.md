# FIGURE 6.7 Header File for the Fifth Bag Template Class

# A Header File

```
// FILE: bag5.h (part of the namespace main_savitch_6B)
// CLASS PROVIDED: bag<Item> (a collection of items; each item may appear multiple times)
// TYPEDEFS for the bag<Item> class:
//   bag<Item>::value_type
//     bag<Item>::value_type is the data type of the items in the bag. It may be any of the
//     C++ built-in types (int, char, etc.), or a class with a default constructor, a copy
//     constructor, an assignment operator, and a test for equality (x == y).
//   bag<Item>::size_type
//     bag<Item>::size_type is the data type of any variable that keeps track of how many
//     items are in a bag.
//   bag<Item>::iterator  and  bag<Item>::const_iterator
//     Forward iterators for a bag and a const bag.
// CONSTRUCTOR for the bag<Item> class:
//   bag( )
//     Postcondition: The bag is empty.
// MODIFICATION MEMBER FUNCTIONS for the bag<Item> class:
//   size_type erase(const Item& target)
//     Postcondition: All copies of target have been removed from the bag. The return value
//     is the number of copies removed (which could be zero).
//   bool erase_one(const Item& target)
//     Postcondition: If target was in the bag, then one copy of target has been removed from
//     the bag; otherwise the bag is unchanged. A true return value indicates that one copy
//     was removed; false indicates that nothing was removed.
//   void insert(const Item& entry)
//     Postcondition: A new copy of entry has been inserted into the bag.
//   void operator +=(const bag& addend)
//     Postcondition: Each item in addend has been added to this bag.
(continued)
```