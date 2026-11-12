

// 合并已排序的两半 theArray[first..mid] 和 theArray[mid+1..last]
merge(theArray, first, mid, last)
}
// 如果 first > last，则无需执行任何操作

显然，归并排序算法中大部分工作都在合并步骤，但该算法真的能排序吗？递归调用会继续将数组分成小片，直到每个片只包含一个元素；显然，只有一个元素的数组是已排序的。然后，算法将这些小片合并成更大的已排序片，直到得到一个已排序的数组。图 11-6 说明了对六个整数组成的数组进行归并排序时的递归调用和合并步骤。

清单 11-4 中的 C++ 函数实现了归并排序算法。要对 n 个元素的数组进行排序，可以通过编写以下内容调用函数 mergeSort：

```
mergeSort(theArray, 0, n - 1);
```

### 图 11-6 对六个整数组成的数组进行归并排序

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_341_0.png)

### 清单 11-4 归并排序的实现

```
const int MAX_SIZE = maximum-number-of-items-in-array;
/* Merges two sorted array segments theArray[first..mid] and
theArray[mid+1..last] into one sorted array.
@pre first <= mid <= last. The subarrays theArray[first..mid] and
theArray[mid+1..last] are sorted in increasing order.
@post theArray[first..last] is sorted.
@param theArray The given array.
@param first The index of the beginning of the first segment in
theArray.
@param mid The index of the end of the first segment in theArray;
mid + 1 marks the beginning of the second segment.
@param last The index of the last element in the second segment in
theArray.
(continues)
@note This function merges the two subarrays into a temporary
array and copies the result into the original array. */
void merge(ItemType theArray[], int first, int mid, int last)
{
   ItemType tempArray[MAX_SIZE]; // Temporary array
   // Initialize the local indices to indicate the subarrays
   int first1 = first; // Beginning of first subarray
   int last1 = mid; // End of first subarray
   int first2 = mid + 1; // Beginning of second subarray
   int last2 = last; // End of second subarray
   // While both subarrays are not empty, copy the
   // smaller item into the temporary array
   int index = first1; // Next available location in tempArray
   while ((first1 <= last1) && (first2 <= last2))
   {
      // At this point, tempArray[first1..index-1] is in order
      if (theArray[first1] < theArray[first2])
      {
         tempArray[index] = theArray[first1];
         first1++;
      }
      else
      {
         tempArray[index] = theArray[first2];
         first2++;
      } // end if
      index++;
   } // end while
   // Finish off the first subarray, if necessary
   while (first1 <= last1)
   {
      // At this point, tempArray[first1..index-1] is in order
      tempArray[index] = theArray[first1];
      first1++;
      index++;
   } // end while
   // Finish off the second subarray, if necessary
   while (first2 <= last2)
   {
      // At this point, tempArray[first1..index-1] is in order
      tempArray[index] = theArray[first2];
      first2++;
      index++;
   } // end while
   // Copy the result back into the original array
   for (index = first; index <= last; index++)
      theArray[index] = tempArray[index];
   // end merge
}

/** Sorts the items in an array into ascending order.
@pre theArray[first..last] is an array.
@post theArray[first..last] is sorted in ascending order.
@param theArray The given array.
@param first The index of the first element to consider in theArray.
@param last The index of the last element to consider in theArray.*/
void mergeSort(ItemType theArray[], int first, int last)
{
   if (first < last)
   {
      // Sort each half
      int mid = first + (last - first) / 2; // Index of midpoint

      // Sort left half theArray[first..mid]
      mergeSort(theArray, first, mid);

      // Sort right half theArray[mid+1..last]
      mergeSort(theArray, mid + 1, last);

      // Merge the two halves
      merge(theArray, first, mid, last);
   } // end if

} // end mergeSort
```

- 题目 7 通过绘制类似图 11-6 所示的图表，跟踪归并排序对以下数组进行升序排序的过程：25 30 20 80 40 60。

- 题目 8 证明归并排序算法满足第 2 章中描述的递归的四个标准。

### 分析

