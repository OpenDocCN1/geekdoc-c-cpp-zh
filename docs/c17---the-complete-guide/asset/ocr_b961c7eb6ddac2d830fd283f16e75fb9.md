Note that for accumulate(), partial_sum(), and inner_product(), new parallel algorithms are provided with relaxed requirements (which is motivated below):

+   - To run accumulate() in parallel, use reduce() or transform_reduce().
+   - To run partial_sum() in parallel, use the ...scan() algorithms.
+   - To run inner_product() in parallel, use transform_reduce().

Table STL Algorithms with Restricted Parallelization lists the algorithms that are standardized to support parallel processing with some modifications.

| Algorithms | Restriction |
|---|---|
| for_each() | Return type void and forward iterators |
| for_each_n() | Forward iterators (NEW) |
| all_of(), any_of(), none_of() | Forward iterators |
| find(), find_if(), find_if_not() | Forward iterators |
| find_first_of() | Forward iterators |
| count(), count_if() | Forward iterators |
| mismatch() | Forward iterators |
| equal() | Forward iterators |
| is_partitioned() | Forward iterators |
| partial_sort_copy() | Forward iterators |
| includes() | Forward iterators |
| lexicographical_compare() | Forward iterators |
| fill_n() | Forward iterators |
| generate_n() | Forward iterators |
| reverse_copy() | Forward iterators |
| rotate_copy() | Forward iterators |
| copy(), copy_n(), copy_if() | Forward iterators |
| move() | Forward iterators |
| transform() | Forward iterators |
| replace_copy(), replace_copy_if() | Forward iterators |
| remove_copy(), remove_copy_if() | Forward iterators |
| unique_copy() | Forward iterators |
| partition_copy() | Forward iterators |
| merge() | Forward iterators |
| set_union(), set_intersection() | Forward iterators |
| set_difference(), set_symmetric_difference() | Forward iterators |
| inclusive_scan(), exclusive_scan() | Forward iterators (NEW) |
| transform_inclusive_scan(), transform_exclusive_scan() | Forward iterators (NEW) |

Table 22.4. STL Algorithms with Restricted Parallelization