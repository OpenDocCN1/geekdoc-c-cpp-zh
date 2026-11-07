```
```cpp
val.substr(val.size()-3) == ".de";
});

// print elements up to the new end:
std::cout << "remaining elements:\n";
for (auto pos = coll.begin(); pos != newEnd; ++pos) {
    std::cout << "  " << *pos << "\n";
}

// print all elements in the container:
std::cout << "all elements:\n";
for (const auto& elem : coll) {
    std::cout << "  " << elem << "\n";
}
}
```
```

The output of the program is as follows:

```
```text
remaining elements:
  "jill@company.com"
  "hana@company.com"
all elements:
  "jill@company.com"
  "hana@company.com"
  "sarah@domain.de"
  "MOVED-FROM"
```
```

After “removing” the elements ending with ".de", the new end is the position behind the second element. However, in the container, you still have the third element, which was not moved at all, and the fourth element that has a new moved-from state because it was move-assigned to the second element (which was moved to the first element before).

Be careful when using these moved-from objects, as discussed in the chapter about moved-from states.

# 14.3 Move Iterators

By using *move iterators* (also introduced with C++11), you can use move semantics even in other algorithms and in general wherever input ranges are taken (e.g., in constructors).

However, be careful when using these iterators. While iterating over elements of a container or range, each access to an element uses `std::move()`. This might be significantly faster but it leaves the element in a valid but unspecified state. You should not use an element twice.