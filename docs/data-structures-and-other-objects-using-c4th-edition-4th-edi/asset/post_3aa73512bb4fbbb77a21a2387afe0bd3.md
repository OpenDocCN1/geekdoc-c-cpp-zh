
## 5.6 STL Vectors vs. STL Lists vs. STL Deques

The designers of the Standard Template Library included three similar container classes—the vector, the list, and the deque (pronounced “deck”)—that differ primarily in their storage mechanism. Vectors use a dynamic array; lists use a doubly linked list; and deques use a third mechanism that we’ll see in Chapter 8. The specifications for the three classes are similar enough that we can provide it in a combined form (Figure 5.17).

### FIGURE 5.17 Documentation for the STL Vector, List, and Deque Classes

Partial List of Members for Three Template Classes: vector<Item> (from #include <vector>), list<Item> (from #include <list>), and deque<Item> (from #include <deque>)

```
// TYPEDEFs for these classes:
// value_type
// When a vector or list is declared, the data type of the elements must be specified. For
// example, to declare a list that contains integers: list<int> scores;
// size_type
// The size_type is the data type for specifying the number of elements in a vector or list.
// Most often, it is an unsigned integer type (negative numbers are forbidden).
// DEFAULT CONSTRUCTOR for value_type of T:
// vector<T>( ) and list<T>( ) and deque<T>( )
// Postcondition: The container (which may contain T objects) is empty.
// MODIFICATION MEMBER FUNCTIONS for the vector or list class:
// void clear( )
// Postcondition: All elements have been removed from the container.
// void push_back(const value_type& entry)
// Postcondition: The size of the container has been increased by one, and the new value
// (at the right end) comes from the entry parameter.
// void pop_back( )
// Precondition: size( ) > 0.
// Postcondition: The rightmost entry of the container has been removed.
// void push_front(const value_type& entry) and void pop_front( )
// For lists and deques only, these add or remove an element at the left end of the list.
// void reserve(size_type amount)
// This function, only for the vector, allows the programmer to control efficiency. Calling
// reserve(amount) guarantees that the vector will not need any additional dynamic
// memory until the size exceeds the requested amount.
```

### (FIGURE 5.17 continued)

```
// void resize(size_type amount, const value_type& entry)
// This function changes the number of elements in the container to the specified
// amount. If this new size is smaller than the current size, then removed elements are
// taken from the right end; if the new size is larger, then new elements have the value of
// the entry parameter. If the new entry is omitted from the function call, then new elements
// are initialized by the default constructor of the value_type.
// ACCESSING ELEMENTS DIRECTLY
// Two functions, back and front, can be used to access the rightmost and
// leftmost elements of a container. Both have the precondition that size( ) > 0:
// cout << v.back( ); // Print the rightmost element of v
// v.front( ) = 42; // Change the leftmost element of v to 42.
// ADDITIONAL VECTOR AND DEQUE ACCESS METHODS
// The vector and deque have two methods of accessing individual elements by their index
// (starting with index zero on the left). These are the [ ] operator and the at member
// function. Both have a precondition that the requested index is less than size( ). If the
// precondition is violated, then the at function immediately has an error; but an
// immediate error is not guaranteed for the [ ] operator. Some examples for a vector v:
// cout << v[3]; // Print element at index 3
// cout << v.at(3); // Same as above, but first verify that size( ) > 3.
// v[3] = 42; // Change element at index 3 to 42
// v.at(3) = 42; // Same as above, but first verify that size( ) > 3.
// ITERATOR FUNCTIONS for these classes:
// See page 140 for a discussion of iterators in a collection class. These classes have four
// member functions that provide iterators as their return value. The reverse iterators run
// backward, so that ++i will move a reverse iterator i back to the previous element.
// iterator begin( ) returns an iterator to the first element of the collection
// iterator end( ) returns an iterator to the first element beyond the collection's end
// iterator rbegin( ) returns reverse iterator to the last element of the collection
// iterator rend( ) returns an iterator to the first element before the collection's start
// Once you have an iterator you may perform various actions at that location:
// iterator erase(iterator it)
// Postcondition: The element at the iterator has been removed. The return value is a new
// iterator that's positioned after the erased element.
// iterator erase(iterator it1, iterator it2)
// Postcondition: All elements starting at it1 and going up to (but not including) it2 have
// been removed. The return value is a new iterator that's positioned after the last
// of the erased elements.
// iterator insert(iterator it, const value_type& entry)
// Postcondition: A new entry has been inserted immediately after the iterator. The
// return value is a new iterator that's positioned at the new entry.
// iterator erase(iterator it1, iterator it2)
// Postcondition: All elements starting at it1 and going up to (but not including) it2 have
// been removed. The return value is a new iterator that's positioned after the last
// of the erased elements.
// VALUE SEMANTICS:
// Assignments and the copy constructor may be used with these objects.
```

With your knowledge of dynamic arrays and linked lists, you can figure out why there are certain differences between the vector and the list classes. For example, the list class has versions of push and pop that work at the front of the linked list. It's easy to add or remove an item from the front of a linked list, but not so easy for a vector, so pop_front and push_front are not part of the vector class. On the other hand, accessing an element by its index is easy for a dynamic array, but not for a linked list; therefore the index access functions are provided only for the vector. Some functions, such as insert, are provided for both containers, but one version will be more efficient than the other. (Which do you think is more efficient for insertions?)

As an example of using the list class, consider a program that allows a user to create and manipulate a list of strings. The strings might contain movie titles or a list of to-do tasks—it doesn't matter. We'll leave the writing of the main program to you, but we will go through one function that the main program might call. Notice that the function uses the data type `list<string>`, in which `<string>` indicates the type of item in the list. Here's the function we have in mind to move an item from position i to the front of the list:

```
void move_to_top
(list<string>& data, list<string>::size_type index)
// Precondition: 0 < index <= data.size().
// The item at position index (starting with 1 at the list front) has been
// removed from that spot and reinserted at the front of the list.
{
    assert(0 <= index && index <= data.size());
    list<string>::iterator it;
    list<string>::size_type i;
    string item;

    it = data.begin();
    for (i = 1; i < index; ++i)
        ++it;
    item = *it;
    data.erase(it);
    data.push_front(item);
}
```

The primary programming technique is a loop that moves an iterator forward until it gets to the right spot in the list. At that point, we make a copy of the item, erase the item, and then reinsert the item at the list front.

### Self-Test Exercises for Section 5.6

- 47. Rewrite the move_to_top function for a vector instead of a list (which does not have a push_front member function).

## CHAPTER SUMMARY

- A linked list consists of nodes; each node contains some data and a pointer to the next node in the list. The pointer field of the final node contains the null pointer.
- Typically, a linked list is accessed through a head pointer that points to the head node (i.e., the first node). Sometimes a linked list is accessed elsewhere, such as through the tail pointer that points to the last node.
- You should be familiar with our functions to manipulate a linked list. These functions follow basic patterns that every programmer uses. Such functions are not node member functions (so that they can handle empty lists with no nodes).
- Linked lists can be used to implement a class. Such a class has one or more private member variables that are pointers to nodes in a linked list. The member functions of the class use the linked-list functions to manipulate the linked list, which is accessed through private member variables.
- You have seen two classes implemented with the linked-list toolkit: a bag and a list. You will see more in the chapters that follow.
- A doubly linked list has nodes with two pointers: one to the next node and one to the previous node. Doubly linked lists are a good choice for supporting a cursor that moves forward and backward.
- Classes can often be implemented in many different ways, such as by using a dynamic array or using a linked list. In general, arrays are better at random access; linked lists are better at insertions/removals at a cursor. In the STL, the vector uses a dynamic array and the list uses a linked list. A third choice, the STL deque, uses a mechanism that we’ll see later.

### Solutions to Self-Test Exercises

- 1. See the class definition on page 226.
- 2. The null pointer is a special value that can be used for any pointer that does not point anywhere. The `cstddef` library should be included to use NULL, but because NULL is not part of the std namespace, it can be written without preceding `std::`.
- 3. The null pointer is used for the link field of the final node of a linked list; it is also used for the head and tail pointers of a list that doesn't yet have any nodes.
- 4. Numbers are given a default value of 0, and bools are given a default value of false.
- 5. `head_ptr` is a pointer to a node. On the other hand, `*head_ptr` is a node, and the type of `head_ptr->data()` is `node::value_type`.
- 6. `if (head_ptr->data() == 0)
      cout << "zero";`
- 7. The operation of accessing a data member has higher precedence than the dereferencing asterisk. Therefore, `*head_ptr.data()` will cause a syntax error because the call to `data()` is attempted before dereferencing `head_ptr`. The alternative syntax is `head_ptr->data();`
- 8. `cout << b_ptr->size();`
