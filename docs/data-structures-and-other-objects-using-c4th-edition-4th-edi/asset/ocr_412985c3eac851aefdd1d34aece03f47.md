```
void attach(const value_type& entry);
// Precondition: size( ) < CAPACITY.
// Postcondition: A new copy of entry has been inserted in the sequence
// after the current item. If there was no current item, then the new entry
// has been attached to the end. In either case, the new item is now the
// current item of the sequence.
```

If there is no current item, then the attach function places the new item at the end of the sequence (rather than the front). Either insert or attach can be used to place the first item on a sequence.

# The remove_current member function.

The current item can be removed from a sequence. The member function for a removal has no parameters.

```
void remove_current( );
// Precondition: is_item returns true.
// Postcondition: The current item has been removed from the sequence,
// and the item after this (if there is one) is now the current item.
```

The function's precondition requires that there is a current item; it is this current item that is removed. For example, suppose scores is the four-item sequence shown at the top of the box in the margin, and the highlighted 8.3 is the current item. After activating scores.remove_current( ), the 8.3 has been deleted, and the 4.1 is now the current item.

![](bbox=[0.75, 0.31, 0.88, 0.5])

# The Sequence Class—Documentation

The header file for this first version of our sequence class is shown in Figure 3.9 on page 128. The header file includes the class definition with our specification for three member variables. We discuss these member variables next.

# The Sequence Class—Design

Our suggested design for the sequence class has three private member variables. The first variable, data, is an array that stores the items of the sequence. Just like the bag, data is a partially filled array. A second member variable, called used, keeps track of how much of the data array is currently being used. Therefore, the used part of the array extends from data[0] to data[used-1]. The third member variable, current_index, gives the index of the "current" item in the array (if there is one). If there is no valid current item in the sequence, then current_index will be the same number as used (since this is larger than any valid index). Here is the complete invariant of our class, stated as three rules:

+   1. The number of items in the sequence is stored in the member variable used.
+   2. For an empty sequence, we do not care what is stored in any of data; for a non-empty sequence, the items are stored in their sequence order from data[0] to data[used-1], and we don't care what is stored in the rest of data.
+   3. If there is a current item, then it lies in data[current_index]; if there is no current item, then current_index equals used.