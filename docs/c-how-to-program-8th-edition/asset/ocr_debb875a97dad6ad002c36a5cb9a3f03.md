| Member function | Description |
|---|---|
| `erase` | Erases one or more elements from the container. |
| `clear` | Erases all elements from the container. |

**Fig. 22.3**  |  Common member functions for most STL containers. (Part 2 of 2.)

# ### STL Container Headers

The headers for each of the Standard Library containers are shown in Fig. 22.3. The contents of these headers are all in namespace `std`.

# ### First-Class Container Common typedefs

Figure 22.4 shows the common typedefs (to create synonyms or aliases for lengthy type names) found in first-class containers. These typedefs are used in generic declarations of variables, parameters to functions and return values from functions. For example, `value_type` in each container is always a typedef that represents the type of elements stored in the container.

| Standard Library container headers |
|---|
| `<vector>` |
| `<list>` |
| `<deque>` |
| `<queue>` — Contains both queue and priority_queue. |
| `<stack>` |
| `<map>` — Contains both map and multimap. |
| `<set>` — Contains both set and multiset. |
| `<valarray>` |
| `<bitset>` |

**Fig. 22.3**  |  Standard Library container headers.

| typedef | Description |
|---|---|
| `allocator_type` | The type of the object used to allocate the container’s memory. |
| `value_type` | The type of element stored in the container. |
| `reference` | A reference for the container’s element type. |
| `const_reference` | A constant reference for the container’s element type. Such a reference can be used only for reading elements in the container and for performing const operations. |
| `pointer` | A pointer for the container’s element type. |

**Fig. 22.4**  |  typedefs found in first-class containers. (Part 1 of 2.)