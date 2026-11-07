```
Array a contains:
    1 2 3 4 5 6 7 8 9 10
Array a after swapping a[0] and a[1] using swap:
    2 1 3 4 5 6 7 8 9 10
Array a after swapping a[0] and a[1] using iter_swap:
    1 2 3 4 5 6 7 8 9 10
Array a after swapping the first five elements
with the last five elements:
    6 7 8 9 10 1 2 3 4 5
```

**Fig. 16.7** | Algorithms iter_swap, swap and swap_ranges. (Part 2 of 2.)

# swap Algorithm

Line 18 uses the **swap** algorithm to exchange two values. In this example, the first and second elements of array a are exchanged. The function takes as arguments references to the two values being exchanged.

# iter_swap Algorithm

Line 24 uses function **iter_swap** to exchange the two elements. The function takes two forward iterator arguments (in this case, iterators to elements of an array) and exchanges the values in the elements to which the iterators refer.

# swap_ranges Algorithm

Line 30 uses function **swap_ranges** to exchange the elements from a.begin() up to, but not including, a.begin() + 5 with the elements beginning at position a.begin() + 5. The function requires three forward iterator arguments. The first two arguments specify the range of elements in the first sequence that will be exchanged with the elements in the second sequence starting from the iterator in the third argument. In this example, the two sequences of values are in the same array, but the sequences can be from different arrays or containers. The sequences must not overlap. The destination sequence must be large enough to contain all the elements of the ranges being swapped.

# 16.3.8 copy_backward, merge, unique and reverse

Figure 16.8 demonstrates algorithms copy_backward, merge, unique and reverse.

```
1  // Fig. 16.8: fig16_08.cpp
2  // Algorithms copy_backward, merge, unique and reverse.
3  #include <iostream>
4  #include <algorithm> // algorithm definitions
5  #include <array>     // array class-template definition
6  #include <iterator>  // ostream_iterator
7  using namespace std;
8
9  int main()
10 {
11     const size_t SIZE = 5;
12     array<int, SIZE> a = { 1, 3, 5, 7, 9 };
```

**Fig. 16.8** | Algorithms copy_backward, merge, unique and reverse. (Part 1 of 2)