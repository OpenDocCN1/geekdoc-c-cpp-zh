
## Section 15.4 Introduction to Algorithms

- The Standard Library algorithms operate on container elements only indirectly through iterators.
- Many algorithms operate on sequences of elements defined by iterators pointing to the first element of the sequence and to one element past the last element.

## Section 15.5 Sequence Containers

- The Standard Library provides sequence containers `array`, `vector`, `forward_list`, `list` and `deque`. Class templates `array`, `vector` and `deque` are based on built-in arrays. Class templates `forward_list` and `list` implement a linked-list data structure.

### Section 15.5.1 `vector` Sequence Container

- Function capacity (p. **669**) returns the number of elements that can be stored in a vector before the vector dynamically resizes itself to accommodate more elements.
- Sequence container function push_back (p. **670**) adds an element to the end of a container.
- `vector` member function cbegin (p. **671**; C++11) returns a `const_iterator` to the `vector`’s first element.
- `vector` member function cend (p. **671**; C++11) returns a `const_iterator` to the location past the last element of the `vector`.
- C++14’s global `cbegin` and `cend` functions work the same way as functions `begin` and `end`, but return `const` iterators that cannot be used to modify the data.
- C++14’s global `rbegin`, `rend`, `crbegin` and `crend` functions support iterating through a built-in array or a container from back to front. Functions `rbegin` and `rend` return iterators that can be used to modify data, and `crbegin` and `crend` return `const` iterators that cannot be used to modify data.
- Functions `begin` and `end` and their C++14 `const` and reverse versions may also receive container objects as arguments—each function calls the corresponding member function in its container argument.
- `vector` member function `crbegin` (p. 672; C++11) returns a `const_reverse_iterator` to the `vector`’s last element.
- `vector` member function `crend` (p. 672; C++11) returns a `const_reverse_iterator` to the location before the first element of the `vector`.
- As of C++11, you can ask a `vector` or `deque` to return unneeded memory to the system by calling member function `shrink_to_fit` (p. 672).
- As of C++11, you can use list initializers to initialize the elements of `vector`s and other containers.
- Algorithm `copy` (p. 674; from header `<algorithm>`) copies each element in a range starting with the location specified by its first iterator argument up to, but not including, the one specified by its second iterator argument.
- Function `front` (p. 674) returns a reference to the first element in a sequence container. Function `begin` returns an iterator pointing to the beginning of a sequence container.
- Function `back` (p. 674) returns a reference to the last element in a sequence container (except `forward_list`). Function `end` returns an iterator pointing to the element one past the end of a sequence container.
- Sequence container function `insert` (p. 675) inserts value(s) before the element at a specific location and returns an iterator pointing to the inserted item or the first of the inserted items.
- Function `erase` (p. 675; in all first-class containers except `forward_list`) removes specific element(s) from the container.
- Function `empty` (p. 675; in all containers and adapters) returns `true` if the container is empty.
- Function `clear` (p. 675; in all first-class containers) empties the container.

### Section 15.5.2 `list` Sequence Container

- The `list` **sequence container** (p. 675; from header `<list>`) implements a doubly linked list that provides an efficient implementation for inserting and deleting anywhere in the container.
- The `forward_list` **sequence container** (p. 676; from header `<forward_list>`) implements a singly linked list that supports only forward iterators.
- `list` member function `push_front` (p. 678) inserts values at the beginning of a list.
- `list` member function `sort` (p. 679) arranges the elements in the list in ascending order.
- `list` member function `splice` (p. 679) removes elements in one `list` and inserts them into another `list` at a specific position.
- `list` member function `unique` (p. 679) removes duplicate elements in a `list`.
- `list` member function `assign` (p. 679) replaces the contents of one `list` with those of another.
- `list` member function `remove` (p. 680) deletes all copies of a specified value from a `list`.

### Section 15.5.3 `deque` Sequence Container

- Class template `deque` (p. 680) provides the same operations as `vector`, but adds member functions `push_front` and `pop_front` (p. 679) to allow insertion and deletion at the beginning of a `deque`, respectively. Header `<deque>` must be included to use class template `deque`.

## Section 15.6 Associative Containers

- The Standard Library’s associative containers provide direct access to store and retrieve elements via **keys** (p. 681).
- The four ordered associative containers are `multiset`, `set`, `multimap` and `map`. The four unordered associative containers are `unordered_multiset`, `unordered_set`, `unordered_multimap` and `unordered_map`. These are nearly identical to their ordered counterparts, but do not maintain keys in sorted order.
- Class templates `multiset` and `set` provide operations for manipulating sets of values where the values are the keys—there is not a separate value associated with each key. Header `<set>` must be included to use class templates `set` and `multiset`.
- A `multiset` allows duplicate keys and a `set` does not.

### Section 15.6.1 `multiset` Associative Container

- The `multiset` **associative container** (p. 682) provides fast storage and retrieval of keys and allows duplicate keys. The key order is determined by a comparator function object. If the order of the keys is not important, you can use `unordered_multiset` (header `<unordered_set>`) instead.
- A `multiset`’s keys can be sorted in ascending order by ordering the keys with comparator function object `less<T>` (p. 682).
- The type of the keys in all associative containers must support comparison properly based on the comparator function object specified.
- A `multiset` supports bidirectional iterators.
- Header `<set>` (p. 682) must be included to use class `multiset`.
- Function `count` (p. 684; available to all associative containers) counts the number of occurrences of the specified value currently in a container.
- Function `find` (p. 684; available to all associative containers) locates a specified value in a container.
- Associative container functions `lower_bound` and `upper_bound` (p. 685) locate the earliest occurrence of the specified value in a container and the element after the value’s last occurrence, respectively.
- Associative container function `equal_range` (p. 685) returns a `pair` containing the results of both a `lower_bound` and an `upper_bound` operation.
- C++ also includes class template `tuple`, which is similar to `pair`, but can hold any number of items of various types.
- As of C++14, the argument to `find` (and other similar functions) can be of any type, provided that there are overloaded comparison operators that can compare values of the argument’s type to values of the container’s key type.

### Section 15.6.2 `set` Associative Container

- The `set` associative container is used for fast storage and retrieval of unique keys. If the order of the keys is not important, you can use `unordered_set` (header `<unordered_set>`) instead.
- If an attempt is made to insert a duplicate key into a `set`, the duplicate is ignored.
- A `set` supports bidirectional iterators.
- Header `<set>` must be included to use class `set`.
