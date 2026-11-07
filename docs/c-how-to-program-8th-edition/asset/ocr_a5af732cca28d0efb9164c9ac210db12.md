| Algorithm | Description |
|---|---|
| `rotate_copy` | Identical to rotate except that the results are stored in a separate sequence indicated by the fourth argument—an output iterator. The two sequences must have the same number of elements. |
| `adjacent_find` | Returns an input iterator indicating the first of two identical adjacent elements in a sequence. If there are no identical adjacent elements, the iterator is positioned at the end of the sequence. |
| `search` | Searches for a subsequence of elements within a sequence of elements and, if such a subsequence is found, returns a forward iterator that indicates the first element of that subsequence. If there are no matches, the iterator is positioned at the end of the sequence to be searched. |
| `search_n` | Searches a sequence of elements looking for a subsequence in which the values of a specified number of elements have a particular value and, if such a sequence is found, returns a forward iterator that indicates the first element of that subsequence. If there are no matches, the iterator is positioned at the end of the sequence to be searched. |
| `partial_sort` | Use three random-access iterators to sort part of a sequence. The first and last arguments indicate the sequence of elements. The second argument indicates the ending location for the sorted part of the sequence. By default, elements are ordered using operator < (a binary predicate function can also be supplied). The elements from the second argument to the end of the sequence are in an undefined order. |
| `partial_sort_copy` | Use two input iterators and two random-access iterators to sort part of the sequence indicated by the two input iterator arguments. The results are stored in the sequence indicated by the two random-access iterator arguments. By default, elements are ordered using operator < (a binary predicate function can also be supplied). The number of elements sorted is the smaller of the number of elements in the result and the number of elements in the original sequence. |
| `stable_sort` | The algorithm is similar to sort except that all equivalent elements are maintained in their original order. This sort is O(n log n) if enough memory is available; otherwise, it’s O(n(log n)²). |

**Fig. 22.39** | Algorithms not covered in this chapter. (Part 2 of 2.)

# 22.9 Class bitset

Class `bitset` makes it easy to create and manipulate bit sets, which are useful for representing a set of bit flags. bitsets are fixed in size at compile time. Class bitset is an alternate tool for bit manipulation, discussed in Chapter 21. The declaration

```
bitset< size > b;
```

creates bitset b, in which every bit is initially 0. The statement

```
b.set( bitNumber );
```

sets bit bitNumber of bitset b “on.” The expression b.set() sets all bits in b “on.”