you should be aware of the management overhead of
list.

+   * vector versus set
If all elements always need to be sorted, then use a set. However, read in the next section that it is worth considering whether you can split your work into a writing phase and a reading phase, because then vector and sort between the phases are the best solution.

+   * vector versus map
If you need an association from a key to a target, a map is usually the best choice.

There are a few key tips to keep in mind when using\vector.

You should add new elements to the back as often as possible. You do this with push_back or emplace_back. You should also remove elements from the back. The method for this is called pop_back.

If you already know or estimate how many elements you will insert, you should request this amount with reserve. The automatic growth of vector is surprisingly efficient, but if you can avoid it, why not?

| 26.1.2 Always Sorted: "set", "map", "multiset", and "multimap"

Before using vector (or list) to keep elements constantly sorted, you should prefer one of the ordered associative container types. An insert in the middle of a vector is really expensive. Because the elements in a vector are