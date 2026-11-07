
### Section 22.6.2 **set** Associative Container

- The set associative container is used for fast storage and retrieval of unique keys.
- If an attempt is made to insert a duplicate key into a set, the duplicate is ignored.
- A set supports bidirectional iterators.
- Header `<set>` must be included to use class set.

### Section 22.6.3 **multimap** Associative Container

- Containers multimap and map provide operations for manipulating values associated with keys.
- The primary difference between a multimap and a map is that a multimap allows duplicate keys with associated values to be stored and a map allows only unique keys with associated values.
- The multimap associative container is used for fast storage and retrieval of key/value pairs.
- Duplicate keys are allowed in a multimap, so multiple values can be associated with a single key. This is called a one-to-many relationship.
- Header `<map>` (p. 881) must be included to use class templates map and multimap.

### Section 22.6.4 **map** Associative Container

- Duplicate keys are not allowed in a map, so only a single value can be associated with each key. This is called a one-to-one mapping (p. 883).
- A map is commonly called an associative array (p. 883).

## Section 22.7 **Container Adapters**

- The STL provides three container adapters—stack, queue and priority_queue.
- Adapters are not first-class containers, because they do not provide the actual data structure implementation in which elements can be stored and they do not support iterators.
- All three adapter class templates provide member functions push and pop (p. 885) that properly insert an element into and remove an element from each adapter data structure, respectively.

### Section 22.7.1 **stack** Adapter

- Class template stack (p. 885) is a last-in, first-out data structure. Header `<stack>` must be included to use class template stack.
- The stack member function top (p. 885) returns a reference to the top element of the stack (implemented by calling function back of the underlying container).
- The stack member function empty determines whether the stack is empty (implemented by calling function empty of the underlying container).
- The stack member function size returns the number of elements in the stack (implemented by calling function size of the underlying container).

### Section 22.7.2 **queue** Adapter

- Class template queue (p. 887) implements a FIFO data structure. Header `<queue>` (p. 888) must be included to use a queue or a priority_queue.
- The queue member function front returns a reference to the first element in the queue.
- The queue member function back (p. 887) returns a reference to the last element in the queue.
- The queue member function empty determines whether the queue is empty.
- The queue member function size returns the number of elements in the queue.

### Section 22.7.3 priority_queue Adapter

- Class template priority_queue provides functionality that enables insertions in sorted order into the underlying data structure and deletions from the front of the underlying data structure.
- The common priority_queue (p. 888) operations are push, pop, top, empty and size.

### Section 22.8.1 fill, fill_n, generate and generate_n

- Algorithms fill and fill_n (p. 890) set every element in a range of container elements to a specific value.
- Algorithms generate and generate_n (p. 891) use a generator function or function object to create values for every element in a range of container elements.

### Section 22.8.2 equal, mismatch and lexicographical_compare

- Algorithm equal (p. 894) compares two sequences of values for equality.
- Algorithm mismatch (p. 894) compares two sequences of values and returns a pair of iterators indicating the location in each sequence of the mismatched elements.
- Algorithm lexicographical_compare (p. 894) compares the contents of two sequences.

### Section 22.8.3 remove, remove_if, remove_copy and remove_copy_if

- Algorithm remove (p. 896) eliminates all elements with a specific value in a certain range.
- Algorithm remove_copy (p. 897) copies all elements that do not have a specific value in a certain range.
- Algorithm remove_if (p. 897) deletes all elements that satisfy the if condition in a certain range.
- Algorithm remove_copy_if (p. 897) copies all elements that satisfy the if condition in a certain range.

### Section 22.8.4 replace, replace_if, replace_copy and replace_copy_if

- Algorithm replace (p. 899) replaces all elements with a specific value in a certain range.
- Algorithm replace_copy (p. 899) copies all elements with a specific value in a certain range.
- Algorithm replace_if (p. 899) replaces all elements that satisfy the if condition in a certain range.
- Algorithm replace_copy_if (p. 899) copies all elements that satisfy the if condition in a certain range.

### Section 22.8.5 Mathematical Algorithms

- Algorithm random_shuffle (p. 902) reorders randomly the elements in a certain range.
- Algorithm count (p. 902) counts the elements with a specific value in a certain range.
- Algorithm count_if (p. 902) counts the elements that satisfy the if condition in a certain range.
- Algorithm min_element (p. 902) locates the smallest element in a certain range.
- Algorithm max_element (p. 902) locates the largest element in a certain range.
- Algorithm accumulate (p. 902) sums the values in a certain range.
- Algorithm for_each (p. 902) applies a general function or function object to every element in a range.
- Algorithm transform (p. 902) applies a general function or function object to every element in a range and replaces each element with the result of the function.

- Algorithm `equal_range` (p. 915) returns the lower bound and upper bound as a pair.

### Section 22.8.12 Heapsort

- Algorithm `make_heap` (p. 917) takes a sequence of values in a certain range and creates a heap that can be used to produce a sorted sequence.
- Algorithm `sort_heap` (p. 918) sorts a sequence of values in a certain range of a heap.
- Algorithm `pop_heap` (p. 918) removes the top heap element.

### Section 22.8.13 min and max

- Algorithms `min` and `max` (p. 918) determine the minimum of two elements and the maximum of two elements, respectively.

## Section 22.9 Class bitset

- Class template `bitset` (p. 920) makes it easy to create and manipulate bit sets, which are useful for representing a set of bit flags.

## Section 22.10 Function Objects

- A function object (p. 924) is an instance of a class that overloads `operator()`.
- The STL provides many predefined function objects, which can be found in header `<functional>` (p. 924).
- Binary function objects (p. 924) take two arguments and return a value. The `binary_function` class template (p. 926) is an empty base class for creating binary function objects that provides standard type names for the function’s parameters and result.

## Self-Review Exercises

State whether the following are true or false, or fill in the blanks. If the answer is false, explain why.

- 22.1  (T/F) The STL makes use of inheritance and virtual functions.
- 22.2  The two types of first-class STL containers are sequence containers and ______ containers.
- 22.3  The five main iterator types are ______, ______, ______, ______ and ______.
- 22.4  (T/F) An iterator acts like a pointer to an element.
- 22.5  (T/F) STL algorithms can operate on C-like pointer-based arrays.
- 22.6  (T/F) STL algorithms are encapsulated as member functions within each container class.
- 22.7  (T/F) When using the remove algorithm on a vector, the algorithm does not decrease the size of the vector from which elements are being removed.
- 22.8  The three STL container adapters are ______, ______ and ______.
- 22.9  (T/F) Container member functions are used to position and yield the position of the container’s last element.
- 22.10  STL algorithms operate on container elements indirectly, using ______.
- 22.11  The sort algorithm requires a(n) ______ iterator.

## Answers to Self-Review Exercises

- 22.1  False. These are avoided for performance reasons.
- 22.2  Associative.
