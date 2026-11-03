
首先，程序比较 a[0] 与 a[1]，然后比较 a[1] 与 a[2]，再比较 a[2] 与 a[3]，依此类推，直到通过比较 a[8] 与 a[9] 完成这一趟。尽管有 10 个元素，但只执行 9 次比较。由于连续比较的方式，较大的值在一趟中可能沿数组向下移动许多位置，而较小的值可能只向上移动一个位置。

在第一趟中，最大值保证会沉到数组的底部元素 a[9]。在第二趟中，第二大值保证会沉到 a[8]。在第九趟中，第九大值沉到 a[1]。这样就把最小值留在 a[0] 中，因此尽管有十个元素，也只需要对数组进行九趟排序。

排序由嵌套的 for 循环（第 21–34 行）执行。如果需要交换，则通过三个赋值完成

```
hold = a[i];
a[i] = a[i + 1];
a[i + 1] = hold;
```

其中额外的变量 hold 临时存储被交换的两个值之一。仅用两个赋值无法完成交换

```
a[i] = a[i + 1];
a[i + 1] = a[i];
```

例如，如果 a[i] 为 7 且 a[i + 1] 为 5，则在第一个赋值之后两个值都将为 5，而值 7 将丢失——因此需要额外的变量 hold。

冒泡排序的主要优点是易于编程。然而，它运行缓慢，因为每次交换只使一个元素向其最终位置靠近一个位置。在对大型数组排序时这一点会变得很明显。在练习中，我们将开发更高效的冒泡排序版本。已经开发出比冒泡排序高效得多的排序方法。我们将在附录 D 中研究其他算法。更高级的课程会更深入地研究排序和搜索。

## 6.9 案例研究：使用数组计算均值、中位数和众数

现在考虑一个更大的示例。计算机常用于调查数据分析，以汇编和分析调查与民意测验的结果。图 6.16 使用数组 response，并用一项调查的 99 个响应进行初始化。每个响应是 1 到 9 的数字。程序计算这 99 个值的均值、中位数和众数。图 6.17 包含该程序的示例运行。此示例包括数组问题中通常需要的大多数常见操作，包括将数组传递给函数。

```
1 // Fig. 6.16: fig06_16.c
2 // Survey data analysis with arrays:
3 // computing the mean, median and mode of the data.
4 #include <stdio.h>
5 #define SIZE 99
```

图 6.16 | 使用数组进行调查数据分析：计算数据的均值、中位数和众数。（第 1 部分，共 4 部分。）

```c
// function prototypes
void mean(const unsigned int answer[]);
void median(unsigned int answer[]);
void mode(unsigned int freq[], const unsigned int answer[]);
void bubbleSort(unsigned int a[]);
void printArray(const unsigned int a[]);

// function main begins program execution
int main(void)
{
    unsigned int frequency[10] = {0}; // initialize array frequency

    // initialize array response
    unsigned int response[SIZE] =
    {6, 7, 8, 9, 8, 7, 8, 9, 8, 9,
     7, 8, 9, 5, 9, 8, 7, 8, 7, 8,
     6, 7, 8, 9, 3, 9, 8, 7, 8, 7,
     7, 8, 9, 8, 9, 8, 9, 7, 8, 9,
     6, 7, 8, 7, 7, 9, 9, 8, 9, 2,
     7, 8, 9, 8, 9, 8, 9, 7, 5, 3,
     5, 6, 7, 2, 5, 3, 9, 4, 6, 4,
     7, 8, 9, 6, 8, 7, 8, 9, 7, 8,
     7, 4, 4, 2, 5, 3, 8, 7, 5, 6,
     4, 5, 6, 1, 6, 5, 7, 8, 7};

    // process responses
    mean(response);
    median(response);
    mode(frequency, response);
}

// calculate average of all response values
void mean(const unsigned int answer[])
{
    printf("\n\n\n\n%s\n%s\n%s\n", "********", " Mean", "********");
    unsigned int total = 0; // variable to hold sum of array elements

    // total response values
    for (size_t j = 0; j < SIZE; ++j) {
        total += answer[j];
    }

    printf("The mean is the average value of the data\n"
           "items. The mean is equal to the total of\n"
           "all the data items divided by the number\n"
           "of data items (%u). The mean value for\n"
           "this run is: %u / %u = %.4f\n\n",
           SIZE, total, SIZE, (double) total / SIZE);
}
```

