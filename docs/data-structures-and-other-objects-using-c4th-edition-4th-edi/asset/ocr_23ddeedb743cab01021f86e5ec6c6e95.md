# FIGURE 3.9 Header File for the Sequence Class

# A Header File

```
// FILE: sequence1.h
// CLASS PROVIDED: sequence (part of the namespace main_savitch_3)
// TYPEDEF and MEMBER CONSTANTS for the sequence class:
//   typedef ___ value_type
//     Postcondition: value_type is the data type of the items in the sequence. It may be any of the
//     C++ built-in types (int, char, etc.), or a class with a default constructor, an assignment
//     operator, and a copy constructor
//   typedef ___ size_type
//     Postcondition: size_type is the data type of any variable that keeps track of how many
//     items are in a sequence.
//   static const size_type CAPACITY = ___
//     Postcondition: CAPACITY is the maximum number of items that a sequence can hold.
// CONSTRUCTOR for the sequence class:
//   sequence( )
//     Postcondition: The sequence has been initialized as an empty sequence.
// MODIFICATION MEMBER FUNCTIONS for the sequence class:
//   void start( )
//     Postcondition: The first item in the sequence becomes the current item (but if the
//     sequence is empty, then there is no current item).
//   void advance( )
//     Precondition: is_item returns true.
//     Postcondition: If the current item was already the last item in the sequence, then there
//     is no longer any current item. Otherwise, the new item is the item immediately after
//     the original current item.
//   void insert(const value_type& entry)
//     Precondition: size( ) < CAPACITY.
//     Postcondition: A new copy of entry has been inserted in the sequence before the
//     current item. If there was no current item, then the new entry has been inserted at the
//     front. In either case, the new item is now the current item of the sequence.
//   void attach(const value_type& entry)
//     Precondition: size( ) < CAPACITY.
//     Postcondition: A new copy of entry has been inserted in the sequence after the current
//     item. If there was no current item, then the new entry has been attached to the end of
//     the sequence. In either case, the new item is now the current item of the sequence.
//   void remove_current( )
//     Precondition: is_item returns true.
//     Postcondition: The current item has been removed from the sequence, and the
//     item after this (if there is one) is now the new current item. (continued)
```