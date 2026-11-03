
// create some data
for (size_t x = 0; x < SIZE; ++x) {
    a[x] = 2 * x;
}

printf("Enter integer search key: ");
int searchKey; // value to locate in array a
scanf("%d", &searchKey);

// attempt to locate searchKey in array a
size_t index = linearSearch(a, searchKey, SIZE);

// display results
if (index != -1) {
    printf("Found value at index %d\n", index);
}
else {
    puts("Value not found");
}

// compare key to every element of array until the location is found
// or until the end of array is reached; return index of element
// if key is found or -1 if key is not found
size_t linearSearch(const int array[], int key, size_t size)
{
    // loop through array
    for (size_t n = 0; n < size; ++n) {
        if (array[n] == key) {
            return n; // return location of key
        }
    }

    return -1; // key not found
}

Enter integer search key: 36
Found value at index 18

Enter integer search key: 37
Value not found

图6.18 | 数组的线性搜索。（第2部分，共2部分）

## 6.10.2 使用二分查找搜索数组

线性查找方法适用于小型数组或未排序的数组。然而，对于大型数组，线性查找效率较低。如果数组已排序，则可以使用高速的二分查找技术。

二分查找算法在每次比较后，会从考虑范围内排除有序数组中的*一半*元素。算法定位数组的*中间元素*，并将其与搜索键进行比较。如果相等，则找到搜索键，并返回该元素的数组下标。如果不相等，问题就缩小为在数组的*一半*中继续搜索。如果搜索键小于数组的中间元素，则算法搜索数组的*前半部分*，否则算法搜索*后半部分*。如果搜索键不是指定子数组（原始数组的一部分）的中间元素，算法会在原始数组的四分之一部分重复上述过程。搜索继续，直到搜索键等于某个子数组的中间元素，或者直到子数组只包含一个不等于搜索键的元素（即未找到搜索键）。

在最坏的情况下，使用二分查找搜索包含1023个元素的有序数组，只需*10*次比较。反复将1,024除以2，得到512、256、128、64、32、16、8、4、2和1。数字1,024（2^10）除以2仅需10次即可得到1。在二分查找算法中，除以2相当于一次比较。包含1,048,576（2^20）个元素的数组最多需要*20*次比较即可找到搜索键。一个包含十亿个元素的有序数组最多需要*30*次比较即可找到搜索键。与对有序数组进行线性查找相比，性能有了巨大提升，因为线性查找平均需要将搜索键与一半的数组元素进行比较。对于十亿元素的数组，这相当于平均5亿次比较和最多30次比较之间的差别！任意数组的最大比较次数可以通过找到大于数组元素个数的第一个2的幂来确定。

图6.19展示了函数`binarySearch`的*迭代*版本（第40–68行）。该函数接收四个参数——要搜索的整数数组`b`、整数`searchKey`、`low`数组下标和`high`数组下标（这些定义了要搜索的数组部分）。如果搜索键与子数组的中间元素*不*匹配，则修改`low`下标或`high`下标，以便搜索更小的子数组。如果搜索键*小于*中间元素，则将`high`下标设置为`middle - 1`，并在从`low`到`middle - 1`的元素上继续搜索。如果搜索键*大于*中间元素，则将`low`下标设置为`middle + 1`，并在从`middle + 1`到`high`的元素上继续搜索。程序使用了一个包含15个元素的数组。大于该数组元素个数的第一个2的幂是16（2^4），因此查找搜索键最多需要4次比较。程序使用函数`printHeader`（第71–88行）输出数组下标，并使用函数`printRow`（第92–110行）在二分查找过程中输出每个子数组。每个子数组中的中间元素用星号（`*`）标记，以指示与搜索键比较的元素。

```c
1   // Fig. 6.19: fig06_19.c
2   // Binary search of a sorted array.
3   #include <stdio.h>
4   #define SIZE 15
5
6   // function prototypes
7   size_t binarySearch(const int b[], int searchKey, size_t low, size_t high);
```

