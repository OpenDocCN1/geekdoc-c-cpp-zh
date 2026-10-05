```
functions lower_bound() or binary_search() from <algorithm>. This is done using binary search and is therefore just as fast as set—probably even faster as vector has better locality behavior, meaning the data is stored in a more CPU-friendly manner in memory.
```

# Binary Search

This is a standard procedure to ensure that a desired element can be found in a sorted sequence of elements with a few steps. In this process, the middle element of the sequence is successively selected and then searched either to the right or left, depending on whether the middle element is greater or smaller than the desired element. This guarantees that the desired element is found after a maximum of log n steps or it is known that it is not in the list.

The disadvantage of this procedure is that you keep more elements in the vector during the insertion phase than in a set. This means that vector loses its speed advantage over set if you expect many duplicates. When exactly this happens depends on many factors. As a rule of thumb, I would recommend using vector as a set replacement is worthwhile if you expect more than about 1,000,000 elements and more than half of them remain unique. For fewer elements, the additional effort in implementation is hardly worthwhile, and for fewer unique elements (i.e., more duplicates), set saves memory.