57
58 // sort array and determine median element's value
59 void median(unsigned int answer[])
60 {
61     printf("\n%s\n%s\n%s\n", "**********", " Median ", "**********");
62     printf("The unsorted array of responses is\n");

63     printArray(answer); // output unsorted array

64     bubbleSort(answer); // sort array

65     printf("\n%s\n", "The sorted array is");
     printArray(answer); // output sorted array

     // display median element
     printf("\nThe median is element %u of\n"
            "the sorted %u element array.\n"
            "For this run the median is %u\n\n",
            SIZE / 2, SIZE, answer[SIZE / 2]);
}

78 // determine most frequent response
79 void mode(unsigned int freq[], const unsigned int answer[])
80 {
81     printf("\n%s\n%s\n%s\n", "**********", " Mode ", "**********");

     // initialize frequencies to 0
     for (size_t rating = 1; rating <= 9; ++rating) {
         freq[rating] = 0;
     }

     // summarize frequencies
     for (size_t j = 0; j < SIZE; ++j) {
         ++freq[answer[j]];
     }

     // output headers for result columns
     printf("%s %11s %19s\n", "Response", "Frequency", "Histogram");

     // output results
     unsigned int largest = 0; // represents largest frequency
     unsigned int modeValue = 0; // represents most frequent response

     for (rating = 1; rating <= 9; ++rating) {
         printf("%8u%11u", rating, freq[rating]);

图 6.16 | 使用数组进行调查数据分析：计算数据的均值、中位数和众数。（第 3 部分，共 4 部分。）

```c
// keep track of mode value and largest frequency value
if (freq[rating] > largest) {
    largest = freq[rating];
    modeValue = rating;
}

// output histogram bar representing frequency value
for (unsigned int h = 1; h <= freq[rating]; ++h) {
    printf("%s", "*");
}

puts(""); // begin a new line of output
}

// display the mode value
printf("\nThe mode is the most frequent value.\n"
"For this run the mode is %u which occurred "
"%u times.\n", modeValue, largest);
}

// function that sorts an array with bubble sort algorithm
void bubbleSort(unsigned int a[])
{
    // loop to control number of passes
    for (unsigned int pass = 1; pass < SIZE; ++pass) {

        // loop to control number of comparisons per pass
        for (size_t j = 0; j < SIZE - 1; ++j) {

            // swap elements if out of order
            if (a[j] > a[j + 1]) {
                unsigned int hold = a[j];
                a[j] = a[j + 1];
                a[j + 1] = hold;
            }
        }
    }
}

// output array contents (20 values per row)
void printArray(const unsigned int a[])
{
    // output array contents
    for (size_t j = 0; j < SIZE; ++j) {

        if (j % 20 == 0) { // begin new line every 20 values
            puts("");
        }

        printf("%2u", a[j]);
    }
}
```

~~~text
**********
   Mean
**********
The mean is the average value of the data
items. The mean is equal to the total of
all the data items divided by the number
of data items (99). The mean value for
this run is: 681 / 99 = 6.8788

**********
  Median
**********
The unsorted array of responses is
6 7 8 7 8 9 8 7 9 8 7 9 8 7 8 7 8
6 7 8 9 3 9 8 7 8 7 8 8 9 8 7 9 8 9
6 7 8 7 8 7 9 8 9 2 7 8 9 8 9 7 5 3
5 6 7 2 5 3 9 4 6 4 7 8 9 6 8 7 8 7
7 4 4 2 5 3 8 7 5 6 4 5 6 1 6 5 7 8 7

The sorted array is
1 2 2 2 3 3 3 4 4 4 4 5 5 5 5 5 5 5
5 6 6 6 6 6 6 6 6 7 7 7 7 7 7 7 7 7 7
7 7 7 7 7 7 7 7 7 7 7 7 8 8 8 8 8 8
8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8
9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9

The median is element 49 of
the sorted 99 element array.
For this run the median is 7

**********
   Mode
**********
Response  Frequency            Histogram

                                    1   1   2   2
                                5   0   5   0   5
1       1       *
2       3       ***
3       4       ****
4       5       *****
5       8       ********
6       9       *********
7       23      ***********************
8       27      ***************************
9       19      *******************

The mode is the most frequent value.
For this run the mode is 8 which occurred 27 times.
~~~

图 6.17 | 调查数据分析程序的示例运行。
