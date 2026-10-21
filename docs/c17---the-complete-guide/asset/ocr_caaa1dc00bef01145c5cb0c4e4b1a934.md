# 22.5 Overview of Parallel Algorithms

Table *STL Algorithms with Unrestricted Parallelization* lists the algorithms that are standardized to support parallel processing without any modification.

Table *STL Algorithms Without Parallelization* lists the algorithms that do not support parallel processing.

| Algorithms with Unrestricted Parallelization |
|---| 
| `find_end(), adjacent_find()` |
| `search(), search_n()` except with "searcher" |
| `swap_ranges()` |
| `replace(), replace_if()` |
| `fill()` |
| `generate()` |
| `remove(), remove_if(), unique()` |
| `reverse(), rotate()` |
| `partition(), stable_partition()` |
| `sort(), stable_sort(), partial_sort()` |
| `is_sorted(), is_sorted_until()` |
| `nth_element()` |
| `inplace_merge()` |
| `is_heap(), is_heap_until()` |
| `min_element(), max_element(), min_max_element()` |

*Table 22.2. STL Algorithms with Unrestricted Parallelization*

| Algorithms Without Parallelization |
|---| 
| `accumulate()` |
| `partial_sum()` |
| `inner_product()` |
| `search()` with "searcher" |
| `copy_backward(), move_backward()` |
| `sample(), shuffle()` |
| `partition_point()` |
| `lower_bound(), upper_bound(), equal_range()` |
| `binary_search()` |
| `is_permutation(),` |
| `next_permutation(), prev_permutation()` |
| `push_heap(), pop_heap(), make_heap(), sort_heap()` |

*Table 22.3. STL Algorithms Without Parallelization*