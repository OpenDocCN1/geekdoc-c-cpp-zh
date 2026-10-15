
Line 66 uses function `set_union` to create a set of all the elements that are in either or both of the two sorted sets (both sets of values must be in ascending order). The elements are copied from both sets into the fifth argument (in this case the array `unionSet`). Elements that appear in both sets are only copied from the first set. The first two iterator arguments must be at least input iterators for the first set of values. The next two iterator arguments must be at least input iterators for the second set of values. The fifth argument must be at least an output iterator indicating where to store the copied elements. The function returns an output iterator positioned immediately after the last value copied into the set to which the fifth argument points. A second version of `set_union` takes a sixth argument that is a binary predicate function indicating the order in which the elements were originally sorted. The two sequences must be sorted using the same comparison function.

## 20.5.11 `lower_bound`, `upper_bound` and `equal_range`

Figure 20.36 demonstrates functions `lower_bound`, `upper_bound` and `equal_range`. Line 24 uses function `lower_bound` to find the first location in a sorted sequence of values at which the third argument could be inserted in the sequence such that the sequence would still be sorted in ascending order. The first two iterator arguments must be at least forward iterators. The third argument is the value for which to determine the lower bound. The function returns a forward iterator pointing to the position at which the insert can occur. A second version of function `lower_bound` takes as a fourth argument a binary predicate function indicating the order in which the elements were originally sorted.

Line 30 uses function `upper_bound` to find the last location in a sorted sequence of values at which the third argument could be inserted in the sequence such that the sequence would still be sorted in ascending order. The first two iterator arguments must be at least forward iterators. The third argument is the value for which to determine the upper bound. The function returns a forward iterator pointing to the position at which the insert can occur. A second version of `upper_bound` takes as a fourth argument a binary predicate function indicating the order in which the elements were originally sorted.

```cpp
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
16     std::vector< int > v( a1, a1 + SIZE ); // copy of a1
17     std::ostream_iterator< int > output( cout, " " );
18
19     cout << "Vector v contains:\n";
20     std::copy( v.begin(), v.end(), output );
21
22     // determine lower-bound insertion point for 6 in v
23     std::vector< int >::iterator lower;
24     lower = std::lower_bound( v.begin(), v.end(), 6 );
25     cout << "\n\nLower bound of 6 is element "
26         << ( lower - v.begin() ) << " of vector v";
27
28     // determine upper-bound insertion point for 6 in v
29     std::vector< int >::iterator upper;
30     upper = std::upper_bound( v.begin(), v.end(), 6 );
31     cout << "\nUpper bound of 6 is element "
32         << ( upper - v.begin() ) << " of vector v";
33
34     // use equal_range to determine both the lower- and
35     // upper-bound insertion points for 6
36     std::pair< std::vector< int >::iterator,
37              std::vector< int >::iterator > eq;
38     eq = std::equal_range( v.begin(), v.end(), 6 );
39     cout << "\nUsing equal_range:\n  Lower bound of 6 is element "
40         << ( eq.first - v.begin() ) << " of vector v";
41     cout << "\n  Upper bound of 6 is element "
42         << ( eq.second - v.begin() ) << " of vector v";
43     cout << "\n\nUse lower_bound to locate the first point\n"
44         << "at which 5 can be inserted in order";
45
46     // determine lower-bound insertion point for 5 in v
47     lower = std::lower_bound( v.begin(), v.end(), 5 );
48     cout << "\n  Lower bound of 5 is element "
49         << ( lower - v.begin() ) << " of vector v";
50     cout << "\n\nUse upper_bound to locate the last point\n"
51         << "at which 7 can be inserted in order";
52
53     // determine upper-bound insertion point for 7 in v
54     upper = std::upper_bound( v.begin(), v.end(), 7 );
55     cout << "\n  Upper bound of 7 is element "
56         << ( upper - v.begin() ) << " of vector v";
57     cout << "\n\nUse equal_range to locate the first and\n"
58         << "last point at which 5 can be inserted in order";
59
60     // use equal_range to determine both the lower- and
61     // upper-bound insertion points for 5
62     eq = std::equal_range( v.begin(), v.end(), 5 );
63     cout << "\n  Lower bound of 5 is element "
64         << ( eq.first - v.begin() ) << " of vector v";
65     cout << "\n  Upper bound of 5 is element "
66         << ( eq.second - v.begin() ) << " of vector v" << endl;
67     return 0;
68 } // end main
```

```text
Vector v contains:
2 2 4 4 4 6 6 6 6 8

Lower bound of 6 is element 5 of vector v
Upper bound of 6 is element 9 of vector v
Using equal_range:
    Lower bound of 6 is element 5 of vector v
    Upper bound of 6 is element 9 of vector v

Use lower_bound to locate the first point
at which 5 can be inserted in order
    Lower bound of 5 is element 5 of vector v

Use upper_bound to locate the last point
at which 7 can be inserted in order
    Upper bound of 7 is element 9 of vector v

Use equal_range to locate the first and
last point at which 5 can be inserted in order
    Lower bound of 5 is element 5 of vector v
    Upper bound of 5 is element 5 of vector v
```

Fig. 20.36 | Algorithms `lower_bound`, `upper_bound` and `equal_range`.

Line 38 uses function `equal_range` to return a pair of forward iterators containing the combined results of performing both a `lower_bound` and an `upper_bound` operation. The first two iterator arguments must be at least forward iterators. The third argument is the value for which to locate the equal range. The function returns a pair of forward iterators for the lower bound (`eq.first`) and upper bound (`eq.second`), respectively.

Functions `lower_bound`, `upper_bound` and `equal_range` are often used to locate insertion points in sorted sequences. Line 47 uses `lower_bound` to locate the first point at which 5 can be inserted in order in `v`. Line 54 uses `upper_bound` to locate the last point at which 7 can be inserted in order in `v`. Line 62 uses `equal_range` to locate the first and last points at which 5 can be inserted in order in `v`.

## 20.5.12 Heapsort

Figure 20.37 demonstrates the Standard Library functions for performing the heapsort sorting algorithm. Heapsort is a sorting algorithm in which an array of elements is arranged into a special binary tree called a heap. The key features of a heap are that the largest element is always at the top of the heap and the values of the children of any node in the binary tree are always less than or equal to that node’s value. A heap arranged in this manner is often called a max heap.
