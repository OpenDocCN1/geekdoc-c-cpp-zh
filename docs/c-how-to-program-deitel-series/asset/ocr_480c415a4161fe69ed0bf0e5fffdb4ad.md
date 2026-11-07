| Sorting and related algorithms from header `<algorithm>` |  |  |  |
|---|---|---|---|
| `inplace_merge` | `includes` | `set_union` | `set_intersection` |
| `set_difference` | `set_symmetric_difference` | `push_heap` |  |
| `pop_heap` | `make_heap` | `sort_heap` | `is_heap` |
| `is_heap_until` | `min` | `max` | `minmax` |
| `min_element` | `max_element` | `minmax_element*` | `lexicographical_compare` |
| `next_permutation` | `prev_permutation` |  |  |

**Fig. 16.19** | Sorting and related algorithms from header `<algorithm>`. (Part 2 of 2.)

# Numerical Algorithms

Figure 16.20 shows the numerical algorithms of the header `<numeric>`.

| Numerical algorithms from header `<numeric>` |  |  |
|---|---|---|
| `accumulate` | `partial_sum` | `iota*` |
| `inner_product` | `adjacent_difference` |  |

**Fig. 16.20** | Numerical algorithms from header `<numeric>`.

# 16.7 Wrap-Up

In this chapter, we demonstrated many of the Standard Library algorithms, including mathematical algorithms, basic searching and sorting algorithms and set operations. You learned the types of iterators each algorithm requires and that each algorithm can be used with any container that supports the minimum iterator functionality the algorithm requires. We introduced function objects that work syntactically and semantically like ordinary functions, but offer advantages such as performance and the ability to store data. Finally, you used lambda expressions to create function objects inline then passed them to Standard Library algorithms.

We introduced exception handling earlier in the book in our discussion of arrays. In the next chapter, we take a deeper look at C++’s rich set of exception handling capabilities.

# Summary

+   *Section 16.1 Introduction*
+   - Standard Library algorithms are functions that perform such common data manipulations as searching, sorting and comparing elements or entire containers.
+   
+   *Section 16.3.1 fill, fill_n, generate and generate_n*
+   - Algorithms fill and fill_n (p. 693) set every element in a range of container elements to a specific value.