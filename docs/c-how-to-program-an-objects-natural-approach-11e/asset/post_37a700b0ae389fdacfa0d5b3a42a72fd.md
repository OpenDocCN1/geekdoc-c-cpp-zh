
ranges. It’s also possible to create your own new algorithms that operate in a similar fashion so they can be used with the standard library containers and iterators. In this chapter, we’ll use the copy algorithm in many examples to copy a container’s contents to the standard output. We discuss many standard library algorithms in Chapter 14.

## 13.7 Sequence Containers

The C++ standard library provides five sequence containers—**array, vector, deque, list** and **forward_list**. The array, vector and deque containers are typically based on built-in arrays. The list and forward_list containers implement linked-list data structures. We’ve already discussed and used array extensively in Chapter 6, so we do not cover it again here. We’ve also already introduced vector in Chapter 6—and we discuss it in more detail here.

### Performance and Choosing the Appropriate Container

Section 13.4.2 presented the operations common to most standard library containers. Beyond these operations, each container typically provides various other capabilities. Many are common to several containers, but they’re not always equally efficient. The C++ Core Guidelines say **vector is satisfactory for most applications.**¹¹ However, you should profile your application to ensure the container you choose is the correct one for your use-case and performance requirements.

**Insertion at the back of a vector is efficient.** The vector grows, if necessary, to accommodate the new item. It’s expensive to insert (or delete) an element at the front or in the middle of a vector. Every item after the insertion (or deletion) point must be moved because **vector elements occupy contiguous cells in memory.**

For applications that require frequent insertions and deletions at both ends of a container, use a **deque** rather than a vector. A deque does not move any elements for insertions and deletions at the front,¹² making it more efficient than vector.¹³

Applications with frequent insertions and deletions in the middle and/or at the extremes of a container sometimes use a **list** due to its efficient implementation of insertion and deletion anywhere in the data structure.

- 11. C++ Core Guidelines, “SL.con.2: Prefer Using STL vector By Default Unless You Have a Reason to Use a Different Container.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rsl-vector.
- 12. “std::deque.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/container/deque.
- 13. “std::vector.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/container/vector.

## 13.8 vector Sequence Container

The **vector** container (introduced in Section 6.15) is a dynamic data structure with contiguous memory locations. It provides rapid indexed access with the overloaded subscript operator **[]**. **Choose the vector container for the best random-access performance in a container that can grow.** When a vector’s capacity is exceeded, it

- allocates a larger built-in array,
- copies or moves (depending on what the element type supports) the original elements into the new built-in array
- deallocates the old built-in array.

### 13.8.1 Using vectors and Iterators

Figure 13.2 illustrates several vector member functions, many of which are available in every sequence container and associative container. As we add items to a vector<int> in this example, we call our showResult function (lines 9–12) to display the new value as well as the vector’s

- **size**—the number of elements it currently contains and
- **capacity**—the number of elements it can store before it needs to dynamically resize itself to accommodate more elements.

```cpp
// fig13_02.cpp
// Standard library vector class template.
#include <format>
#include <iostream>
#include <ranges>
#include <vector> // vector class-template definition

// display value appended to vector and updated vector size and capacity
void showResult(int value, size_t size, size_t capacity) {
    std::cout << std::format("appended: {}; size: {}; capacity: {}\n",
                              value, size, capacity);
}
```

**Fig. 13.2** | Standard library vector class template.

### Creating a vector and Displaying Its Initial Size and Capacity

Line 15 defines the vector<int> object integers. vector’s default constructor creates an empty vector with its size and capacity set to 0. So, the vector will have to allocate memory when elements are added to it. Lines 17–18 display the size and capacity. Function size returns the number of elements currently stored in the container.¹⁴ Function capacity returns the vector’s current capacity.

- 14. forward_list does not have the size member function.

```cpp
int main() {
    std::vector<int> integers{}; // create vector of ints

    std::cout << "Size of integers: " << integers.size()
              << "\nCapacity of integers: " << integers.capacity() << "\n\n";
}
```

```text
Size of integers: 0
Capacity of integers: 0
```

### vector Member Function push_back

