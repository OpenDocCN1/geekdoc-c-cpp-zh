
This function will work only with arrays, vectors and deques. A second version of this function takes as a third argument a binary predicate function for comparing values.

Line 25 uses function `sort_heap` to sort a sequence of values in the range from `v.begin()` (but not including `v.end()`) that are already arranged in a heap. The two iterator arguments must be random-access iterators. A second version of this function takes as a third argument a binary predicate function for comparing values.

Line 39 uses function `push_heap` to add a new value into a heap. We take one element of array `a` at a time, append it to the end of the vector `v2` and perform the push_heap operation. If the appended element is the only element in the vector, the vector is already a heap. Otherwise, function push_heap rearranges the vector elements into a heap. Each time push_heap is called, it assumes that the last element currently in the vector (i.e., the one that's appended before the push_heap function call) is the element being added to the heap and that all other elements in the vector are already arranged as a heap. The two iterator arguments to push_heap must be random-access iterators. A second version of this function takes as a third argument a binary predicate function for comparing values.

Line 50 uses `pop_heap` to remove the top heap element. This function assumes that the elements in the range specified by its two random-access iterator arguments are already a heap. Repeatedly removing the top heap element results in a sorted sequence of values. Function pop_heap swaps the first heap element (`v2.begin()`) with the last heap element (the element before `v2.end() - i`), then ensures that the elements up to, but not including, the last element still form a heap. Notice in the output that, after the pop_heap operations, the vector is sorted in ascending order. A second version of this function takes as a third argument a binary predicate function for comparing values.

## 22.8.13 min and max

Algorithms `min` and `max` determine the minimum and the maximum of two elements, respectively. Figure 22.38 demonstrates min and max for int and char values.

```cpp
// Fig. 22.38: Fig22_38.cpp
// Standard Library algorithms min and max.
#include <iostream>
#include <algorithm>
using namespace std;

int main()
{
   cout << "The minimum of 12 and 7 is: " << min(12, 7);
   cout << "\nThe maximum of 12 and 7 is: " << max(12, 7);
   cout << "\nThe minimum of 'G' and 'Z' is: " << min('G', 'Z');
   cout << "\nThe maximum of 'G' and 'Z' is: " << max('G', 'Z');
   cout << endl;
} // end main
```

```
The minimum of 12 and 7 is: 7
The maximum of 12 and 7 is: 12
The minimum of 'G' and 'Z' is: G
The maximum of 'G' and 'Z' is: Z
```

**Fig. 22.38** | Algorithms min and max.

## 22.8.14 STL Algorithms Not Covered in This Chapter

Figure 22.39 summarizes STL algorithms that are not covered in this chapter.

| Algorithm | Description |
|---|---|
| `inner_product` | Calculate the sum of the products of two sequences by taking corresponding elements in each sequence, multiplying those elements and adding the result to a total. |
| `adjacent_difference` | Beginning with the second element in a sequence, calculate the difference (using operator −) between the current and previous elements, and store the result. The first two input iterator arguments indicate the range of elements in the container and the third indicates where the results should be stored. A second version of this algorithm takes as a fourth argument a binary function to perform a calculation between the current element and the previous element. |
| `partial_sum` | Calculate a running total (using operator +) of the values in a sequence. The first two input iterator arguments indicate the range of elements in the container and the third indicates where the results should be stored. A second version of this algorithm takes as a fourth argument a binary function that performs a calculation between the current value in the sequence and the running total. |
| `nth_element` | Use three random-access iterators to partition a range of elements. The first and last arguments represent the range of elements. The second argument is the partitioning element’s location. After this algorithm executes, all elements before the partitioning element are less than that element and all elements after the partitioning element are greater than or equal to that element. A second version of this algorithm takes as a fourth argument a binary comparison function. |
| `partition` | Similar to nth_element, but requires less powerful bidirectional iterators, making it more flexible. It requires two bidirectional iterators indicating the range of elements to partition. The third argument is a unary predicate function that helps partition the elements so that all elements for which the predicate is true are to the left (toward the beginning of the sequence) of those for which the predicate is false. A bidirectional iterator is returned indicating the first element in the sequence for which the predicate returns false. |
| `stable_partition` | Similar to partition except that this algorithm guarantees that equivalent elements will be maintained in their original order. |
| `next_permutation` | Next lexicographical permutation of a sequence. |
| `prev_permutation` | Previous lexicographical permutation of a sequence. |
| `rotate` | Use three forward iterator arguments to rotate the sequence indicated by the first and last argument by the number of positions indicated by subtracting the first argument from the second argument. For example, the sequence 1, 2, 3, 4, 5 rotated by two positions would be 4, 5, 1, 2, 3. |
| `rotate_copy` | Identical to rotate except that the results are stored in a separate sequence indicated by the fourth argument—an output iterator. The two sequences must have the same number of elements. |
| `adjacent_find` | Returns an input iterator indicating the first of two identical adjacent elements in a sequence. If there are no identical adjacent elements, the iterator is positioned at the end of the sequence. |
| `search` | Searches for a subsequence of elements within a sequence of elements and, if such a subsequence is found, returns a forward iterator that indicates the first element of that subsequence. If there are no matches, the iterator is positioned at the end of the sequence to be searched. |
| `search_n` | Searches a sequence of elements looking for a subsequence in which the values of a specified number of elements have a particular value and, if such a sequence is found, returns a forward iterator that indicates the first element of that subsequence. If there are no matches, the iterator is positioned at the end of the sequence to be searched. |
| `partial_sort` | Use three random-access iterators to sort part of a sequence. The first and last arguments indicate the sequence of elements. The second argument indicates the ending location for the sorted part of the sequence. By default, elements are ordered using operator < (a binary predicate function can also be supplied). The elements from the second argument to the end of the sequence are in an undefined order. |
| `partial_sort_copy` | Use two input iterators and two random-access iterators to sort part of the sequence indicated by the two input iterator arguments. The results are stored in the sequence indicated by the two random-access iterator arguments. By default, elements are ordered using operator < (a binary predicate function can also be supplied). The number of elements sorted is the smaller of the number of elements in the result and the number of elements in the original sequence. |
| `stable_sort` | The algorithm is similar to sort except that all equivalent elements are maintained in their original order. This sort is O(n log n) if enough memory is available; otherwise, it’s O(n(log n)²). |

**Fig. 22.39** | Algorithms not covered in this chapter. (Part 1 of 2.)
**Fig. 22.39** | Algorithms not covered in this chapter. (Part 2 of 2.)

## 22.9 Class bitset

Class `bitset` makes it easy to create and manipulate bit sets, which are useful for representing a set of bit flags. bitsets are fixed in size at compile time. Class bitset is an alternate tool for bit manipulation, discussed in Chapter 21. The declaration

```cpp
bitset< size > b;
```

creates bitset b, in which every bit is initially 0. The statement

```cpp
b.set( bitNumber );
```

sets bit bitNumber of bitset b “on.” The expression b.set() sets all bits in b “on.”
