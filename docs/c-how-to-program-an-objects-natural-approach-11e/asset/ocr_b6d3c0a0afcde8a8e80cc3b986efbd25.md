| Container member function (Cont.) | Description |
|---|---|
| `rend` | Returns a `reverse_iterator` or a `const_reverse_iterator` (depending on whether the container is const) referring to the position before the container’s first element. |
| `crbegin` | Returns a `const_reverse_iterator` referring to the container’s last element. |
| `crend` | Returns a `const_reverse_iterator` referring to the position before the container’s first element. |

# Other Member Functions

The following table lists various additional container member functions. If a function is not supported for all containers, we specify which do not support it. For a container’s complete list of member functions, see its documentation page, which you can access from

https://en.cppreference.com/w/cpp/container

| Container member function | Description |
|---|---|
| `clear` | Removes all elements from the container. Not supported for arrays. |
| `contains` | Returns true if the specified key is present in the container; otherwise, returns false. Supported only for associative containers. |
| `empty` | Returns true if the container is empty; otherwise, returns false. |
| `emplace` | Constructs an item in place where it will reside in the container. If there is already an item in that position, it constructs the object in a separate location, then moves it into place with move assignment. Not supported for arrays. A forward_list supports emplace_after and emplace_front, not erase. The associative containers provide emplace and emplace_hint. |
| `erase` | Removes one or more elements from the container. Not supported for arrays. A forward_list supports erase_after, not erase. |
| `extract` | The associative containers are linked data structures of nodes containing values. Associative container member function extract removes a node from the container and returns an object of that container’s node_type. |
| `insert` | Inserts an item in the container. This is overloaded to support copy and move semantics. Not supported for arrays. A forward_list supports insert_after, not insert. |
| `max_size` | Returns the maximum number of elements for a container. |
| `size` | Returns the number of elements currently in the container. Not supported for forward_lists. |
| `swap` | Swaps the contents of two containers. |