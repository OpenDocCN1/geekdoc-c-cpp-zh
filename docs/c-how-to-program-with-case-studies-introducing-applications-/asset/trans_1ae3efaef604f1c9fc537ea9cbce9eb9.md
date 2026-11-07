
讨论一种简单的排序方案。在第 12 章和第 13 章中，我们将研究能带来更好性能的更复杂的方案。通常，最简单的算法性能较差。它们的优点在于易于编写、测试和调试。更复杂的算法通常是实现最大性能所必需的。

## Bubble Sort

图 6.12 将 10 个元素的数组 a 的值（第 8 行）按升序排序。我们使用的技术称为冒泡排序或下沉排序，因为较小的数值会像水中的气泡上升一样逐渐“冒泡”到数组顶部，而较大的数值则下沉到数组底部。该技术使用多次遍历数组。每次遍历时，算法比较连续的元素的对（元素 0 和元素 1，然后是元素 1 和元素 2，等等）。如果一对元素是递增顺序（或值相同），我们保持值不变。如果一对元素是递减顺序，我们在数组中交换它们的值。

```
~~~c
1 // fig06_12.c
2 // Sorting an array's values into ascending order.
3 #include <stdio.h>
4 #define SIZE 10
5
6 // function main begins program execution
7 int main(void) {
8     int a[SIZE] = {2, 6, 4, 8, 10, 12, 89, 68, 45, 37};
9
10     puts("Data items in original order");
11
12     // output original array
13     for (size_t i = 0; i < SIZE; ++i) {
14         printf("%4d", a[i]);
15     }
16
17     // bubble sort
18     // loop to control number of passes
19     for (int pass = 1; pass < SIZE; ++pass) {
20         // loop to control number of comparisons per pass
21         for (size_t i = 0; i < SIZE - 1; ++i) {
22             // compare adjacent elements and swap them if first
23             // element is greater than second element
24             if (a[i] > a[i + 1]) {
25                 int hold = a[i];
26                 a[i] = a[i + 1];
27                 a[i + 1] = hold;
28             }
29         }
30     }
31
32     puts("\nData items in ascending order");
33
34     // output sorted array
35     for (size_t i = 0; i < SIZE; ++i) {
36         printf("%4d", a[i]);
37     }
38
39     puts("");
40 }
~~~
```

Fig. 6.12 | 将数组的值按升序排序。（第 1 部分，共 2 部分。）

| 原始顺序的数据项 | 2 | 6 | 4 | 8 | 10 | 12 | 89 | 68 | 45 | 37 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 升序的数据项 | 2 | 4 | 6 | 8 | 10 | 12 | 37 | 45 | 68 | 89 |

Fig. 6.12 | 将数组的值按升序排序。（第 2 部分，共 2 部分。）

首先，程序比较 a[0] 与 a[1]，然后 a[1] 与 a[2]，然后 a[2] 与 a[3]，依此类推，直到通过比较 a[8] 与 a[9] 完成一次遍历。虽然有 10 个元素，但只执行了九次比较。由于连续比较的方式，一个大值可能在一轮遍历中向下移动很多位置，但一个小值每次只能向上移动一个位置。

第一次遍历时，最大的值保证下沉到数组的底部元素 a[9]。第二次遍历时，第二大的值保证下沉到 a[8]。第九次遍历时，第九大的值下沉到 a[1]。这使得最小值留在 a[0] 中，因此对 10 个元素的数组排序只需要九次遍历。

### Swapping Elements

排序由嵌套的 for 循环（第 19–30 行）执行。如果需要交换，则由第 25–27 行的三个赋值完成

```
    int hold = a[i];
    a[i] = a[i + 1];
    a[i + 1] = hold;
```

变量 hold 暂时存储正在交换的两个值之一。交换不能仅用两个赋值完成

```
    a[i] = a[i + 1];
    a[i + 1] = a[i];
```

例如，如果 a[i] 为 7 且 a[i + 1] 为 5，则在第一次赋值后，两个值都将为 5，值 7 将丢失——因此需要额外的变量 hold。

### Bubble Sort Is Easy to Implement, But Slow

