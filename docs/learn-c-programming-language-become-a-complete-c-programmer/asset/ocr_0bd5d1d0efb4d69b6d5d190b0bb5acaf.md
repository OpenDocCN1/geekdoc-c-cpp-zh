`priority_queue` is almost certainly implemented using a `heap` (§32.6.4).

# 31.6 Advice

+   [1] An STL container defines a sequence; §31.2.  
+   [2] Use `vector` as your default container; §31.2, §31.4.  
+   [3] Insertion operators, such as `insert()` and `push_back()` are often more efficient on a `vector` than on a `list`; §31.2, §31.4.1.1.  
+   [4] Use `forward_list` for sequences that are usually empty; §31.2, §31.4.2.  
+   [5] When it comes to performance, don’t trust your intuition: measure; §31.3.  
+   [6] Don’t blindly trust asymptotic complexity measures; some sequences are short and the cost of individual operations can vary dramatically; §31.3.  
+   [7] STL containers are resource handles; §31.2.1.  
+   [8] A `map` is usually implemented as a red-black tree; §31.2.1, §31.4.3.  
+   [9] An `unordered_map` is a hash table; §31.2.1, §31.4.3.2.  
+   [10] To be an element type for a STL container, a type must provide copy or move operations; §31.2.2.  
+   [11] Use containers of pointers or smart pointers when you need to preserve polymorphic behavior; §31.2.2.  
+   [12] Comparison operations should implement a strict weak order; §31.2.2.1.  
+   [13] Pass a container by reference and return a container by value; §31.3.2.  
+   [14] For a container, use the `()`-initializer syntax for sizes and the `{}`-initializer syntax for lists of elements; §31.3.2.  
+   [15] For simple traversals of a container, use a `rangefor` loop or a begin/end pair of iterators; §31.3.4.  
+   [16] Use `const` iterators where you don’t need to modify the elements of a container; §31.3.4.  
+   [17] Use `auto` to avoid verbosity and typos when you use iterators; §31.3.4.  
+   [18] Use `reserve()` to avoid invalidating pointers and iterators to elements; §31.3.3, §31.4.1.  
+   [19] Don’t assume performance benefits from `reserve()` without measurement; §31.3.3.  
+   [20] Use `push_back()` or `resize()` on a container rather than `realloc()` on an array; §31.3.3, §31.4.1.1.  
+   [21] Don’t use iterators into a resized `vector` or `deque`; §31.3.3.  
+   [22] When necessary, use `reserve()` to make performance predictable; §31.3.3.  
+   [23] Do not assume that `[]` range checks; §31.2.2.  
+   [24] Use `at()` when you need guaranteed range checks; §31.2.2.  
+   [25] Use `emplace()` for notational convenience; §31.3.7.

Section 31.6 Advice 925

+   [26] Prefer compact and contiguous data structures; §31.4.1.2.  
+   [27] Use `emplace()` to avoid having to pre-initialize elements; §31.4.1.3.  
+   [28] A `list` is relatively expensive to traverse; §31.4.2.