图6.19 | 有序数组的二分查找。（第1部分，共4部分）

```
void printHeader(void);
void printRow(const int b[], size_t low, size_t mid, size_t high);

// function main begins program execution
int main(void)
{
    int a[SIZE]; // create array a

    // create data
    for (size_t i = 0; i < SIZE; ++i) {
        a[i] = 2 * i;
    }

    printf("%s", "Enter a number between 0 and 28: ");
    int key; // value to locate in array a
    scanf("%d", &key);

    printHeader();

    // search for key in array a
    size_t result = binarySearch(a, key, 0, SIZE - 1);

    // display results
    if (result != -1) {
        printf("\n%d found at index %d\n", key, result);
    }
    else {
        printf("\n%d not found\n", key);
    }
}

// function to perform binary search of an array
size_t binarySearch(const int b[], int searchKey, size_t low, size_t high)
{
    // loop until low index is greater than high index
    while (low <= high) {

        // determine middle element of subarray being searched
        size_t middle = (low + high) / 2;

        // display subarray used in this loop iteration
        printRow(b, low, middle, high);

        // if searchKey matched middle element, return middle
        if (searchKey == b[middle]) {
            return middle;
        }

        // if searchKey is less than middle element, set new high
        else if (searchKey < b[middle]) {
            high = middle - 1; // search low end of array
        }
    }
```

```
60
61 // if searchKey is greater than middle element, set new low
62 else {
63 low = middle + 1; // search high end of array
64 }
65 } // end while
66
67 return -1; // searchKey not found
68 }
69
70 // Print a header for the output
71 void printHeader(void)
72 {
73 puts("\nIndices:");
74
75 // output column head
76 for (unsigned int i = 0; i < SIZE; ++i) {
77 printf("%3u ", i);
78 }
79
80 puts("");
81 // start new line of output
82 // output line of - characters
83 for (unsigned int i = 1; i <= 4 * SIZE; ++i) {
84 printf("%s", "-");
85 }
86
87 puts("");
88 // start new line of output
89 }
90 // Print one row of output showing the current
91 // part of the array being processed.
92 void printRow(const int b[], size_t low, size_t mid, size_t high)
93 {
94 // loop through entire array
95 for (size_t i = 0; i < SIZE; ++i) {
96
97 // display spaces if outside current subarray range
98 if (i < low || i > high) {
99 printf("%s", " ");
100 }
101 else if (i == mid) { // display middle element
102 printf("%3d*", b[i]); // mark middle value
103 }
104 else { // display other elements in subarray
105 printf("%3d ", b[i]);
106 }
107 }
108
109 puts(""); // start new line of output
110 }
```

```
Enter a number between 0 and 28: 25
Indices:
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
0 2 4 6 8 10 12 14* 16 18 20 22 24 26 28
               16 18 20 22* 24 26 28
                           24 26* 28
                                 24*
25 not found
```

```
Enter a number between 0 and 28: 8
Indices:
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
0 2 4 6 8 10 12 14* 16 18 20 22 24 26 28
0 2 4 6* 8 10 12
        8 10* 12
            8*
8 found at index 4
```

```
Enter a number between 0 and 28: 6
Indices:
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
0 2 4 6 8 10 12 14* 16 18 20 22 24 26 28
0 2 4 6* 8 10 12
6 found at index 3
```

图6.19 | 有序数组的二分查找。（第4部分，共4部分）

## 6.11 多维数组

C语言中的数组可以有多个下标。多维数组（C标准将其称为 multidimensional arrays）的一个常见用途是表示由按行和列排列的信息组成的值表。要标识特定的表元素，我们必须指定两个下标：第一个（按惯例）标识元素的行，第二个（按惯例）标识元素的列。需要两个下标来标识特定元素的表或数组称为二维数组。多维数组可以具有两个以上的下标。

### 6.11.1 演示双下标数组

图6.20演示了一个二维数组a。该数组包含3行4列，因此称为3×4数组。通常，具有m行n列的数组称为m×n数组。

