# ISO/IEC 14882:2017(E)

one-dimensional. The set of one-dimensional index values specified by a galice are

```
k = s + \sum_{j} i_{ij}d_j
```

where the multidimensional indices $i_j$ range value from 0 to $l_{ij} - 1$.

+   [ Example: The galice specification
start = 3
length = (2, 4, 3)
stride = (19, 4, 1)
yields the sequence of one-dimensional indices

```
k = 3 + (0, 1) \times 19 + (0, 1, 2) \times 4 + (0, 1, 2) \times 1
```

which are ordered as shown in the following table:

| i_0, i_1, i_2, k |
| (0, 0, 0, 3) |
| (0, 0, 1, 4) |
| (0, 0, 2, 5) |
| (0, 1, 0, 7) |
| (0, 1, 1, 8) |
| (0, 1, 2, 9) |
| (0, 2, 0, 11) |
| (0, 2, 1, 12) |
| (0, 2, 2, 13) |
| (0, 3, 0, 15) |
| (0, 3, 1, 16) |
| (0, 3, 2, 17) |
| (1, 0, 0, 22) |
| (1, 0, 1, 23) |
| (1, 3, 2, 36) |

That is, the highest-ordered index slices turn fastest. — end example— is repeated.

+   [ Example: If the stride parameters in the previous example are changed to {1, 1, 1}, the first few elements of the resulting sequence of indices will be

| (0, 0, 0, 3) |
| (0, 0, 1, 4) |
| (0, 0, 2, 5) |
| (0, 1, 0, 4) |
| (0, 1, 1, 5) |
| (0, 1, 2, 6) |

end example—

+   If a degenerate slice is used as the argument to the non-const version of operator[] (const gslice&), the behavior is undefined.