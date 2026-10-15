predicate function indicating the order in which the elements were originally sorted. The two sequences must be sorted using the same comparison function.

Line 66 uses function set_union to create a set of all the elements that are in either or both of the two sorted sets (both sets of values must be in ascending order). The elements are copied from both sets into the fifth argument (in this case the array unionSet). Elements that appear in both sets are only copied from the first set. The first two iterator arguments must be at least input iterators for the first set of values. The next two iterator arguments must be at least input iterators for the second set of values. The fifth argument must be at least an output iterator indicating where to store the copied elements. The function returns an output iterator positioned immediately after the last value copied into the set to which the fifth argument points. A second version of set_union takes a sixth argument that is a binary predicate function indicating the order in which the elements were originally sorted. The two sequences must be sorted using the same comparison function.

# 20.5.11 lower_bound, upper_bound and equal_range

Figure 20.36 demonstrates functions lower_bound, upper_bound and equal_range. Line 24 uses function lower_bound to find the first location in a sorted sequence of values at which the third argument could be inserted in the sequence such that the sequence would still be sorted in ascending order. The first two iterator arguments must be at least forward iterators. The third argument is the value for which to determine the lower bound. The function returns a forward iterator pointing to the position at which the insert can occur. A second version of function lower_bound takes as a fourth argument a binary predicate function indicating the order in which the elements were originally sorted.

Line 30 uses function upper_bound to find the last location in a sorted sequence of values at which the third argument could be inserted in the sequence such that the sequence would still be sorted in ascending order. The first two iterator arguments must be at least forward iterators. The third argument is the value for which to determine the upper bound. The function returns a forward iterator pointing to the position at which the insert can occur. A second version of upper_bound takes as a fourth argument a binary predicate function indicating the order in which the elements were originally sorted.

```
1  // Fig. 20.36: fig20_36.cpp
2  // Standard Library functions lower_bound, upper_bound and
3  // equal_range for a sorted sequence of values.
4  #include <iostream>
5  using std::cout;
6  using std::endl;
7
8  #include <algorithm> // algorithm definitions
9  #include <vector> // vector class-template definition
10 #include <iterator> // ostream_iterator
11
12 int main()
13 {
14     const int SIZE = 10;
15     int a1[ SIZE ] = { 2, 2, 4, 4, 4, 6, 6, 6, 6, 8 };
```