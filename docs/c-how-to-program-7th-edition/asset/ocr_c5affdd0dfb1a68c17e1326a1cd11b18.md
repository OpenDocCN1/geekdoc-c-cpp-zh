variables, parameters to functions and return values from functions. For example, `value_type` in each container is always a typedef that represents the type of value stored in the container.

| Header | Description |
| --- | --- |
| `<vector>` | |
| `<list>` | |
| `<deque>` | |
| `<queue>` | Contains both queue and priority_queue. |
| `<stack>` | |
| `<map>` | Contains both map and multimap. |
| `<set>` | Contains both set and multiset. |
| `<valarray>` | |
| `<bitset>` | |

Fig. 22.3 | Standard Library container header files.

| typedef | Description |
| --- | --- |
| allocator_type | The type of the object used to allocate the container's memory. |
| value_type | The type of element stored in the container. |
| reference | A reference to the type of element stored in the container. |
| const_reference | A constant reference to the type of element stored in the container. Such a reference can be used only for reading elements in the container and for performing const operations. |
| pointer | A pointer to the type of element stored in the container. |
| const_pointer | A pointer to a constant of the container's element type. |
| iterator | An iterator that points to an element of the container's element type. |
| const_iterator | A constant iterator that points to the type of element stored in the container and can be used only to read elements. |
| reverse_iterator | A reverse iterator that points to the type of element stored in the container. This type of iterator is for iterating through a container in reverse. |
| const_reverse_iterator | A constant reverse iterator that points to the type of element stored in the container and can be used only to read elements. This type of iterator is for iterating through a container in reverse. |
| difference_type | The type of the result of subtracting two iterators that refer to the same container (operator - is not defined for iterators of lists and associative containers). |
| size_type | The type used to count items in a container and index through a sequence container (cannot index through a list). |

Fig. 22.4 | typedefs found in first-class containers.