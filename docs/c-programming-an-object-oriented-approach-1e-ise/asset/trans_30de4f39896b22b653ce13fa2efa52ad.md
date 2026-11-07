

### 程序 17.7 使用辅助函数的 isPalindrome 函数

```cpp
/******************************************************************
 * A program that checks if a string is a palindrome by using      *
 * a helper function to avoid creating substring objects           *
 ******************************************************************/
#include <string>
#include <iostream>
using namespace std;

// Function declaration
bool isPalindrome (const string & str);
bool isPalindrome (const string & str, int left, int right);

int main ()
{
    // Checking if the strings are palindromes
    cout << boolalpha;
    cout << "Is 'rotor' a palindrome? " << isPalindrome ("rotor") << endl;
    cout << "Is 'madam' a palindrome? " << isPalindrome ("madam") << endl;
    cout << "Is 'Hello' a palindrome? " << isPalindrome ("Hello");
}
// Function definition for non-recursive isPalindrome
bool isPalindrome(const string& str)
{
    return isPalindrome (str, 0, str.size() - 1);
}
// Function definition for helper recursive isPalindrome
bool isPalindrome(const string& str, int left, int right)
{
    if (right <= left)
    {
        return true;
    }
    else if (str[left] != str[right])
    {
        return false;
    }
    return isPalindrome (str, left + 1, right - 1);
}

Run:
Is 'rotor' a palindrome? true
Is 'madam' a palindrome? true
Is 'Hello' a palindrome? false
```

## 17.2 递归排序与查找

在计算机科学中，我们经常需要对列表进行排序和查找。当列表已排序时，查找可以非常快。

### 17.2.1 快速排序

*排序*是指重新排列列表（例如数组）中的元素，使这些值按顺序排列。本节介绍的排序算法称为*快速排序*（一种递归算法）。这是一种快速且高效的算法，被用于大多数库中。快速排序算法使用一种称为*划分*的非递归算法，我们接下来讨论它。

### 划分算法

划分算法围绕一个*枢轴*（数组中的一个元素）重新排列数组，使所有大于或等于*枢轴*的元素移到它后面，所有小于*枢轴*的元素移到它前面。*枢轴*通常选择为第一个元素。

下面展示了划分算法。

```c
int partition (int arr[], int i, int j) // i and j are partition indexes
{
  int p = i; // p is the pivot
  while (i < j) // outer loop
  {
    while (arr[j] > arr[p]) // first inner loop
    {
      j--;
    }
    swap(arr[j], arr[p]);
    p = j;
    j--;
    while (arr[i] < arr[p]) // second inner loop
    {
      i++;
    }
    swap(arr[i], arr[p]);
    p = i;
    i++;
  }
  return p;
}
```

在外层循环的每次执行中，我们执行以下两组操作。

- 只要 *arr[j]* 大于 *arr[p]*，我们就将 *j* 向左移动。然后交换 *arr[j]* 和 *arr[p]* 的值，并设置 *p = j*。接着再将 *j* 向左移动一个元素。
- 只要 *arr[i]* 小于 *arr[p]*，我们就将 *i* 向右移动。然后交换 *arr[i]* 和 *arr[p]* 的值，并设置 *p = i*。接着再将 *i* 向右移动一个元素。

*枢轴* *p* 被设置为第一个元素，但它会移动到数组中的最终位置。注意，在第二次迭代之后，*i* 移动到 *j* 的右侧，外层循环终止。

![](img/d68f6199646ca63591a6d8419e0ed4ba_812_0.png)

**图例：**
- 递归调用
- 主函数
- 调用
- p：枢轴

**注意：** 每个分支中的基本情况在对应划分区域为空时到达。

**图 17.11** 快速排序算法的思想

### 程序 17.8 快速排序程序

```cpp
/***************************************************************
 * A program that uses the quicksort algorithm to sort an array *
 * by calling the partition algorithm recursively              *
 ***************************************************************/
#include <iostream>
using namespace std;

// Function declarations
void swap (int& x, int& y);
void print (int array[], int size);
int partition (int arr[], int beg, int end);
void quickSort (int arr[], int beg, int end);

int main ()
{
    // Declaration of an unsorted array
    int array [10] = {27, 22, 11, 94, 83, 14, 30, 19, 46, 33};
    // Printing unsorted array
    cout << "Original array: " << endl;
    print (array, 10);
    // Calling quickSort function
    quickSort (array, 0, 9);
    // Printing sorted array
    cout << "Sorted array: " << endl;
```

