# 6.3 Dealing with Broken Invariants

Unfortunately, moved-from objects can break the “valid but unspecified state” guarantee a lot easier than breaking the requirement to be destructible. We can accidentally bring objects into a state where we break their invariants.

Fortunately, this is only a problem if move semantics is explicitly requested, because temporary objects are destroyed immediately anyway. However, an explicit request to move might not only be caused by marking an object with std::move(). You can create moved-from objects with:

+   - `std::move()` for an object
+   - Moving algorithms (`std::move()` and `std::move_backward()`)
+   - Algorithms that “remove” elements by moving “non-removed” elements to the front (e.g., `std::remove()`, `std::remove_if()`, `std::unique()`)
+   - Move iterators

In principle, if the invariants of a class are broken by a (generated) move operation, you have the following options:

+   - Fix the move operations to bring the moved-from objects into a state that does not break the invariants.
+   - Disable move semantics.
+   - Relax the invariants that define all possible moved-from states also as valid. In particular, this might mean that member functions and functions that use the objects have to be implemented differently to deal with the new possible states.
+   - Document and provide a member function to check for the state of “broken invariants” so that users of the type do not use an object of this type after it has been marked with `std::move()` (or only use a limited set of operations).

Let us look at some examples of broken invariants and discuss how to fix them.

# 6.3.1 Breaking Invariants Due to a Moved Value Member

The first reason for move operations breaking invariants relates to objects where the moved-from state of a member is a problem in itself because the state is valid but should not happen.

+   - Disabling move semantics (which would be the behavior here without declaring special move member functions)

According to the Rule of Zero, you should encapsulate error-prone resource management in a helper type so that application programmers have to implement zero special member functions. In this case, you might use a helper class (template) that provides both members (the std::array and a member for the actual number of elements used) and a correct implementations of the move operations.

The whole problem is also a side effect of a design mistake of class std::thread. The type does not follow the RAII principle. For all std::threads with running threads, you have to call join() (or detach()) before their destructor is called; otherwise the destructor of a thread throws. Since C++20, you could and should use class std::jthread instead, which will automatically call join() if the object still represents a running thread.