冒泡排序的主要优点是易于编程。然而，它运行缓慢，因为每次交换只使一个元素更接近其最终位置一个位置。当对大型数组进行排序时，这一点变得明显。在练习中，我们将开发更高效的冒泡排序版本。比冒泡排序更高效的排序方法已经开发出来。我们将在第 13 章中研究其他算法。更高级的课程会更深入地研究排序和搜索。

## Self Check

1 (Multiple Choice) Which of the following statements a), b) or c) is true?
- a) The chief virtue of the bubble sort is that it’s easy to program.
- b) Bubble sort runs slowly because every exchange moves an element only one position closer to its final position. This becomes apparent when sorting large arrays.
- c) Far more efficient sorts than the bubble sort have been developed.
- d) All of the above statements are true.

Answer: d.

2 (True/False) If a swap is necessary in the bubble sort, it uses the assignments:

```
a[i] = a[i + 1];
a[i + 1] = a[i];
```

Answer: False. Actually, the swap requires one more variable and one more statement:

```
int hold = a[i];
a[i] = a[i + 1];
a[i + 1] = hold;
```

where the variable hold temporarily stores one of the two values being swapped.

## 6.9 Intro to Data Science Case Study: Survey Data Analysis

我们现在考虑一个更大的例子。计算机通常用于调查数据分析，以汇总和分析调查和民意调查的结果。图 6.13 使用数组 response 初始化了对一次调查的 99 个响应。每个响应都是 1 到 9 之间的数字。程序计算 99 个值的平均值、中位数和众数。此示例包括数组问题中所需的许多常见操作，包括向函数传递数组。请注意，第 48–52 行包含仅由空白分隔的多个字符串文字。C 编译器会自动将此类字符串文字合并为一个——这有助于使长字符串文字更易读。

// fig06_13.c
// Survey data analysis with arrays:
// computing the mean, median and mode of the data.
#include <stdio.h>
#define SIZE 99

// function prototypes
void mean(const int answer[]);
void median(int answer[]);
void mode(int freq[], const int answer[]);
void bubbleSort(int a[]);
void printArray(const int a[]);

Fig. 6.13 | 使用数组进行调查数据分析：计算数据的平均值、中位数和众数。（第 1 部分，共 5 部分。）

```
~~~c
13
14 // function main begins program execution
15 int main(void) {
16    int frequency[10] = {0}; // initialize array frequency
17
18    // initialize array response
19    int response[SIZE] =
20       {6, 7, 8, 9, 8, 7, 8, 9, 8, 9,
21        7, 8, 9, 5, 9, 8, 7, 8, 7, 8,
22        6, 7, 8, 9, 3, 9, 8, 7, 8, 7,
23        7, 8, 9, 8, 9, 8, 9, 7, 8, 9,
24        6, 7, 8, 7, 8, 7, 9, 8, 9, 2,
25        7, 8, 9, 8, 9, 8, 9, 7, 5, 3,
26        5, 6, 7, 2, 5, 3, 9, 4, 6, 4,
27        7, 8, 9, 6, 8, 7, 8, 9, 7, 8,
28        7, 4, 4, 2, 5, 3, 8, 7, 5, 6,
29        4, 5, 6, 1, 6, 5, 7, 8, 7};
30
31    // process responses
32    mean(response);
33    median(response);
34    mode(frequency, response);
35 }
36
37 // calculate average of all response values
38 void mean(const int answer[]) {
39    printf("%s\n%s\n%s\n", "********", "  Mean", "********");
40
41    int total = 0; // variable to hold sum of array elements
42
43    // total response values
44    for (size_t j = 0; j < SIZE; ++j) {
45       total += answer[j];
46    }
47
48    printf("The mean is the average value of the data\n"
49          "items. The mean is equal to the total of\n"
50          "all the data items divided by the number of\n"
51          "data items (%u). The mean value for\n"
52          "this run is: %u / %u = %.4f\n\n",
53          SIZE, total, SIZE, (double) total / SIZE);
54 }
55
56 // sort array and determine median element's value
57 void median(int answer[]) {
58    printf("\n%s\n%s\n%s\n%s", "********", " Median", "********",
59          "The unsorted array of responses is");
60
61    printArray(answer); // output unsorted array
62
63    bubbleSort(answer); // sort array
~~~
```

Fig. 6.13 | 使用数组进行调查数据分析：计算数据的平均值、中位数和众数。（第 2 部分，共 5 部分。）

