
An *algorithm* is a procedure that is used to process the data contained in the containers. The STL includes many different kinds of algorithms to provide support to tasks such as initializing, searching, copying, sorting, and merging. Algorithms are implemented by template functions.

An *iterator* is an object (like a pointer) that points to an element in a container. We can use iterators to move through the contents of containers. Iterators are handled just like pointers. We can increment or decrement them. Iterators connect algorithms with containers and play a key role in the manipulation of data stored in the containers.

## 14.3 Containers

As stated earlier, containers are objects that hold data (of same type). The STL defines ten containers which are grouped into three categories as illustrated in **Fig. 14.2**. **Table 14.1** gives the details of all these containers as well as header file to be included to use each one of them and the type of iterator supported by each container class.

**Table 14.1** *Containers supported by the STL*

| Container | Description | Header file | Iterator |
|---|---|---|---|
| vector | A dynamic array. Allows insertions and deletions at back. Permits direct access to any element | `<vector>` | Random access |
| list | A bidirectional, linear list. Allows insertions and deletions anywhere. | `<list>` | Bidirectional |
| deque | A double-ended queue. Allows insertions and deletions at both the ends. Permits direct access to any element. | `<deque>` | Random access |
| set | An associative container for storing unique sets. Allows rapid lookup. (No duplicates allowed) | `<set>` | Bidirectional |
| multiset | An associative container for storing non-unique sets. (Duplicates allowed) | `<set>` | Bidirectional |
| map | An associative container for storing unique key/value pairs. Each key is associated with only one value (One-to-one mapping). Allows key-based lookup. | `<map>` | Bidirectional |
| multimap | An associative container for storing key/value pairs in which one key may be associated with more than one value (one-to-many mapping). Allows key-based lookup. | `<map>` | Bidirectional |
| stack | A standard stack. Last-in-first-out (LIFO). | `<stack>` | No iterator |
| queue | A standard queue. First-in-first-out (FIFO). | `<queue>` | No iterator |
| priority_queue | A priority queue. The first element out is always the highest priority element. | `<queue>` | No iterator |

**Fig. 14.3** *Elements in a sequence container*

The STL provides three types of sequence containers:

- vector
- list
- deque

Elements in all these containers can be accessed using an iterator. The difference between the three of them is related to only their performance. Table 14.2 compares their performance in terms of speed of random access and insertion or deletion of elements.

**Table 14.2** — *Comparison of sequence containers*

| Container | Random access | Insertion or deletion in the middle | Insertion or deletion at the ends |
|---|---|---|---|
| vector | Fast | Slow | Fast at back |
| list | Slow | Fast | Fast at front |
| deque | Fast | Slow | Fast at both the ends |

### Associative Containers

Associative containers are designed to support direct access to elements using keys. They are not sequential. There are four types of associative containers:

- set
- multiset
- map
- multimap

All these containers store data in a structure called *tree* which facilitates fast searching, deletion, and insertion. However, these are very slow for random access and inefficient for sorting.

Containers **set** and **multiset** can store a number of items and provide operations for manipulating them using the values as the keys. For example, a **set** might store objects of the **student** class which are ordered alphabetically using names as keys. We can search for a desired student using his name as the key. The main difference between a **set** and a **multiset** is that a **multiset** allows duplicate items while a **set** does not.

Containers **map** and **multimap** are used to store pairs of items, one called the *key* and the other called the *value*. We can manipulate the values using the keys associated with them. The values are sometimes called *mapped values*. The main difference between a **map** and a **multimap** is that a **map** allows only one key for a given value to be stored while **multimap** permits multiple keys.

### Derived Containers

The STL provides three derived containers namely, **stack**, **queue**, and **priority_queue**. These are also known as *container adaptors*.

Stacks, queues and priority queues can be created from different sequence containers. The derived containers do not support iterators and therefore we cannot use them for data manipulation. However, they support two member functions **pop()** and **push()** for implementing deleting and inserting operations.

## 14.4 Algorithms

Algorithms are functions that can be used generally across a variety of containers for processing their contents. Although each container provides functions for its basic operations, STL provides more than sixty standard algorithms to support more extended or complex operations. Standard algorithms also permit us to work with two different types of containers at the same time. Remember, STL algorithms are not member functions or friends of containers. They are standalone template functions.

**Table 14.3** *Non-mutating algorithms*

| Operations | Description |
|---|---|
| `search()` | Finds a subsequence within a sequence |
| `search_n()` | Finds a sequence of a specified number of similar elements |

**Table 14.4** *Mutating algorithms*

| Operations | Description |
|---|---|
| `copy()` | Copies a sequence |
| `copy_backward()` | Copies a sequence from the end |
| `fill()` | Fills a sequence with a specified value |
| `fill_n()` | Fills first n elements with a specified value |
| `generate()` | Replaces all elements with the result of an operation |
| `generate_n()` | Replaces first n elements with the result of an operation |
| `iter_swap()` | Swaps elements pointed to by iterators |
| `random_shuffle()` | Places elements in random order |
| `remove()` | Deletes elements of a specified value |
| `remove_copy()` | Copies a sequence after removing a specified value |
| `remove_copy_if()` | Copies a sequence after removing elements matching a predicate |
| `remove_if()` | Deletes elements matching a predicate |
| `replace()` | Replaces elements with a specified value |
| `replace_copy()` | Copies a sequence replacing elements with a given value |
| `replace_copy_if()` | Copies a sequence replacing elements matching a predicate |
| `replace_if()` | Replaces elements matching a predicate |
| `reverse()` | Reverses the order of elements |
| `reverse_copy()` | Copies a sequence into reverse order |
| `rotate()` | Rotates elements |
| `rotate_copy()` | Copies a sequence into a rotated sequence |
| `swap()` | Swaps two elements |
| `swap_ranges()` | Swaps two sequences |
| `transform()` | Applies an operation to all elements |
| `unique()` | Deletes equal adjacent elements |
| `unique_copy()` | Copies after removing equal adjacent elements |

**Table 14.5** *Sorting algorithms*

| Operations | Description |
|---|---|
| `binary_search()` | Conducts a binary search on an ordered sequence |
| `equal_range()` | Finds a subrange of elements with a given value |
| `inplace_merge()` | Merges two consecutive sorted sequences |
| `lower_bound()` | Finds the first occurrence of a specified value |
| `make_heap()` | Makes a heap from a sequence |
| `merge()` | Merges two sorted sequences |
| `nth_element()` | Puts a specified element in its proper place |
| `partial_sort()` | Sorts a part of a sequence |
| `partial_sort_copy()` | Sorts a part of a sequence and then copies |
| `partition()` | Places elements matching a predicate first |
| `pop_heap()` | Deletes the top element |
| `push_heap()` | Adds an element to heap |
| `sort()` | Sorts a sequence |
| `sort_heap()` | Sorts a heap |
