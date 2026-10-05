better in this regard and works excellently with the algorithms for sorting and binary searching. The flat ... adapters around a vector are a compromise, but the best approach is to first collect the data, then sort:

+   * sort
Usage: constant; iterators: ra
Sorts the elements in the range; see for example
Listing 25.2.

+   * stable_sort
Usage: frequent; iterators: ra
Like sort, but ensures that equal elements retain their relative order.

+   * partial_sort
Usage: occasional; iterators: ra
Like partition, uses the comparison with the middle element as the predicate.

+   * partial_sort_copy
Usage: occasional; iterators: in/ra
Like partial_sort, but copies the result into a target range.

+   * is_sorted
Usage: frequent; iterators: fw
Checks if a range is sorted.

+   * is_sorted_until
Usage: occasional; iterators: fw
Finds the first element in a range that breaks the sorting.

+   * nth_element
Usage: occasional; iterators: ra