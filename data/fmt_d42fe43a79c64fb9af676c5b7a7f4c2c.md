
```cpp
****************************************************************
* 检查字符串是否为回文的程序
****************************************************************
#include <iostream>
#include <string>
using namespace std;

// 递归函数的声明
bool isPalindrome(string str);
int main () {
    // 实例化一些字符串
    string str1("");
    string str2("rotor");
    string str3("hello");
    // 检查回文
    cout << boolalpha;
    cout << "Is a palindrome? " << isPalindrome(str1) << endl;
    cout << "Is rotor a palindrome? " << isPalindrome(str2) << endl;
    cout << "Is hello a palindrome? " << isPalindrome(str3) << endl;
    return 0;
}
// 递归函数的定义
bool isPalindrome(string str)
{}
```

（继续）

# 程序 17.5 使用递归 isPalindrome 函数（继续）

```cpp
if (str.size() <= 1) {
    return true;
}
else if (str[0] != str[str.size() - 1]) {
    return false;
}
return isPalindrome(str.substr(1, str.size() - 2));
}
```

运行:

Is "palindrome" true // 空字符串

Is 'rotor' a palindrome? true

Is 'hello' a palindrome? false

# 17.1.3 尾递归和非尾递归函数

在前面的节讨论的示例中，我们遇到了两种类型的递归：尾递归和非尾递归（图 17.8）。

# 尾递归

在尾递归中，每个一般情况在调用下一个一般情况或基准情况后终止。换句话说，一般情况的职责是调用下一个一般函数或基准函数。基准情况的职责是将整个操作的结果返回给 main 函数。在尾递归中，持有下次函数调用记录的栈只有一个记录，因为当调用下一个函数时，当前函数已经终止了。

图 17.8 尾函数和非尾函数的区别

## 17.1 引言

并且其记录从栈中弹出。我们到目前为止看到的尾递归函数示例有 `gcd` 和 `isPalindrome`。请注意，如果我们设计一个 `void` 类型的递归函数，它是一个尾递归函数，其基准情况不向主函数返回任何内容。

## 非尾递归

**在非局部递归中**，通用调用的职责在下一次调用返回之前不会结束。当前函数将它持有的信息与下一次调的信息相结合，并传递给上一个情况。最终信息由第一个通用情况返回给主函数。在非局部递归中，栈持有下一次递归调用的记录直到其返回。讨论的非局部递归函数示例有 `sum`、`factorial`、`fibonacci` 和 `reverse`。

## 17.1.4 辅助函数

递归函数可能是低效的。特别是，非局部递归函数低效的原因有两个：首先，每个通用情况都必须持有信息，直到下一次调用的结果返回。此外，栈会持有许多记录，这可能需要大量的内存。为了提高效率，我们可以使用辅助函数。**辅助函数**是一个比非局部递归函数更多参数的尾递归函数。我们可以使用非递归函数来调用辅助函数。图 17.9 显示了该设计。

我们知道 `sum` 函数不是尾函数，且当参数很大时是低效的。我们可以创建一个尾递归函数作为辅助函数，并带有一个额外的参数 (`result`) 用来存储 `n` 的值，否则该值将作为变量持有。每次递归调用都将此参数传递给下一次调用，没有额外的内存消耗。由于辅助函数也是尾递归函数，栈的低效问题也消除了。程序 17.6 显示了该版本的 `sum` 函数。

![](img/ce9c99d45f71111839bc062830bd19fd_807_0.png)

**图 17.9** 使用辅助函数消除低效

## 程序 17.6 在 sum 函数中使用辅助函数

