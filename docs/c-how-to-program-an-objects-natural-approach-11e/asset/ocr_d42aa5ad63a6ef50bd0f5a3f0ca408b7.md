cessor after each loop iteration. Like sleeping, yielding helps us emphasize that you cannot predict the relative speeds of asynchronous concurrent threads.

Lines 31–32 create `std::jthreads` that each execute `incrementer`. Then, the block terminates, and the `jthreads` go out of scope, automatically joining the threads. Finally, lines 35–37 display the values of `count1`, `atomicCount` and `count2`—`atomicCount`’s load function obtains the object’s integer value. The variable `count2` was incremented indirectly via `atomicRefCount`.

# ### Analyzing the Sample Outputs

Lines 20–29 should increment the `count1`, `atomicCount` and `count2` (indirectly through `atomicRefCount`) 2,000 times. However, the sample outputs show that incrementing the `int count` from concurrent threads **without synchronization** can produce different totals each time, including the seemingly correct total in the first output. Incrementing `atomicCount` and incrementing `count2` indirectly through `atomicRefCount` from concurrent threads **without synchronization** is guaranteed to produce the proper total of 2,000 for each.

# ### More About Atomic Types<sup>94,95</sup>

There are predefined `std::atomic` class template specializations and corresponding type aliases for type `bool` and every integral type. You also can specialize `std::atomic` for

+   - pointer types,
+   - floating-point types and
+   - trivially copyable types<sup>96</sup>—that is, the compiler provides the copy and move constructors, copy and move assignment operators, and destructor, and there are no virtual functions.

The specializations for integral, pointer and, as of C++20, floating-point types each support adding a value to or subtracting a value from an atomic data item. The integral specializations also provide atomic bitwise `&=` (and), `|=` (or) and `^=` (xor) operations.

# ### C++20 Atomic Smart Pointers and Atomic Pointers<sup>97,98</sup>

C++20 adds atomic smart pointer specializations for `std::atomic<std::shared_ptr<T>>` and `std::atomic<std::weak_ptr<T>>`, enabling atomic pointer manipulations of these smart pointer types.

For all atomic pointers, only the pointer manipulations are atomic—for example,

+   - aiming the pointer at a different object,
+   - incrementing the pointer by an integer or
+   - decrementing the pointer by an integer.

Atomic pointers can be used to implement thread-safe, linked data structures.