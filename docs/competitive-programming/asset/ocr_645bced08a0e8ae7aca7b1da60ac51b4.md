![](bbox=[0.326, 0.061, 0.683, 0.178])

Figure 2.1: Examples of BST (Left) and Heap (Right)

Heap is useful to model Priority Queue, where item with highest priority can be deleted in O(log n) and new item can be inserted into priority queue also in O(log n). The implementation of `priority_queue` is available in C++ STL `<queue>`. Priority Queue is an important component in algorithms like Kruskal's for Minimum Spanning Tree (MST) problem (Section 4.4) and Dijkstra's for Single-Source Shortest Paths (SSSP) problem (Section 4.5).

This data structure is also used to perform `partial_sort` in C++ STL `<algorithm>`. This is done by taking the max element k times (k is the number of the top most items to be sorted). As each delete-max is in O(log n), `partial_sort` has O(k log n) time complexity.

+   - Hash Table: no native C++ STL support (Java HashMap/HashSet/HashTable)
+   
+     Hash Table is another form of non-linear data structures, but we do not recommend using it in contests unless necessary. Reasons: designing a good performing hash function is quite tricky and there is no native C++ STL support for it. Moreover C++ STL `<map>` or `<set>` are usually good enough as the typical input size of programming contest problems is ≤ 1M, making O(1) for Hash Table and O(log 1M) for balanced BST actually do not differ by much.
+   
+     However, a form of Hash Table is actually used in contests, namely 'Direct Addressing Table' (DAT), where the key itself determines the index, bypassing the need of 'hash function'. For example, UVa 11340 - Newspaper, where all possible ASCII characters [0-255] are assigned to certain monetary values, e.g. 'a' → '3', 'W' → '10', ..., 'I' → '13'.

Programming exercises to practice using basic data structures and algorithms (with libraries):

+   - Static array, C++ STL `<vector>`, `<bitset>`, Direct Addressing Table
+     1. UVa 482 - Permutation Arrays (simple array manipulation)
+     2. UVa 594 - One Two Three Little Endian (manipulate bit string easily with `<bitset>`)
+     3. UVa 11340 - Newspaper (Direct Addressing Table)
+   - C++ STL `<algorithm>`
+     1. UVa 146 - ID Codes (use `next_permutation`)
+     2. UVa 10194 - Football a.k.a. Soccer (multi-fields sorting, use `sort`)
+     3. UVa 10258 - Contest Scoreboard (multi-fields sorting, use `sort`)
+   - Sorting-related problems
+     1. UVa 299 - Train Swapping (inversion index^4 problem solvable with bubble sort)
+     2. UVa 612 - DNA Sorting (inversion index + `stable_sort`)
+     3. UVa 10810 - Ultra Quicksort (inversion index - requires O(n log n) merge sort)

^4 Inversion index problem: count how many swaps are needed to make the list sorted.