| 行号 | 内容 |
| :--- | :--- |
| 1 | * 一个使用辅助函数创建尾递归函数的程序， |
| 2 | * 该函数比非尾函数更有效率 |/ |
| 3 | #include <iostream> |
| 4 | using namespace std; |
| 5 | // 函数声明 |
| 6 | int sum(int n); |
| 7 | int sum(int n, int result); |
| 8 | int main () |
| 9 | { |
| 10 | // 调用四次非递归函数 |
| 11 | cout << "Sum (0) = " << sum(0) << endl; |
| 12 | cout << "Sum (1) = " << sum(1) << endl; |
| 13 | cout << "Sum (3) = " << sum(3) << endl; |
| 14 | cout << "Sum (7) = " << sum(7) << endl; |
| 15 | return 0; |
| 16 | } |
| 17 | // 非递归 |
| 18 | int sum(int n) |
| 19 | { |
| 20 | return sum(n, 0); |
| 21 | } |
| 22 | // 递归 |
| 23 | int sum(int n, int result) |
| 24 | { |
| 25 | if (n == 0) |
| 26 | return result; |
| 27 | } |
| 28 | return sum(n - 1, n + result); |
| 29 | } |

运行:

Sum(0) = 0

Sum(1) = 1

Sum(3) = 6

Sum(7) = 28

作为另一个示例，我们使用辅助函数重新设计了 `isPalindrome` 函数。注意，`isPalindrome` 已经是一个尾递归函数，但重新设计它消除了每次调用函数时创建子字符串的低效性。

## 程序 17.7 使用辅助函数的 isPalindrome 函数

| 行号 | 内容 |
| :--- | :--- |
| 1 | * 一个通过使用辅助函数检查字符串是否为回文的程序，* |
| 2 | * 以避免创建子字符串对象 * |
| 3 | ************************************************* |
| 4 | #include <string> |
| 5 | #include <iostream> |
| 6 | using namespace std; |
| 7 | |
| 8 | // 函数声明 |
| 9 | bool isPalindrome(const string& str); |
| 10 | bool isPalindrome(const string& str, int left, int right); |
| 11 | |
| 12 | int main () { |
| 13 | // 检查字符串是否为回文 |
| 14 | cout << boolalpha; |
| 15 | cout << "Is 'rotor' a palindrome?" << isPalindrome("rotor") << endl; |
| 16 | cout << "Is 'madam' a palindrome?" << isPalindrome("madam") << endl; |
| 17 | cout << "Is 'Hello' a palindrome?" << isPalindrome("Hello") << endl; |
| 18 | return 0; |
| 19 | } | |
| 20 | // 非递归 isPalindrome 定义 |
| 21 | bool isPalindrome(const string& str) |
| 22 | { |
| 23 | return isPalindrome(str, 0, str.size() - 1); |
| 24 | } |
| 25 | // 辅助 isPalindrome 定义 |
| 26 | bool isPalindrome(const string& str, int left, int right) |
| 27 | { |
| 28 | if (left >= right) |
| 29 | return true; |
| 30 | } |
| 31 | else if (str[left] != str[right]) |
| 32 | return false; |
| 33 | } |
| 34 | return isPalindrome(str, left + 1, right - 1); |
| 35 | } |

运行:

Is 'rotor' true

Is 'madam' true

Is 'hello' false

## 17.2 递归排序与搜索

在计算机科学中，我们经常需要对列表进行排序。列表排序后搜索可以非常快。排序意味着重新排列列表元素使其有序。这是一种快速快速排序。

### 17.2.1 快速排序

快速排序算法使用基准（通常选择第一个元素），使得大于或等于基准的元素移动之后，小于基准的元素移动到之前。以下是分区算法。

#### 分区算法

```
int partition (int arr[], int beg, int end) {
    int p = arr[beg]; // p 是基准
    int i = beg;
    int j = end;
    while (i < j) { // 外层循环
        while (i < j && arr[i] <= p) { // 第一个内部循环
            i++;
        }
        while (i < j && arr[j] > p) { // 第二个内部循环
            j--;
        }
        if (i < j) {
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[beg], arr[i]);
    return i;
}
```

```cpp
void quicksort (int arr[], int beg, int end) {
    if (beg < end) {
        int p = partition(arr, beg, end);
        quicksort(arr, beg, p - 1);
        quicksort(arr, p + 1, end);
    }
}
```

# 程序 17.8 快速排序程序（续）

