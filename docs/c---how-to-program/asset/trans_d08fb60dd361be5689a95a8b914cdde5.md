
插入。第 48 行将元素向右移动，第 49 行递减下一次插入元素的位置。循环结束后，第 52 行将元素插入到位。该程序的输出使用短横线表示每趟后数组中已排序的部分。星号放在该趟中插入到位的元素旁边。

```c
// Fig. D.2: figD_02.c
// The insertion sort algorithm.
#define SIZE 10
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// function prototypes
void insertionSort(int array[], size_t length);
void printPass(int array[], size_t length, unsigned int pass, size_t index);

int main(void)
{
    int array[SIZE]; // declare the array of ints to be sorted

    srand(time(NULL)); // seed the rand function

    for (size_t i = 0; i < SIZE; i++) {
        array[i] = rand() % 90 + 10; // give each element a value
    }

    puts("Unsorted array:");

    for (size_t i = 0; i < SIZE; i++) { // print the array
        printf("%d  ", array[i]);
    }

    puts("\n");
    insertionSort(array, SIZE);
    puts("Sorted array:");

    for (size_t i = 0; i < SIZE; i++) { // print the array
        printf("%d  ", array[i]);
    }
}

// function that sorts the array
void insertionSort(int array[], size_t length)
{
    // loop over length - 1 elements
    for (size_t i = 1; i < length; i++) {
        size_t moveItem = i; // initialize location to place element
        int insert = array[i]; // holds element to insert
```

**图 D.2** | 插入排序算法。（第 1 部分，共 3 部分。）

```c
45 // search for place to put current element
46 while (moveItem > 0 && array[moveItem - 1] > insert) {
47 // shift element right one slot
48 array[moveItem] = array[moveItem - 1];
49 --moveItem;
50 }

52 array[moveItem] = insert; // place inserted element
53 printPass(array, length, i, moveItem);
54 }

56 // function that prints a pass of the algorithm
57 void printPass(int array[], size_t length, unsigned int pass, size_t index)
58 {
59 printf("After pass %2d: ", pass);

61 // output elements till selected item
62 for (size_t i = 0; i < index; i++) {
63 printf("%4d ", array[i]);
64 }

66 printf("%4d* ", array[index]); // indicate swap

68 // finish outputting array
69 for (size_t i = index + 1; i < length; i++) {
70 printf("%4d ", array[i]);
71 }

73 printf("%s", "\n"); // for alignment

75 // indicate amount of array that is sorted
76 for (size_t i = 0; i <= pass; i++) {
77 printf("%s", "-- ");
78 }

80 puts(""); // add newline
81 }
```

未排序数组：
72 16 11 92 63 99 59 82 99 30

第 1 趟后：16* 72 11 92 63 99 59 82 99 30
--

第 2 趟后：11* 16 72 92 63 99 59 82 99 30
-- --

第 3 趟后：11 -- 16 72 92* 63 99 59 82 99 30
-- -- --

第 4 趟后：11 16 63* 72 -- 92 99 59 82 99 30
-- -- -- --

第 5 趟后：11 16 63 72 99* 59 82 99 30
-- -- -- -- --

第 6 趟后：11  16  59* 63  72  92  99  82  99  30
                 --  --  --  --  --  --  --
第 7 趟后：11  16  59  63  72  82* 92  99  99  30
                 --  --  --  --  --  --  --  --
第 8 趟后：11  16  59  63  72  82  92  99  99* 30
                 --  --  --  --  --  --  --  --
第 9 趟后：11  16  30* 59  63  72  82  92  99  99
                 --  --  --  --  --  --  --  --
排序后的数组：
11  16  30  59  63  72  82  92  99  99

**图 D.2** | 插入排序算法。（第 3 部分，共 3 部分。）

## 插入排序的效率

