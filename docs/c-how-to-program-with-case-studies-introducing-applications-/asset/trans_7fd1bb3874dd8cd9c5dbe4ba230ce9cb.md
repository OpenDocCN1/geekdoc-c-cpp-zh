
```c
// function that prints a pass of the algorithm
void printPass(int array[], size_t length, int pass, size_t index) {
    printf("After pass %2d: ", pass);
    
    // output elements till selected item
    for (size_t i = 0; i < index; i++) {
        printf("%d ", array[i]);
    }
    
    printf("%d* ", array[index]); // indicate swap
    
    // finish outputting array
    for (size_t i = index + 1; i < length; i++) {
        printf("%d ", array[i]);
    }
    
    printf("%s", "\n"); // for alignment
    
    // indicate amount of array that is sorted
    for (int i = 0; i < pass; i++) {
        printf("%s", "-- ");
    }
    
    puts(""); // add newline
}
```

```
Unsorted array:
72 34 88 14 32 12 34 77 56 83

After pass 1: 12 34 88 14 32 72* 34 77 56 83
  --

After pass 2: 12 14 88 34* 32 72 34 77 56 83
  -- --

After pass 3: 12 14 32 34 88* 72 34 77 56 83
  -- -- --

After pass 4: 12 14 32 34* 88 72 34 77 56 83
  -- -- -- --

After pass 5: 12 14 32 34 34 72 88* 77 56 83
  -- -- -- -- --

After pass 6: 12 14 32 34 34 56 88 77 72* 83
  -- -- -- -- -- --

After pass 7: 12 14 32 34 34 56 72 77 88* 83
  -- -- -- -- -- -- --

After pass 8: 12 14 32 34 34 56 72 77* 88 83
  -- -- -- -- -- -- -- --

After pass 9: 12 14 32 34 34 56 72 77 83 88*
  -- -- -- -- -- -- -- -- --

Sorted array:
12 14 32 34 34 56 72 77 83 88
```

**图 13.1** | 选择排序算法。（第 3 部分，共 3 部分。）

在函数 selectionSort（第 40–55 行）中，变量 smallest（第 43 行）存储剩余最小元素的索引。第 42–54 行循环 length - 1 次。第 43 行将索引 i（数组中未排序部分的第一个索引）赋给 smallest。第 46–50 行处理剩余元素。对于每个元素，第 47 行判断该元素的值是否小于索引 smallest 处的元素。如果是，第 48 行将当前元素的索引赋给 smallest。此循环结束后，smallest 包含剩余最小元素的索引。第 52 行调用 swap（第 58–62 行）来交换位置 i 和 smallest 处的值，将剩余最小元素放到数组中的位置 i。

输出使用短横线标出每一趟之后保证已排序的数组部分。我们在该趟中与最小元素交换的元素旁边放置一个星号。星号左侧的元素和最右侧短横线上方的元素，就是每一趟中被交换的两个值。

### 13.3.2 选择排序的效率

选择排序算法的运行时间为 O(n²)。在我们的 selectionSort 函数中，外层循环（第 42–54 行）处理数组的前 n – 1 个元素，将剩余最小项交换到其有序位置。内层循环（第 46–50 行）处理剩余项，查找最小元素。该循环在第一次外层循环迭代期间执行 n – 1 次，在第二次执行 n – 2 次，然后是 n – 3、…、3、2、1。因此，这个内层循环总共迭代 n(n – 1) / 2 次，即 (n² – n)/2 次。在大 O 记号中，较小的项被舍去，常数被忽略，最终得到的大 O 为 O(n²)。

### 自测

- 1（讨论）考虑以下数组，它反映了选择排序第一趟的结果：

  4 56 34 10 77 51 93 30 5 52

  第二趟会做什么？展示结果数组。

  答案：第二趟将 56 与 5（第二小元素）交换，结果为：4 5 34 10 77 51 93 30 56 52

- 2（代码）考虑以下 selectionSort 函数：

  ```c
  void selectionSort(int array[], size_t length) {
    // loop over length - 1 elements
    for (size_t i = 0; i < length - 1; i++) {
      size_t smallest = i; // first index of remaining array

      // loop to find index of smallest element
      for (size_t j = i + 1; j < length; j++) {
        if (array[j] < array[smallest]) {
          ???
        }
      }

      swap(array, i, smallest); // swap smallest element
      printPass(array, length, i + 1, smallest); // output pass
    }
  }
  ```

  第 9 行中应该用什么语句替换 ??? 以补全代码？

  答案：smallest = j;