由于算法的合并步骤需要付出最多努力，让我们从这里开始分析。每个合并步骤都会合并 theArray[first...mid] 和 theArray[mid+1...last]。图 11-7 提供了一个需要最大比较次数的合并步骤示例。如果要合并的两个数组段中的元素总数为 n，那么合并这些段最多需要 n-1 次比较。（例如，在图 11-7 中，段中有六个元素，需要五次比较

### 图 11-7 归并排序中合并步骤的最坏情况实例

合并两半：
- a. 1 < 4，因此将 1 从 theArray[first...mid] 移动到 tempArray
- b. 2 < 4，因此将 2 从 theArray[first...mid] 移动到 tempArray
- c. 8 > 4，因此将 4 从 theArray[mid+1...last] 移动到 tempArray
- d. 8 > 5，因此将 5 从 theArray[mid+1...last] 移动到 tempArray
- e. 8 > 6，因此将 6 从 theArray[mid+1...last] 移动到 tempArray
- f. theArray[mid+1...last] 已处理完毕，因此将 8 移动到 tempArray

### 图 11-8 对八个元素组成的数组进行 mergeSort 的递归调用层次

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_344_0.png)

）。此外，从原始数组到临时数组有 n 次移动，从临时数组回到原始数组也有 n 次移动。因此，每个合并步骤需要 3 × n − 1 次主要操作。

每次对 mergeSort 的调用都会递归地调用自身两次。如图 11-8 所示，如果原始对 mergeSort 的调用位于第 0 层，那么递归第 1 层会发生两次对 mergeSort 的调用。这些调用中的每一个随后又会调用 mergeSort 两次，因此递归第 2 层会发生四次对 mergeSort 的调用，以此类推。递归有多少层？我们可以按如下方式计数。

每次对 mergeSort 的调用都将数组减半。第一次减半会产生两个片段。接下来的递归调用会将这两个片段各自减半，从而产生原始数组的四个片段；接下来的递归调用会将这四个片段各自减半，从而产生八个片段，以此类推。递归调用会继续进行，直到数组片段中每个都只包含一个元素——也就是说，直到共有 n 个片段，其中 n 是原始数组中的元素数量。如果 n 是 2 的幂（n = 2^k），则递归深度为 k = log2 n 层。例如，在图 11-8 中，mergeSort 有三层递归调用，因为原始数组包含八个元素，且 8 = 2^3。如果 n 不是 2 的幂，则 mergeSort 有 1 + log2 n（向下取整）层递归调用。

第 0 层的原始 mergeSort 调用会调用 merge 一次。然后 merge 会合并所有 n 个元素，并需要 3 × n − 1 次操作，如前面所示。在递归第 1 层，会发生两次对 mergeSort 的调用，因此也会发生两次对 merge 的调用。这两次 merge 调用中的每一次都会合并 n / 2 个元素，并需要 3 × (n / 2) − 1 次操作。这两次 merge 调用一共需要 2 × (3 × (n / 2) − 1) 或 3 × n − 2 次操作。在递归第 m 层，会发生 2^m 次对 merge 的调用；这些调用中的每一次都会合并 n / 2^m 个元素，因此需要 3 × (n / 2^m) − 1 次操作。这 2^m 次 merge 调用一共需要 3 × n − 2^m 次操作。因此，递归的每一层都需要 O(n) 次操作。因为递归层数要么是 log2 n，要么是 1 + log2 n，所以归并排序在最坏情况和平均情况下都是 O(n × log n)。你应该查看上一章中的图 10-3，以确信 O(n × log n) 比 O(n^2) 快得多。

> 归并排序是 O(n * log n)

尽管归并排序在时间方面是一种极其高效的算法，但它确实有一个缺点：合并步骤需要一个辅助数组。这种额外存储以及必要的元素复制都是缺点。

## 11.2.2 快速排序

> 另一种分治算法

考虑伪代码函数 kSmall 的前两个步骤，该函数用于解决查找数组 theArray[first..last] 中第 k 小元素的问题，并在第 2 章的 2.4.4 节中讨论过：

