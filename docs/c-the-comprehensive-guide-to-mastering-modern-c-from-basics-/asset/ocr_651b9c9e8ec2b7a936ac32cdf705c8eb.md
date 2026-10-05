# Initialize

You initialize a deque just like a vector: using the default constructor without arguments, an initializer list, with an initial size, a pair of iterators, or another container for copying/moving. Starting from C++23, initialization with from_range is also available.

# Assignment

The assign method, like in vector, has the same options as the constructors. With operator=, reassignment by copy and move is possible. With swap, you can exchange the contents of two deques in O(1). Starting from C++23, assign_range is also available.

# Insert

The deque can efficiently insert elements at both the front and back compared to the vector:

+   * Efficient appending at both ends
From vector, the deque has push_back and emplacement_back for appending to the back. For the front, there are push_front and emplacement_front, which also run optimally in O(1). Starting from C++23, you can also efficiently append ranges with append_range and prepend_range.
* Inserting at any position
There is no difference from vector here. Inserting somewhere with emplacement requires copying or moving many elements and thus takes O(n) time. The insert_range method is available starting from C++23.

# Deleting

Unlike with vector, you can also efficiently remove elements from the front with the deque:

+   * All elements
clear() removes all elements from the deque.
* Last or first element
pop_back() works for deque like it does for vector; remove from the front with pop_front() in O(1).
* Single arbitrary element
iterator erase(const_iterator) deletes a single element like vector in O(n).
* Range
iterator erase(const_iterator from, const_iterator to) deletes all elements