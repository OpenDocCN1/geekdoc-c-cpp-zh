# list

The template class (declared in the list header file) represents a doubly linked list. Each element, other than the first and last, is linked to the element before it and the item following it, implying that a list can be traversed in both directions. The crucial difference between list and vector is list provides constant-time insertion of elements at any location in the list. (Recall that the vector template provides linear-time insertion and removal except at the end, where it provides constant-time insertion and removal.) Thus, vector emphasizes access via random access, whereas list emphasizes rapid insertion and removal of elements.

Unlike vector, list is a reversible container. Unlike vector iterator, a list iterator does not support notation and random access to the same element after even items are inserted or removed from a container. For example, suppose you have an iterator pointing to the first element of a vector. Then suppose you insert an element at the beginning of the container. All the other elements have to be moved to make room, so after the insert, the fifth element now contains the value that was in the fourth. Thus, the iterator points to the same location but different data. Inserting a new element into a list doesn't move the existing elements; it just alters the link information. An iterator pointing to a certain item still points to the same item, but it may be linked to different items than before.

The list class has list-oriented member functions in addition to those that come with sequences and reversible containers. Table 16.9 lists many of them. (For a complete list of STL methods and functions, see Appendix G.) The Alloc template parameter you normally don't have to worry about because it has a default value.

# Table 16.9 Some list Member Functions

| Function | Description |
|---|---|n| void merge(list<T, Alloc>& x) | Merges list x with the invoking list. Both lists must be sorted. The resulting list is the invoking list, and x is left empty. This function has linear-time complexity. |
| void remove(const T& val) | Removes all instances of val from the list. This function has linear-time complexity. |
| void sort() | Sorts the list using the < operator; the complexity is N log N for N elements. |
| void splice(iterator pos, list<T, Alloc> x) | Inserts the contents of list x in front of pos, and x is left empty. This function has constant-time complexity. |
| void unique() | Collapses each consecutive group of elements to a single element. This function has linear-time complexity. |