# FIGURE 5.11 Header File for Our Third Bag Class

# A Header File

```
// FILE: bag3.h (part of the namespace main_savitch_5)
// CLASS PROVIDED: bag (a collection of items, where each item may appear multiple times)
// TYPEDEFS for the bag class:
//   typedef___ value_type
//     bag::value_type is the data type of the items in the bag. It may be any of the C++
//     built-in types (int, char, etc.), or a class with a default constructor, a copy constructor,
//     an assignment operator, and a test for equality (x == y).
//   typedef___ size_type
//     bag::size_type is the data type of any variable that keeps track of how many items are
//     in a bag.
// CONSTRUCTOR for the bag class:
//   bag( )
//     Postcondition: The bag is empty.
// MODIFICATION MEMBER FUNCTIONS for the bag class:
//   size_type erase(const value_type& target)
//     Postcondition: All copies of target have been removed from the bag. The return value
//     is the number of copies removed (which could be zero).
//   bool erase_one(const value_type& target)
//     Postcondition: If target was in the bag, then one copy of target has been removed from
//     the bag; otherwise the bag is unchanged. A true return value indicates that one copy
//     was removed; false indicates that nothing was removed.
//   void insert(const value_type& entry)
//     Postcondition: A new copy of entry has been inserted into the bag.
//   void operator +=(const bag& addend)
//     Postcondition: Each item in addend has been added to the bag.
// CONSTANT MEMBER FUNCTIONS for the bag class:
//   size_type size( ) const
//     Postcondition: The return value is the total number of items in the bag.
//   size_type count(const value_type& target) const
//     Postcondition: The return value is the number of times target is in the bag.
//   value_type grab( ) const
//     Precondition: size( ) > 0.
//     Postcondition: The return value is a randomly selected item from the bag.
```