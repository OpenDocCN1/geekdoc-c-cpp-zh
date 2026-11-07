
The four **unordered associative containers** (implemented using hashing⁷,⁸) are

- **`unordered_multiset`**—Rapid lookup, duplicates allowed.
- **`unordered_set`**—Rapid lookup, no duplicates allowed.
- **`unordered_multimap`**—One-to-many mapping, duplicates allowed, rapid key-based lookup.
- **`unordered_map`**—One-to-one mapping, no duplicates allowed, rapid key-based lookup.

## Container Adaptors

The standard library implements **`stack`**, **`queue`** and **`priority_queue`** as container adaptors that enable a program to view a sequence container in a constrained manner. The three container adaptors are

- **`stack`**—Last-in, first-out (LIFO) data structure.
- **`queue`**—First-in, first-out (FIFO) data structure.
- **`priority_queue`**—Highest-priority element is always the first element out.

## Near Containers

There are other container types that are considered near containers—built-in arrays (Chapter 7), bitsets (Section 13.13) for maintaining sets of flag values, strings and valarrays for performing high-speed mathematical vector operations⁹ (not to be confused with the vector container). These types are considered near containers because they exhibit some, but not all, capabilities of the **sequence and associative containers**.

## 13.4.1 Common Nested Types in Sequence and Associative Containers

The table below shows the common types defined inside each sequence and associative container’s class definition. These nested types are used in template-based variable declarations, function parameters and function return types, as you’ll see in this chapter and Chapter 14. For example, each container’s `value_type` always represents the container’s element type.

| Nested type | Description |
|---|---|
| `allocator_type` | The type of object used to allocate the container’s memory—not included in the array container. Containers that use allocators each provide a default allocator, which is sufficient for most programmers. Custom allocators are beyond this book’s scope. |
| `value_type` | The type of the container’s elements. |
| `reference` | The type used to declare a reference to a container element. |
| `const_reference` | The type used to declare a reference to a const container element. |
| `pointer` | The type used to declare a pointer to a container element. |
| `const_pointer` | The type used to declare a pointer to a const container element. |
| `iterator` | An iterator that points to a container element. |
| `const_iterator` | An iterator that points to an element of a const container. Used only to read elements and to perform const operations. |
| `reverse_iterator` | A reverse iterator that points to a container element. Iterates through a container back-to-front. Not provided for `forward_list`. |
| `const_reverse_iterator` | A reverse iterator that points to a container element and can be used only to read elements and to perform const operations. Used to iterate through a container in reverse. Not provided for `forward_list`. |
| `difference_type` | A signed type representing the number of elements between two iterators that refer to elements of the same container. A value of this type is returned by an iterator’s overloaded minus (-) operator and by the function `std::distance`. |
| `size_type` | The unsigned type used to count items in a container and index through a random-access sequence container. |

## 13.4.2 Common Container Member and Non-Member Functions

Most containers provide similar functionality. Many operations apply to all containers, and others apply to specific container categories. The following tables describe the commonly available functions in most standard library containers. Before using any container, you should study its capabilities. For a complete list of all the container member functions and which containers support them, see the **cppreference.com member function table**.<sup>10</sup> Several member functions we do not list in this section are covered throughout the chapter as we present various sequence containers, associative containers and container adaptors.

10. “Container Library—Member Functions Table.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/container.

### Container Special Member Functions

The following table describes the special member functions provided by each container. In addition, each container class typically provides many overloaded constructors for initializing containers and container adaptors in various ways. For example, each sequence and associative container can be initialized from an `initializer_list`.

| Container special member function | Description |
|---|---|
| default constructor | A constructor that initializes an empty container. |
| copy constructor | A constructor that initializes the container to be a copy of an existing container of the same type. |
| copy operator= | Copies the elements of one container into another. |
| move constructor | Moves the contents of an existing container into a new one of the same type. The old container no longer contains the data. This avoids the overhead of copying each element of the existing container. |
| move operator= | Moves the contents of one container into another of the same type. The old container no longer contains the data. This avoids the overhead of copying each element of the existing container. |
| destructor | Destructor function to destroy the container elements. |

### Non-Member Relational and Equality Operators

The `<`, `<=`, `>`, `>=`, `==` and `!=` operators are supported by most containers. In C++17 and earlier, these are overloaded as non-member functions. In C++20, the `<`, `<=`, `>`, `>=` and `!=` operators are synthesized by the compiler using the new three-way comparison operator `<=>` and the `==` operator. As we showed in Section 11.7, the C++ compiler can use `<=>` to implement each relational and equality comparison by rewriting it in terms of `<=>`. For example, the compiler rewrites `x < y` as

`(x <=> y) < 0`

The unordered associative containers do not support `<`, `<=`, `>` and `>=`. The relational and equality operators are not supported for `priority_queue`s.

### Member Functions That Return Iterators

The following table shows container member functions that return iterators. The container `forward_list` does not have the member functions `rbegin`, `rend`, `crbegin` and `crend`.

| Container member function | Description |
|---|---|
| `begin` | Returns an iterator or a `const_iterator` (depending on whether the container is const) referring to the container’s first element. |
| `end` | Returns an iterator or a `const_iterator` (depending on whether the container is const) referring to the next position after the end of the container. |
| `cbegin` | Returns a `const_iterator` referring to the container’s first element. |
| `cend` | Returns a `const_iterator` referring to the next position after the end of the container. |
| `rbegin` | Returns a `reverse_iterator` or a `const_reverse_iterator` (depending on whether the container is const) referring to the container’s last element. |
| `rend` | Returns a `reverse_iterator` or a `const_reverse_iterator` (depending on whether the container is const) referring to the position before the container’s first element. |
| `crbegin` | Returns a `const_reverse_iterator` referring to the container’s last element. |
| `crend` | Returns a `const_reverse_iterator` referring to the position before the container’s first element. |

### Other Member Functions

The following table lists various additional container member functions. If a function is not supported for all containers, we specify which do not support it. For a container’s complete list of member functions, see its documentation page, which you can access from

https://en.cppreference.com/w/cpp/container

| Container member function | Description |
|---|---|
| `clear` | Removes all elements from the container. Not supported for arrays. |
| `contains` | Returns true if the specified key is present in the container; otherwise, returns false. Supported only for associative containers. |
| `empty` | Returns true if the container is empty; otherwise, returns false. |
| `emplace` | Constructs an item in place where it will reside in the container. If there is already an item in that position, it constructs the object in a separate location, then moves it into place with move assignment. Not supported for arrays. A `forward_list` supports `emplace_after` and `emplace_front`, not `emplace`. The associative containers provide `emplace` and `emplace_hint`. |
| `erase` | Removes one or more elements from the container. Not supported for arrays. A `forward_list` supports `erase_after`, not `erase`. |
| `extract` | The associative containers are linked data structures of nodes containing values. Associative container member function `extract` removes a node from the container and returns an object of that container’s `node_type`. |
| `insert` | Inserts an item in the container. This is overloaded to support copy and move semantics. Not supported for arrays. A `forward_list` supports `insert_after`, not `insert`. |
| `max_size` | Returns the maximum number of elements for a container. |
| `size` | Returns the number of elements currently in the container. Not supported for `forward_list`s. |
| `swap` | Swaps the contents of two containers. |
