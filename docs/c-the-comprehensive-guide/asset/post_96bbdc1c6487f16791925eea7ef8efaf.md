
You only notice it when you request memory that is theoretically available but can no longer be provided to you. Yes, there are solutions for this, but they are situation-dependent. One of the possible solutions is this: use a vector.

> **Noteworthy Special Case: “vector<bool>”**
> 
> A `vector<bool>` is optimized for low memory usage. It packs the elements tightly—that is, eight bools per byte. Chapter 24, Table 24.12 presents the different alternatives for storing many bool values.

### 26.1.6 Size Dynamic: All Except “array”

`array<int,5>` means space for five. Not four, not six, but five. You can neither remove elements from the array nor add any. All other containers grow with their tasks: they start empty and with possibly preallocated memory and grow dynamically as you add more elements. In most cases, you don't have to worry about the additional overhead when growing.

But there are exceptions. Here are the facts about the growth of containers in the C++ standard library:

- `array` cannot grow.
- `list` and `forward_list` manage singly linked elements. They behave optimally when growing: the elements are inserted individually and independently into the data structure. However, many small memory allocations can cause a lot of memory fragmentation.
- `vector` can grow well, but it is not optimal. Occasionally, `vector` has to double its size and temporarily occupies three times the memory actually needed for the elements, but it immediately releases one-third of it. However, the memory does not fragment, even if you store many small elements.
- The ordered associative containers link elements individually in a tree-like structure. This is also good for growth. However, parts of the tree need to be rearranged when inserting, which involves some effort.
- The unordered associative containers also store the elements individually linked, which is good for adding elements one by one. However, the hash table occasionally needs to be resized. To estimate the effort of resizing, assume the hash table is a vector with approximately as many pointers as the container has elements.
- The `deque` has the most degrees of freedom when it comes to implementation. It grows well, at worst like a vector. However, it is more likely that memory is requested in larger chunks and not as much temporary storage is needed.

That's all there is to say about growth. But what about shrinking?

- You can't remove anything from an `array`.
- `list` and `forward_list` as well as all associative containers manage their elements individually, and removing an element also frees its memory. Only in the case of unordered associative containers might the hash table not be affected by shrinking.
- `vector` does not shrink when you remove elements. The maximum space that a `vector` once required will continue to be required, even if you delete elements. You can explicitly call `shrink_to_fit`, which releases (parts of) the excess memory. The implementation may do this, but it doesn't have to. However, all implementations known to me support `shrink_to_fit` to the next larger power of two. Note that you should not call `shrink_to_fit` after every removal.
- `deque` can be implemented like `vector` and therefore has `shrink_to_fit`, but it can also be implemented with blocks and automatically behave better regarding removal.

## 26.2 Recipes for Containers

After the general guide to container selection, I will show you some specific recipes for handling containers. I have chosen problems that frequently occur in practice:

- Is a `set` really the right container for a sorted collection?
- How do I output the contents of a container?
- Can I really not add an element to an `array`?

Answering these questions in the following sections also helps in understanding some fundamental aspects of C++ and the standard library: the linear memory layout of `vector`, the interaction between streams and containers, and the moving of values.

### 26.2.1 Two Phases: “vector” as a Good “set” Replacement

Note that whenever your use of `set` splits into two distinct phases for filling and reading, you should prefer using a `vector`. A `set` keeps its elements sorted at all times and incurs some overhead with every insertion. Often, it is better to first dump all elements into a `vector` using `push_back()` and then sort them in one go with `sort()` from the header `<algorithm>`.

```cpp
// https://godbolt.org/z/T4d4jdqox
#include <vector>
#include <iostream>
#include <algorithm>
using std::vector; using std::ostream; using std::cout;
int main() {
vector<int> data{};
data.reserve(400);                    // Space for 400 elements
// Phase 1: fill
for(int idx = 1; idx < 20; ++idx) {
    for(int val = 0; val < 20; ++val) {
        data.push_back(val % idx);    // something between 0 and 19
    }
}
cout << data.size() << '\n';          // 400 elements between 0 and 19
// Post-processing Phase 1: create set-equivalent
std::sort(data.begin(), data.end());  // preparation for unique
auto wo = std::unique(data.begin(), data.end()); // duplicates to the end
data.erase(wo, data.end());            // remove duplicates
data.shrink_to_fit();
cout << data.size() << '\n';          // only 20 elements left
// Phase 2: use
for (auto &e : data)
    cout << e << ' ';                 // Output: 0 1 2 ... 18 19
cout << '\n';
auto it = std::find(data.begin(), data.end(), 16); // search value
if (it != data.end() && *it == 16)
    cout << "found!\n";
if (std::binary_search(data.begin(), data.end(), 7))  // yes or no
    cout << "also found!\n";
}
```

**Listing 26.1** With a “vector,” you can simulate a “set.”

If you then iterate over the elements of the vector, you get the same result as with a `multiset`. To simulate a `set`, follow the call to `sort()` with a call to `unique()` from the header `<algorithm>` and then remove duplicates with a call to `erase()`.

Then you can use the vector almost as if it were a `set`. The elements are sorted, which means you can read them out in the same order. Instead of using `find()` to search for elements, you now use, for example, the functions `lower_bound()` or `binary_search()` from `<algorithm>`. This is done using binary search and is therefore just as fast as `set`—probably even faster as `vector` has better locality behavior, meaning the data is stored in a more CPU-friendly manner in memory.

### Binary Search

This is a standard procedure to ensure that a desired element can be found in a sorted sequence of elements with a few steps. In this process, the middle element of the sequence is successively selected and then searched either to the right or left, depending on whether the middle element is greater or smaller than the desired element. This guarantees that the desired element is found after a maximum of log n steps or it is known that it is not in the list.

The disadvantage of this procedure is that you keep more elements in the vector during the insertion phase than in a `set`. This means that `vector` loses its speed advantage over `set` if you expect many duplicates. When exactly this happens depends on many factors. As a rule of thumb, I would recommend that using a `vector` as a `set` replacement is worthwhile if you expect more than about 1,000,000 elements and more than half of them remain unique. For fewer elements, the additional effort in implementation is hardly worthwhile, and for fewer unique elements (i.e., more duplicate cases), `set` saves memory.

### 26.2.2 Output the Contents of a Container to a Stream

This recipe is needed repeatedly: for example, for debugging or during unit tests. Of course, there are a thousand ways to output the elements of a container to a stream: from a simple loop to a ranged for loop to a specialized overload of the `operator<<`.

The most elegant way, however, is to copy the contents of the container to the stream—for this, `std::ranges::copy()` from `<algorithm>` is used, or `std::copy` before C++20. Then, all that is needed is the `ostream_iterator` from `<iterator>` as an adapter, and the output is a one-liner:

```cpp
// https://godbolt.org/z/fGKsfs1Y4
#include <iostream>   // cout
#include <algorithm>  // copy
#include <iterator>   // ostream_iterator
#include <vector>

int main() {
  std::vector<char> path{};
  for (char ch = 'a'; ch <= 'z'; ++ch) {
    path.push_back(ch);
  }
  std::ranges::copy(path, // here everything, but it also works with other ranges
    std::ostream_iterator<char>(std::cout, " ") // copy to cout, separator " "
  );
}
```

### 26.2.3 So “array” Is Not That Static

After reading the chapter on containers, you might think that `array` always has a fixed size. While this is true, you don't have to completely discard `array` if you need one more
