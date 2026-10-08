We left out **array** and **forward_list** because they are imperfect fits to the standard library ideal of interchangeability:

+   * **array** is not a handle, cannot have its number of elements changed after initialization, and must be initialized by an initializer list, rather than by a constructor.
* **forward_list** doesn’t support back operations. In particular, it has no **size()**. It is best seen as a container optimized for empty and near-empty sequences.

# ### B.4.2 Member types

A container defines a set of member types:

| Member types |
| :--- |
| **value_type** | type of element |
| **size_type** | type of subscripts, element counts, etc. |
| **difference_type** | type of difference between iterators |
| **iterator** | behaves like **value_type**\* |
| **const_iterator** | behaves like **const value_type**\* |
| **reverse_iterator** | behaves like **value_type**\* |
| **const_reverse_iterator** | behaves like **const value_type**\* |
| **reference** | **value_type**\& |
| **const_reference** | **const value_type**\& |
| **pointer** | behaves like **value_type**\* |
| **const_pointer** | behaves like **const value_type**\* |
| **key_type** | type of key (associative containers only) |
| **mapped_type** | type of mapped value (associative containers only) |
| **key_compare** | type of comparison criterion (associative containers only) |
| **allocator_type** | type of memory manager |