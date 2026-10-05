Applies a unary function to the first $n$ elements of a range.

+   * find
Usage: constant; iterators: in
Finds by a sample value.

+   * find_if
Usage: constant; iterators: in
Finds by a predicate, see Listing 25.9.

+   * find_if_not
Usage: frequent; iterators: in
Finds by the negation of a predicate.

+   * find_end
Usage: rare; iterators: fw
Finds the end of a matching subsequence.

+   * find_first_of
Usage: frequent; iterators: in/fw
Finds one of several sample values.

+   * ranges::find_last, find_last_if, find_last_if_not
Usage: occasional (C+23); iterators: in/fw
Finds the last element or the element matching the predicate.

+   * adjacent_find
Usage: occasional; iterators: fw
Finds the first position where two adjacent elements both satisfy a predicate.

+   * count
Usage: constant; iterators: in
Counts the number of occurrences of a sample value.