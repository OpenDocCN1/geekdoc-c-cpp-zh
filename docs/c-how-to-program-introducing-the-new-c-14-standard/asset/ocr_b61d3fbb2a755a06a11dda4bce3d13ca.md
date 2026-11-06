# `vector` *Member Function* `erase`

Lines 40 and 45 use the two `erase` functions that are available in all *first-class containers* (except `array`, which has a fixed size, and `forward_list`, which has the function `erase_after` instead). Line 40 erases the element at the location specified by the iterator argument (in this example, the first element). Line 45 specifies that all elements in the range specified by the two iterator arguments should be erased. In this example, all the elements are erased. Line 47 uses function `empty` (available for all containers and adapters) to confirm that the `vector` is empty.

![](bbox=[0.119, 0.489, 0.194, 0.546])

# Common Programming Error 15.3

*Normally `erase` destroys the objects that are erased from a container. However, erasing an element that is a pointer to a dynamically allocated object does not `delete` the dynamically allocated memory—this can lead to a memory leak. If the element is a `unique_ptr` (Section 17.9), the `unique_ptr` would be destroyed and the dynamically allocated memory would be deleted. If the element is a `shared_ptr` (Chapter 24), the reference count to the dynamically allocated object would be decremented and the memory would be deleted only if the reference count reached `0`.*