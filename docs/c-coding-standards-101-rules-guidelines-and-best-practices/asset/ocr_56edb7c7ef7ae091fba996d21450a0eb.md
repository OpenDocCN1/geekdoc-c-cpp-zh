# # 86. Use the right STL sort algorithm.

# ## Summary

Sort “just enough:” Understand what each of the sorting algorithms does, and use the cheapest algorithm that does what you need.

# ## Discussion

You don’t always need a full sort; you usually need less, and rarely you need more. In general order from cheapest to most expensive, your standard sorting algorithm options are: `partition`, `stable_partition`, `nth_element`, `partial_sort` (with its variant `partial_sort_copy`), `sort`, and `stable_sort`. Use the least expensive one that does the work you actually need; using a more powerful one is wasteful.

`partition`, `stable_partition`, and `nth_element` run in linear time, which is nice.

`nth_element`, `partial_sort`, `sort`, and `stable_sort` require random-access iterators. You can’t use them if you have only bidirectional iterators (e.g., `list<T>::iterators`). If you need these algorithms but you don’t have random-access iterators, consider using the index container idiom: Create a container that supports random-access iterators (e.g., a `vector`) of iterators into the range you have, and then use the more powerful algorithm on that using a dereferencing version of your predicate (one that dereferences the iterators before doing its usual comparison).

Use the `stable_...` versions only if you need to preserve the relative ordering of equal elements. Note that `partial_sort` and `nth_element` aren’t stable (meaning that they don’t keep equivalent elements in the same relative order they were in before the sort), and they have no standardized stable versions. If you otherwise want these algorithms but need stability, you probably want `stable_sort`.

Of course, don’t use any sorting algorithm at all if you don’t have to: If you are using a standard associative container (`set/multiset` or `map/multimap`) or the `priority_queue` adapter, and only need one sort order, the elements in the container stay sorted all the time.

# ## Examples

*Example 1: `partition`. Use `partition` to just divide the range into two groups: all elements that satisfy the predicate, followed by all elements that don’t. This is all you need to answer questions like these:*