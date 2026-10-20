
```java
68     if ( data[ leftIndex ] <= data[ rightIndex ] )
69         combined[ combinedIndex++ ] = data[ leftIndex++ ];
70     else
71         combined[ combinedIndex++ ] = data[ rightIndex++ ];
72 } // end while

73
74 // if left array is empty
75 if ( leftIndex == middle2 )
76     // copy in rest of right array
77     while ( rightIndex <= right )
78         combined[ combinedIndex++ ] = data[ rightIndex++ ];
79 else // right array is empty
80     // copy in rest of left array
81     while ( leftIndex <= middle1 )
82         combined[ combinedIndex++ ] = data[ leftIndex++ ];

84 // copy values back into original array
85 for ( int i = left; i <= right; i++ )
86     data[ i ] = combined[ i ];

88 // output merged array
89 System.out.println( "      " + subarray( left, right ) );
90 System.out.println();
91 } // end method merge
92
93 // method to output certain values in array
94 public String subarray( int low, int high )
95 {
96     StringBuilder temporary = new StringBuilder();
97
98     // output spaces for alignment
99     for ( int i = 0; i < low; i++ )
100         temporary.append( "   " );
101
102     // output elements left in array
103     for ( int i = low; i <= high; i++ )
104         temporary.append( "   " + data[ i ] );
105
106     return temporary.toString();
107 } // end method subarray
108
109 // method to output values in array
110 public String toString()
111 {
112     return subarray( 0, data.length - 1 );
113 } // end method toString
114 } // end class MergeSort
```

图 19.10 | 创建一个填充随机整数的数组的类。提供一个方法使用归并排序对数组进行排序。 （第 3 部分，共 3 部分。）

merge 方法中的第 64–72 行循环直到程序到达任一子数组的末尾。第 68 行测试两个数组开头元素的大小。如果左数组中的元素较小，则第 69 行将其放置在 combined 数组中的位置。如果右数组中的元素较小，则第 71 行将其放置在 combined 数组中的位置。当 while 循环完成时（第 72 行），整个子数组已被放置在 combined 数组中，但另一个子数组仍包含数据。第 75 行测试左数组是否已到达末尾。如果是，则第 77–78 行用右数组的元素填充 combined 数组。如果左数组未到达末尾，则右数组必须已到达末尾，第 81–82 行用左数组的元素填充 combined 数组。最后，第 85–86 行将 combined 数组复制回原始数组。图 19.11 创建并使用 MergeSort 对象。此程序的输出显示了归并排序执行的拆分和合并，展示了算法在每一步的排序进度。花时间逐步分析这些输出以完全理解这种优雅的排序算法是值得的。

```java
// Fig. 19.11: MergeSortTest.java
// Testing the merge sort class.
public class MergeSortTest
{
    public static void main( String[] args )
    {
        // create object to perform merge sort
        MergeSort sortArray = new MergeSort( 10 );

        // print unsorted array
        System.out.println( "Unsorted:" + sortArray + "\n" );

        sortArray.sort(); // sort array

        // print sorted array
        System.out.println( "Sorted:  " + sortArray );
    } // end main
} // end class MergeSortTest
```

```
Unsorted: 75 56 85 90 49 26 12 48 40 47
split:     75 56 85 90 49 26 12 48 40 47
           75 56 85 90 49
                       26 12 48 40 47
split:     75 56 85 90 49
           75 56 85
                       90 49
split:     75 56 85
           75 56
                       85
split:     75 56
           75
               56
merge:     75
               56
           56 75
```

图 19.11 | 测试归并排序类。 （第 1 部分，共 2 部分。）

对 merge 的调用在最坏情况下需要 n-1 次比较来填充原始数组，即为 O(n)。 （请回忆，每个数组元素都可以通过比较来自两个子数组的各一个元素来选择。）对 sortArray 的两次调用导致对 sortArray 的另外四次递归调用，每个调用的子数组大约是原始数组大小的四分之一，同时还有两次对 merge 方法的调用。这两次对 merge 方法的调用在最坏情况下各需要 n/2 – 1 次比较，总比较次数为 O(n)。此过程继续，每个 sortArray 调用生成另外两次 sortArray 调用和一次 merge 调用，直到算法将数组拆分为单元素子数组。在每个层级，合并子数组需要 O(n) 次比较。每个层级将数组大小减半，因此将数组大小加倍需要多一个层级。将数组大小四倍化需要多两个层级。这种模式是对数式的，导致 log2 n 个层级。这导致总效率为 O(n log n)。

