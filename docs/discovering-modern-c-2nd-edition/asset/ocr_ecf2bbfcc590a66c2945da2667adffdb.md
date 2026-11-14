```
float sum_w= accumulate(begin(w), end(w), 0.0f),
product_w= accumulate(begin(w), end(w), 1.0f,
[] (float x, float y){return x *
y});
```

The function iota was not part of C++03 but is integrated in the standard since C++11.

# 4.1.4.5 Complexity

Bjarne Stroustrup summarized the complexities of all STL algorithms in a concise table (Table 4–1) that he graciously allowed us to share.

# Table 4–1: Complexity of STL Algorithms

| Complexity | Algorithms |
| :--- | :--- |
| O(1) | swap, iter_swap |
| O(log n) | lower_bound, upper_bound, equal_range, binary_search, push_heap, pop_heap |
| O(n log n) | inplace_merge, stable_partition, all sorting algorithms |
| O(n2) | find_end, find_first_of, search, search_n |
| O(n) | All other algorithms |

From [62, page 931]

# 4.1.5 Ranges

# 4.1.5.1 Risks and Limitations of Iterators

C++20 Iterators undoubtedly made an important contribution to modern programming in C++. Nonetheless, they can be quite dangerous and lead to inelegant interfaces. Let's start with the dangers. Iterators often appear in pairs and only the programmer can assure that the two iterators really relate to each other. This offers us an unattractive repertoire of mistakes:

+   • The end iterator comes first.