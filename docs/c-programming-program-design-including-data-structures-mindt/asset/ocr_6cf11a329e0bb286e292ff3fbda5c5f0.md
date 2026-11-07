# TABLE 21-21  Containers, Their Associated Header Files, and the Type of Iterator Supported by Each Container

| Sequence containers | Associated header file | Type of iterator support |
|---|---|---|
| `vector` | `<vector>` | Random access |
| `deque` | `<deque>` | Random access |
| `list` | `<list>` | Bidirectional |
| Associative containers | Associated header file | Type of iterator support |
| `map` | `<map>` | Bidirectional |
| `multimap` | `<map>` | Bidirectional |
| `set` | `<set>` | Bidirectional |
| `multiset` | `<set>` | Bidirectional |
| Adapters | Associated header file | Type of iterator support |
| `stack` | `<stack>` | No iterator support |
| `queue` | `<queue>` | No iterator support |
| `priority_queue` | `<queue>` | No iterator support |

# Algorithms

Several operations can be defined for a container. Some of the operations are very specific to a container and, therefore, are provided as part of the container definition (that is, as member functions of the class implementing the container). However, several operations—such as find, sort, and merge—are common to all containers. These operations are provided as generic algorithms and can be applied to all containers, as well as the built-in array type. The algorithms are bound to a particular container through an iterator pair.

The generic algorithms are contained in the header file algorithm. This section describes several of these algorithms and shows how to use them in a program. Because algorithms are implemented with the help of functions, in this section, the terms function and algorithm mean the same thing.