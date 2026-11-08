underlying. That holds for a `std::span` with a dynamic extent (line 15) and a `std::span` with a static extent (line 17). Doing it the other way around (line 18) or trying to initialize a `std::span<long>` with a `std::span<int>` gives a compile-time error.

You can use a `std::span` with static extent to initialize a `std::span` with dynamic extent (line 28). Initializing a `std::span` with static extent with a `std::span` with dynamic extent is undefined behavior if the sizes of the `std::span`'s differ (line 29). Furthermore, it causes a compile-time error when you use `std::span`'s with static extent to initialize a `std::span` with static extent, both having a different size.

One important reason for having a `std::span<T>` is that a plain C-array decays to a pointer if passed to a function; therefore, the size is lost. This decay is a typical reason for errors in C/C++.

# 5.2.3 Automatically Deduces the Size of a Contiguous Sequence of Objects

In contrast to a C-array, `std::span<T>` automatically deduces the size of contiguous sequences of objects.

A `std::span` automatically deduces the size of its referenced sequence of objects

```
```cpp
1  // printSpan.cpp
2  
3  #include <iostream>
4  #include <vector>
5  #include <array>
6  #include <span>
7  
8  void printMe(std::span<int> container) {
9  
10     std::cout << "container.size(): " << container.size() << '\n';
11     for (auto e : container) std::cout << e << ' ';
12     std::cout << "\n\n";
13 }
14 
15 int main() {
16 
17     std::cout << '\n';
18 
19     int arr[]{1, 2, 3, 4};
20     printMe(arr);
21 
22     std::vector vec{1, 2, 3, 4, 5};
23     printMe(vec);
```
```