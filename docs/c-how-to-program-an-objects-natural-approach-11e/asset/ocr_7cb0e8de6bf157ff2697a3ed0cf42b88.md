| Nested type | Description |
|---|---|
| `allocator_type` | The type of object used to allocate the container’s memory—not included in the array containers. Containers that use allocators each provide a default allocator, which is sufficient for most programmers. Custom allocators are beyond this book’s scope. |
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

# ### 13.4.2 Common Container Member and Non-Member Functions

Most containers provide similar functionality. Many operations apply to all containers, and others apply to specific container categories. The following tables describe the commonly available functions in most standard library containers. Before using any container, you should study its capabilities. For a complete list of all the container member functions and which containers support them, see the **cppreference.com member function table**.<sup>10</sup> Several member functions we do not list in this section are covered throughout the chapter as we present various sequence containers, associative containers and container adaptors.

# #### Container Special Member Functions

The following table describes the special member functions provided by each container. In addition, each container class typically provides many overloaded constructors for initializing containers and container adaptors in various ways. For example, each sequence and associative container can be initialized from an `initializer_list`.

10. “Container Library—Member Functions Table.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/container.