插入排序算法同样在 $O(n^2)$ 时间内运行。与选择排序一样，插入排序函数使用嵌套循环。for 循环（第 41—54 行）迭代 SIZE - 1 次，将一个元素插入到目前已排序元素中的适当位置。对于本应用而言，SIZE - 1 等价于 $n - 1$（因为 SIZE 是数组的大小）。while 循环（第 46—50 行）遍历数组中前面的元素。最坏情况下，这将需要 $n - 1$ 次比较。每个单独的循环都在 $O(n)$ 时间内运行。在大 O 记法中，嵌套循环意味着必须将每个循环的迭代次数相乘。对于外层循环的每次迭代，内层循环都会有一定数量的迭代。在该算法中，对于外层循环的每次 $O(n)$ 迭代，内层循环都会有 $O(n)$ 次迭代。将这些值相乘，得到的大 O 为 $O(n^2)$。

## D.5 归并排序

归并排序算法很高效，但在概念上比选择排序和插入排序更复杂。归并排序算法通过将数组拆分为两个大小相等的子数组、对每个子数组排序，然后将它们合并为一个更大的数组来排序。当元素个数为奇数时，该算法创建两个子数组，使其中一个比另一个多一个元素。

本示例中归并排序的实现是递归的。基准情形是只有一个元素的数组。只有一个元素的数组当然已经排好序，因此当以单元素数组调用归并排序时，它会立即返回。递归步骤将包含两个或更多元素的数组拆分为两个大小相等的子数组，递归地对每个子数组排序，然后将它们合并为一个更大的已排序数组。[同样，如果元素个数为奇数，则一个子数组比另一个多一个元素。]

假设该算法已经合并了较小的数组，创建了已排序数组 A：

```
4   10   34   56   77
```

以及 B：

```
5   30   51   52   93
```

归并排序将这两个数组合并为一个更大的已排序数组。A 中最小的元素是 4（位于 A 的索引 0 处）。B 中最小的元素是 5（位于 B 的索引 0 处）。为了确定较大数组中的最小元素，该算法比较 4 和 5。来自 A 的值更小，因此 4 成为合并后数组的第一个元素。该算法继续比较 10（A 中的第二个元素）与 5（B 中的第一个元素）。来自 B 的值更小，因此 5 成为较大数组的第二个元素。该算法继续比较 10 与 30，10 成为数组的第三个元素，依此类推。

图 D.3 实现了归并排序算法，第 35—38 行定义了归并排序函数。第 37 行调用函数 sortSubArray，参数为 0 和 length − 1（length 是数组的大小）。这些参数对应于要排序数组的起始索引和结束索引，使 sortSubArray 作用于整个数组。函数 sortSubArray 定义在第 41—64 行。第 44 行测试基准情形。如果数组大小为 1，则数组已排序，因此函数将立即返回。如果数组大小大于 1，函数将数组一分为二，递归调用函数 sortSubArray 对两个子数组排序，然后合并它们。第 58 行递归调用函数 sortSubArray 处理数组的前半部分，第 59 行递归调用函数 sortSubArray 处理数组的后半部分。当这两个函数调用返回时，数组的每一半都已排序。第 62 行对数组的两半调用函数 merge（第 67—114 行），将两个已排序数组合并为一个更大的已排序数组。

```c
// Fig. D.3: FigD_03.c
// The merge sort algorithm.
#define SIZE 10
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Function prototypes
void mergeSort(int array[], size_t length);
void sortSubArray(int array[], size_t low, size_t high);
void merge(int array[], size_t left, size_t middle,
    size_t middle2, size_t right);
void displayElements(int array[], size_t length);
void displaySubArray(int array[], size_t left, size_t right);

int main(void)
{
    int array[SIZE]; // declare the array of ints to be sorted

    srand(time(NULL)); // seed the rand function

    for (size_t i = 0; i < SIZE; i++) {
        array[i] = rand() % 90 + 10; // give each element a value
    }

    puts("Unsorted array:");
    displayElements(array, SIZE); // print the array
    puts("\\n");
    mergeSort(array, SIZE); // merge sort the array
    puts("Sorted array:");
```

**图 D.3** | 归并排序算法。（第 1 部分，共 5 部分。）
