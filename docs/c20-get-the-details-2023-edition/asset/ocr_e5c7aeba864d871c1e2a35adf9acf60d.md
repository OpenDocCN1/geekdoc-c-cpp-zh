# Possible resizing of the underlying contiguous range

```
```cpp
std::vector<int> myVec{1, 2, 3, 4, 5};

std::span<int> sp1{myVec};

myVec.push_back(6); // undefined behavior
```
```

The statement `myVec.push_back(6)` can trigger a reallocation of the container. Consequently, `myVec.push_back()` causes undefined behavior.

![](bbox=[0.119, 0.325, 0.176, 0.369])

# Distilled Information

+   - A `std::span` is an object that refers to a contiguous sequence of objects. A `std::span`, also known as view, is never an owner and, therefore, does not allocate memory. The contiguous sequence of objects can be a plain C-array, a pointer with a size, a `std::array`, a `std::vector`, or a `std::string`.
+   - A `std::span` can have a static extent or a dynamic extent. The size of a `std::span` with static extent is known at compile time and cannot be changed.
+   - In contrast to a C-array, a `std::span` automatically deduces the size of its referenced sequence of objects.
+   - When a `std::span` modifies its elements, the reference objects are also modified.
+   - Using a `std::span` on a temporary or changing the size of the underlying range is undefined behavior.