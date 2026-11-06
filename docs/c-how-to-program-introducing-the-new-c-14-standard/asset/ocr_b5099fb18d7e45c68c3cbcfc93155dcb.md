elements resizes to accommodate 2,000,000 elements when a new element is added, leaving 999,999 unused elements. You can use `reserve` and `shrink_to_fit` to control space usage better.

+   M. As of C++11, you can ask a `vector` or `deque` to return unneeded memory to the system by calling member function `shrink_to_fit`.

+   N. The associative containers provide direct access to store and retrieve elements via keys (often called search keys). The ordered associative containers are `multiset`, `set`, `map`, and `multimap`.

+   O. Classes `set` and `multiset` provide operations for manipulating sets of values where the values are the keys—there is *not* a separate value associated with each key.

+   P. We use C++11’s `auto` keyword to deduce the type of a variable from its initializer.

+   Q. A `multimap` is implemented to efficiently locate all values paired with a given key.

+   R. The Standard Library container adapters are `stack`, `queue` and `priority_queue`.

# Discussion Questions

+   1. 15.6 Why is it expensive to insert (or delete) an element in the middle of a `vector`?