```c
// fig13_02.c
// The insertion sort algorithm.
#define SIZE 10
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// function prototypes
void insertionSort(int array[], size_t length);
void printPass(int array[], size_t length, int pass, size_t index);

int main(void) {
    int array[SIZE] = {0}; // declare the array of ints to be sorted

    srand(time(NULL)); // seed the rand function

    for (size_t i = 0; i < SIZE; i++) {
        array[i] = rand() % 90 + 10; // give each element a value
    }

    puts("Unsorted array:");

    for (size_t i = 0; i < SIZE; i++) { // print the array
        printf("%d ", array[i]);
    }

    puts("\n");
    insertionSort(array, SIZE);
    puts("Sorted array:");

    for (size_t i = 0; i < SIZE; i++) { // print the array
        printf("%d ", array[i]);
    }

    puts("");
}

// function that sorts the array
void insertionSort(int array[], size_t length) {
    // loop over length - 1 elements
    for (size_t i = 1; i < length; i++) {
        size_t moveItem = i; // initialize location to place element
        int insert = array[i]; // holds element to insert

        // search for place to put current element
        while (moveItem > 0 && array[moveItem - 1] > insert) {
            // shift element right one slot
            array[moveItem] = array[moveItem - 1];
            --moveItem;
        }

        array[moveItem] = insert; // place inserted element
        printPass(array, length, i, moveItem);
    }
}

// function that prints a pass of the algorithm
void printPass(int array[], size_t length, int pass, size_t index) {
    printf("After pass %2d: ", pass);
    // output elements till selected item
    for (size_t i = 0; i < index; i++) {
        printf("%d ", array[i]);
    }
    printf("%d* ", array[index]); // indicate swap
    // finish outputting array
    for (size_t i = index + 1; i < length; i++) {
        printf("%d ", array[i]);
    }
    printf("%s", "\n"); // for alignment
    // indicate amount of array that is sorted
    for (size_t i = 0; i <= pass; i++) {
        printf("%s", "--- ");
    }
    puts(""); // add newline
}
```

```
Unsorted array:
72 16 11 92 63 99 59 82 99 30
After pass 1: 16* 72 11 92 63 99 59 82 99 30
--- ---
After pass 2: 11* 16 72 92 63 99 59 82 99 30
--- --- ---
After pass 3: 11 16 72 92* 63 99 59 82 99 30
--- --- --- ---
After pass 4: 11 16 63* 72 92 99 59 82 99 30
--- --- --- --- ---
After pass 5: 11 16 63 72 92 99* 59 82 99 30
--- --- --- --- --- ---
After pass 6: 11 16 59* 63 72 92 99 82 99 30
--- --- --- --- --- --- ---
After pass 7: 11 16 59 63 72 82* 92 99 99 30
--- --- --- --- --- --- --- ---
After pass 8: 11 16 59 63 72 82 92 99 99* 30
--- --- --- --- --- --- --- --- ---
After pass 9: 11 16 30* 59 63 72 82 92 99 99
--- --- --- --- --- --- --- --- --- ---
Sorted array:
11 16 30 59 63 72 82 92 99 99
```

**图 13.2** | 插入排序算法。（第 1 部分，共 2 部分。）

### 13.4.2 插入排序的效率

与选择排序一样，插入排序算法的运行时间为 $O(n^2)$。与 13.3.1 节中的函数 `selectionSort` 一样，`insertionSort` 函数也使用嵌套循环。外层循环（第 41–54 行）迭代 `SIZE − 1` 次，将元素插入到目前已排序元素中的适当位置。对于本应用程序而言，`SIZE − 1` 等价于 $n − 1$，其中 `SIZE` 是数组的元素个数。嵌套循环（第 46–50 行）遍历数组中当前元素之前的元素。在最坏情况下，这个 while 循环需要 $n − 1$ 次比较。每个单独的循环都在 $O(n)$ 时间内运行。在大 O 记号中，必须将嵌套循环中每个循环的迭代次数相乘。对于每次外层循环迭代，都会有一定数量的内层循环迭代。在这个算法中，对于每次 $O(n)$ 的外层循环迭代，都会有 $O(n)$ 次内层循环迭代。将这些值相乘，得到的大 O 为 $O(n^2)$。

### 自测

- 1. **（填空）** 插入排序算法的第一次迭代取数组的第二个元素，如果它小于第一个元素，就将其与第一个元素交换。第二次迭代查看第三个元素，并相对于前两个元素将其插入正确位置，从而使这三个元素都有序。在算法的第 $i$ 次迭代之后，数组的前 ____ 个元素将是有序的。

  **答案：** 前 $i$ 个。

- 2. **（讨论）** 插入排序和选择排序算法的运行时间都是 $O(n^2)$。它们各自具有的什么程序结构导致了 $O(n^2)$ 的运行时间？

  **答案：** 它们各自都有一个嵌套的 for 循环。

### 13.5 案例研究：可视化高性能归并排序

归并排序算法很高效，但在概念上比选择排序和插入排序更复杂。归并排序算法通过将数组分成两个大小相等的子数组、对每个子数组排序，然后将它们合并成一个更大的数组来对数组排序。当元素个数为奇数时，该算法创建两个子数组，使其中一个比另一个多一个元素。

本示例中的归并排序实现是递归的。基准情况是单元素数组，它当然是有序的。因此，当以单元素数组调用归并排序时，它会立即返回。递归步骤将包含两个或更多元素的数组分成两个大小相等的子数组，递归地对每个子数组排序，然后将它们合并成一个更大的有序数组。同样，如果元素个数为奇数，则一个子数组比另一个多一个元素。

假设该算法已经合并了较小的数组，创建了有序数组 A：

```
4    10    34    56    77
```

以及 B：

```
5    30    51    52    93
```