图 19.12 总结了本章介绍的搜索和排序算法及其 Big O。图 19.13 列出了本章介绍的 Big O 值以及 n 的若干值，以突出增长率的差异。

图 19.12 | 具有 Big O 值的搜索和排序算法。

| Algorithm | Location | Big O |
|---|---|---|
|Searching Algorithms:|||
|Linear search|Section 19.2.1|O(n)|
|Binary search|Section 19.2.2|O(log n)|
|Recursive linear search|Exercise 19.8|O(n)|
|Recursive binary search|Exercise 19.9|O(log n)|
|Sorting Algorithms:|||
|Selection sort|Section 19.3.1|O(n²)|
|Insertion sort|Section 19.3.2|O(n²)|
|Merge sort|Section 19.3.3|O(n log n)|
|Bubble sort|Exercises 19.5 and 19.6|O(n²)|

图 19.13 | 常见 Big O 表示法的比较次数。

| n = | O(log n) | O(n) | O(n log n) | O(n²) |
|---|---|---|---|---|
|1|0|1|0|1|
|2|1|2|2|4|
|3|1|3|3|9|
|4|1|4|4|16|
|5|1|5|5|25|
|10|1|10|10|100|
|100|2|100|200|10,000|
|1,000|3|1,000|3,000|10^6|
|1,000,000|6|1,000,000|6,000,000|10^12|
|1,000,000,000|9|1,000,000,000|9,000,000,000|10^18|

## 19.4 Wrap-Up

本章介绍了搜索和排序。我们讨论了两种搜索算法——线性搜索和二分搜索——以及三种排序算法——选择排序、插入排序和归并排序。我们介绍了 Big O 记法，它有助于分析算法的效率。接下来的三章将继续讨论可在执行时增长或缩小的动态数据结构。第 20 章介绍 Java API 的内置算法（如搜索和排序）和通用集合。第 21 章演示如何使用 Java 的泛型功能实现泛型方法和类。第 22 章讨论实现泛型数据结构的细节。

## Summary

### Section 19.1 Introduction

- Searching (p. 799) 涉及确定搜索键是否在数据中，如果在，则找到其位置。
- Sorting (p. 799) 涉及将数据按顺序排列。

### Section 19.2 Searching Algorithms

- 线性搜索算法 (p. 800) 顺序搜索数组中的每个元素，直到找到正确元素，或直到在未找到元素的情况下到达数组末尾。
- 搜索算法之间一个主要区别是它们返回结果所需的努力量。
- Big O 记法 (p. 802) 描述算法的效率，即解决问题的所需工作量。对于搜索和排序算法，它通常取决于数据中的元素数量。
- O(1) 算法不一定只需要一次比较 (p. 803)。它只是意味着比较次数不会随着数组大小的增加而增长。
- O(n) 算法被称为具有线性运行时间 (p. 803)。
- Big O 设计用于突出主导因素并忽略在高 n 值时变得不重要的项。
- Big O 记法关注算法运行时间的增长率，因此常数被忽略。
- 线性搜索算法运行时间为 O(n)。
- 线性搜索的最坏情况是必须检查每个元素以确定搜索项是否存在。这发生在搜索键是数组中最后一个元素或不存在时。
- 二分搜索 (p. 804) 比线性搜索更有效，但要求数组已排序。
- 二分搜索的第一次迭代测试数组中的中间元素。如果这是搜索键，算法返回其位置。如果搜索键小于中间元素，搜索将继续进行数组的前半部分。如果搜索键大于中间元素，搜索将继续进行数组的后半部分。每次迭代测试剩余数组的中间值，如果未找到元素，则消除剩余元素的一半。
- 二分搜索是一种比线性搜索更有效的搜索算法，因为每次比较都会从考虑中消除数组中一半的元素。
- 二分搜索运行时间为 O(log n)，因为每一步都去掉剩余元素的一半；这也称为对数运行时间 (p. 809)。
- 如果数组大小加倍，二分搜索只需要一次额外的比较。