### 程序 17.8 快速排序程序（续）

```cpp
68  return p;
69 }
70 // Quick sort function
71 void quickSort (int arr[], int beg, int end)
72 {
73     if (beg >= end || beg < 0)
74     {
75         return;
76     }
77     int pivot = partition (arr, beg, end);
78     quickSort (arr, beg, pivot - 1);
79     quickSort (arr, pivot + 1, end);
80 }

Run:
Original array:
27 22 11 94 83 14 30 19 46 33
Sorted array:
11 14 19 22 27 30 33 46 83 94
```

会容易得多。例如，如果电话簿中的条目未排序，要在其中查找一个条目将非常困难。二分查找算法旨在在已排序数组中查找某个值。二分查找首先查看中间元素。我们可以有三种情况：

- 如果该值等于中间元素，则查找停止。已找到索引。
- 如果该值大于中间元素，则在数组的右半部分继续查找。
- 如果该值小于中间元素，则在数组的左半部分继续查找。

图 17.12 展示了一个二分查找的示例。我们在一个包含 10 个元素的已排序数组中查找值 30。经过三次尝试后，返回该值的索引 5。

![](img/d68f6199646ca63591a6d8419e0ed4ba_814_0.png)

![](img/d68f6199646ca63591a6d8419e0ed4ba_815_0.png)

### 递归二分查找

图 17.13 展示了使用辅助函数的递归二分查找算法。

如图 17.13 所示，我们有两个基本情况。第一种情况是未找到该值，第二种情况是找到了该值。

在传统二分查找中，应用程序使用数组名、大小和要查找的值来调用搜索函数，例如 `binarySearch(arr, size, value)`。如果该值不是中间元素，我们必须再次调用，但新的调用只能搜索数组的左半部分或右半部分。如果要搜索左半部分，数组指针不需要改变，但大小必须改变。如果要搜索右半部分，我们必须将数组指针移到中间元素之后，并调整大小。使用辅助函数会更方便、更高效：该函数不移动数组指针，而是在每次调用中使用从 `low` 到 `high` 的数组子部分。辅助递归调用的格式为 `binarySearch(arr, low, high, value)`。在每次调用中，只有 `low` 或 `high` 的值会改变；`arr` 指针和搜索参数保持不变。

程序 17.9 展示了如何使用辅助函数实现递归二分查找。

### 程序 17.9 递归二分查找

```cpp
/******************************************************
 * A program that uses the recursive binary search to search *
 * an array for a value                              *
 ******************************************************/
#include <iostream>
using namespace std;

// Declaration of non-recursive and recursive search functions
int binarySearch (const int arr[], int size, int value);
int binarySearch (const int arr[], int low, int high, int value);
// Declaration of array to be searched
const int size = 10;
int array [size] = {11, 14, 19, 22, 27, 30, 33, 46, 63, 94};
```

### 程序 17.9 递归二分查找（续）

```cpp
57  {
58      return binarySearch(arr, mid + 1, high, value);
59  }
60 }

Run:
Enter the value to be found: 11
The value was found at index: 0

Run:
Enter the value to be found: 27
The value was found at index: 4

Run:
Enter the value to be found: 94
The value was found at index: 9

Run:
Enter the value to be found: 10
The value is not in the array!

Run:
Enter the value to be found: 95
The value is not in the array!
```

### 17.2.3 汉诺塔

我们再讨论一个经典的递归问题：汉诺塔。它通常使用递归方法求解。在该问题中，有三根柱子（塔）。第一根柱子上叠放着一组圆盘，最小的圆盘在最上面。图 17.14 展示了四个圆盘的情形。

我们必须将圆盘从第一根柱子（A）移动到第三根柱子（C）。第二根柱子（B）用于在此过程中临时存放圆盘。该任务使用以下规则：

- 一次只能移动一个圆盘。
- 较大的圆盘绝不能叠放在较小的圆盘之上。
- 使用一根临时柱子（B）用于圆盘的中间存储。

这个问题有趣有两个原因。第一，递归解法比迭代解法更容易编写代码。第二，这个问题的解法模式与我们一直在讨论的简单示例不同。

![](img/d68f6199646ca63591a6d8419e0ed4ba_817_0.png)

**图 17.14** 只有四个圆盘的汉诺塔