Lines 21–24 call push_back to append one element at a time to the vector. Each loop iteration calls showResult to display the added item and the vector’s new size and capacity. Function push_back is available in sequence containers other than array and forward_list. Sequence containers other than array and vector also provide a push_front function. If the vector’s **size equals its capacity** when you add a new element, the vector increases its capacity to accommodate more elements.

```cpp
// append 1-10 to integers and display updated size and capacity
for (int i : std::views::iota(1, 11)) {
    integers.push_back(i);  // push_back is in vector, deque and list
    showResult(i, integers.size(), integers.capacity());
}
```

```text
appended: 1; size: 1; capacity: 1
appended: 2; size: 2; capacity: 2
appended: 3; size: 3; capacity: 3
appended: 4; size: 4; capacity: 4
appended: 5; size: 5; capacity: 6
appended: 6; size: 6; capacity: 6
appended: 7; size: 7; capacity: 9
appended: 8; size: 8; capacity: 9
appended: 9; size: 9; capacity: 9
appended: 10; size: 10; capacity: 13
```

### Updated size and capacity After Modifying a vector

The C++ standard does not specify how a vector grows to accommodate more elements—a time-consuming operation. **Some implementations double the vector’s capacity.** Others increase the capacity by 1.5 times, as shown in the output from Visual C++. This becomes apparent starting when the size and capacity are both 4:

- When we appended 5, the vector increased the capacity from 4 to 6, and the size became 5, leaving room for one more element.
- When we appended 6, the capacity remained at 6, and the size became 6.
- When we appended 7, the vector increased the capacity from 6 to 9, and the size became 7, leaving room for two more elements.
- When we appended 8, the capacity remained at 9, and the size became 8.
- When we appended 9, the capacity remained at 9, and the size became 9.
- When we appended 10, the vector increased the capacity from 9 to 13 (1.5 times 9 rounded down to the nearest integer), and the size became 10, leaving room for three more elements before the vector will need to allocate more space.

### vector Growth in g++

C++ library implementers use various schemes to minimize vector resizing overhead, so this program’s output may vary based on your compiler’s vector growth implementation. GNU g++, for example, doubles a vector’s capacity when more room is needed, producing the following output:

```text
appended: 1; size: 1; capacity: 1
appended: 2; size: 2; capacity: 2
appended: 3; size: 3; capacity: 4
appended: 4; size: 4; capacity: 4
appended: 5; size: 5; capacity: 8
appended: 6; size: 6; capacity: 8
appended: 7; size: 7; capacity: 8
appended: 8; size: 8; capacity: 8
appended: 9; size: 9; capacity: 16
appended: 10; size: 10; capacity: 16
```

### Other vector Sizing Considerations

Some programmers allocate a large initial capacity. If a vector stores a small number of elements, such capacity may waste space. However, it can greatly improve performance if a program adds many elements to a vector and does not have to reallocate memory to accommodate those elements. This is a classic space-time trade-off. Library implementors must balance the amount of memory used against the time required to perform various vector operations.

It can be wasteful to double a vector’s size when more space is needed. For example, in a vector implementation that doubles the allocated memory when space is needed, a full vector of 1,000,000 elements resizes to accommodate 2,000,000 elements even when only one new element is added. This leaves 999,999 unused elements. You can use member functions **reserve** to control space usage better.

### Outputting vector Contents with Iterators

Lines 28–31 output the vector’s contents. Line 28 initializes the control variable const_iterator using vector member function cbegin, which returns a const_iterator to the vector’s first element. We use **auto** to infer the control variable’s type `vector<int>::const_iterator` which simplifies the code and reduces errors when working with more complex types.

```cpp
26      std::cout << "\nOutput integers using iterators: ";
27
28      for (auto constIterator{integers.cbegin()};
29           constIterator != integers.cend(); ++constIterator) {
30          std::cout << *constIterator << ' ';
31      }
32
```

```text
Output integers using iterators: 1 2 3 4 5 6 7 8 9 10
```

The loop continues as long as constIterator has not reached the vector’s end. This is determined by comparing constIterator to the result of calling the vector’s cend function. When constIterator equals this value, the loop terminates. **Attempting to dereference an iterator positioned outside its container is a logic error. The iterator returned by end or cend should never be dereferenced or incremented.**
