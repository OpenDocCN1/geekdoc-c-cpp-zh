When *erasing* from a container, iterators to the *erased* elements are invalidated. In addition:

+   - for a `vector`—Iterators from the erased element to the end of the `vector` are invalidated.
+   - for a `deque`—If an element in the middle of the `deque` is erased, all iterators are invalidated.