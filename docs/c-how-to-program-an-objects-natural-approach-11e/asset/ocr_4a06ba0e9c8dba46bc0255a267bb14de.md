# forward_list Container

The `forward_list` sequence container (header `<forward_list>`) is implemented as a singly linked list—every node contains a pointer to the next node in the `forward_list`. This enables a `forward_list` to support forward iterators that allow the container to be traversed in the forward direction. Any algorithm that requires input, output or forward iterators can operate on a `forward_list`.

# list Member Functions

In addition to the common sequence container member functions discussed in Section 13.4, `list` provides member functions `splice`, `push_front`, `pop_front`, `emplace_front`, `emplace_back`, `remove`, `remove_if`, `unique`, `merge`, `reverse` and `sort`. Several of these are `list`-optimized implementations of standard library algorithms we show in Chapter 14. Both `push_front` and `pop_front` are also supported by `forward_list` and `deque`. Figure 13.4 demonstrates several `list` features. Many of the functions presented in Figs. 13.2–13.3 also can be used with `list`s. We focus on the new features in this example's discussion.

```
```cpp
1  // Fig13_04.cpp
2  // Standard Library list class template.
3  #include <algorithm> // copy algorithm
4  #include <iostream>
5  #include <iterator> // ostream_iterator
6  #include <list> // list class-template definition
7  #include <vector>
8
9  // printList function template definition; uses
10 // ostream_iterator and copy algorithm to output list elements
11 template <typename T>
12 void printList(const std::list<T>& items) {
13    if (items.empty()) { // list is empty
14       std::cout << "List is empty";
15    }
16    else {
17       std::ostream_iterator<T> output{std::cout, " "};
18       std::ranges::copy(items, output);
19    }
20 }
21
```
```

**Fig. 13.4** | Standard library `list` class template.

Function template `printList` (lines 11–20) checks whether its `list` argument is empty (line 13) and, if so, displays an appropriate message. Otherwise, `printList` uses an `ostream_iterator` and the `std::ranges::copy` algorithm to copy the `list`'s elements to the standard output, as shown in Fig. 13.3.