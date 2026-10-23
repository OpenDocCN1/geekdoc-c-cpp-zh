| 28 | 17 | 40 | 99 | 27 | 22 | 96 | 98 |

Total number of elements are 8

Divide them in two series, each of 08/2=4 elements

(28, 17, 40, 99)   (27, 22, 96, 98)

Total number of elements are 4

Divide them in two series, each of 4/2=2 elements

(28, 17) (40, 99)   (27, 22) (96, 98)

Figure 10-6: Divide and conquer in quick sort

Program to depict the merge sort has been given as follows.

```
// Program to sort the array using mergesort
void mergesort (int ar [], int lower, int upper)
{
int mid;
if (upper > lower)
{
mid= (lower+upper)/2;
mergesort (ar, lower, mid);   // divide the series into two (left side)
mergesort (ar, mid+1, upper); // divide the series into two (right side)
merge (ar, lower, mid, mid+1, upper); // merge the half
}      // end of if
}      // end of function
```

# F. Heap sort

Heap is a data structure that is widely utilized in priority queue. Heap is defined as follows:

+   - A large dynamic area of memory that can be utilized by the programmer and same may be de-allocated when not needed.
+   - A balanced, left justified binary tree in which no node has a value greater than the value in its parents.

Heap sorts follow the second definition. Quick sort proved to be immensely effective in sorting algorithm. Same is apparent with the performance that yield performance of O (n log