```cpp
print (array, 10);
return 0;
}
// 交换函数
void swap (int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}
// 打印数组函数
void print (int array[], int size)
{
    for (int i = 0; i < size; i++) {
        cout << array[i] << " ";
    }
    cout << endl;
}
// 分区函数
void partition (int arr[], int beg, int end)
{
    int p = beg; // 初始化基值
    int i = beg; // 初始化 i
    int j = end;
    while (i < j) {
        // 将 j 向左移动
        while (arr[j] > arr[p]) {
            j--;
        }
        swap(arr[j], arr[p]);
        p = j;
        // 将 i 向右移动
        while (arr[i] < arr[p]) {
            i++;
        }
        swap(arr[i], arr[p]);
        p = i;
    }
68 return p;
}
// 快速排序函数
void quickSort(int arr[], int beg, int end)
{
    if (beg >= end || beg < 0)
    {
        return;
    }
    int pivot = partition(arr, beg, end);
    quickSort(arr, beg, pivot - 1);
    quickSort(arr, pivot + 1, end);
}
```

运行：

原始数组：

| 27 | 22 | 11 | 94 | 83 | 14 | 30 | 19 | 46 | 33 |

排序后的数组：

| 14 | 19 | 22 | 27 | 30 | 33 | 46 | 83 | 94 |

容易得多。因为如果电话簿中的条目没有排序，在电话簿中查找条目将非常困难。二分查找算法的设计用于在有序数组中查找值。二分查找从查看中间元素开始。我们有三种情况：

- 如果该值等于中间元素，搜索停止。已找到数组索引。
- 如果该值大于中间元素，则在数组的右半部分继续搜索。
- 如果该值小于中间元素，则在数组的左半部分继续搜索。

图 17.12 是二分查找的一个示例。我们在包含 10 个元素的有序数组中查找 30。在尝试三次后，返回值 5。

要查找的值：30

| low | mid | high | | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 11 | 14 | 19 | 22 | 27 | 30 | 33 | 46 | 83 | 94 |
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
| low | mid | high | | | | | | | | | |
| 11 | 14 | 19 | 22 | 27 | 30 | 33 | 46 | 83 | 94 |
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
| low | high | | | | | | | | | | |
| 11 | 14 | 19 | 22 | 27 | 30 | 33 | 46 | 83 | 94 |
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

- 图例：
* 已搜索
* 未搜索
* 不是元素

图 17.12 在索引 5 找到值，二分查找示例

# 17.2 递归排序与搜索

```cpp
int main ()
{
    binarySearch (...);
    binarySearch (...);
}
```

| 图例 |
| :--- |
| 函数调用 |
| 返回值 |
| 非递归 |
| 递归通用 |
| 递归基准情况 |
| 主函数 |

图 17.13 二分查找算法的设计

注意：我们有两个基准情况。

# 递归二分查找

图 17.13 显示了使用辅助函数的递归搜索算法。

如图 17.13 所示，我们有两个基准情况。在第一种，未找到值；在第二种，找到了。

在传统的二分查找中，应用程序使用数组名、要查找的值来调用搜索函数，例如 `binarySearch(arr, size, value)`。如果该值不是中间元素，我们必须再次调用，但新的调用必须只搜索数组的左部分或右部分。如果我们想搜索左部分，不需要更改数组指针，但如果我们想搜索右部分，则有将将指针移动到中间元素之后并调整大小。使用一个不移动数组指针但在每次调用中处理数组中从 low 到 high 的子数组的辅助函数是方便且高效的。递归调用的格式为 `binarySearch(arr, low, high)`。在每次调用中，`low` 或 `high` 的值会变化；`arr` 指针和搜索参数保持不变。

程序 17.9 如何使用辅助函数实现二分查找：

```cpp
************************************************
* 一个使用递归搜索在数组中
* 查找值的程序
************************************************
#include <iostream>
using namespace std;

// 非递归和递归搜索函数的声明
int binarySearch(int arr[], int size, int value);
int binarySearch(int arr[], int low, int high);
// 待查找数组的声明
const int size = 10;
int array[size] = {11, 14, 19, 22, 27, 30, 33, 46, 83, 94};
```

（续）

# 17.2 递归排序查找
