

## 图 13.1 选择排序

## 一个程序

```
// FILE: select.cxx
// An interactive test program for the selectionsort function
#include <algorithm> // Provides swap
#include <cstddef> // Provides EXIT_SUCCESS, size_t
#include <iostream> // Provides cout and cin
using namespace std;

// PROTOTYPE of the function used in this test program:
void selectionsort(int data[], size_t n);
// Precondition: data is an array with at least n components.
// Postcondition: The elements are rearranged so that data[0] <= data[1] <= ... <= data[n-1].

int main( )
{
    const char BLANK = ' ';
    const size_t ARRAY_SIZE = 10; // Number of elements in the array to be sorted
    int data[ARRAY_SIZE]; // Array of integers to be sorted
    int user_input; // Number typed by the user
    size_t number_of_elements; // How much of the array is used
    size_t i; // Array index

    // Provide some instructions.
    cout << "Please type up to " << ARRAY_SIZE << " positive integers. ";
    cout << " Indicate the list's end with a zero." << endl;

    // Read the input numbers.
    number_of_elements = 0;
    cin >> user_input;
    while ((user_input != 0) && (number_of_elements < ARRAY_SIZE))
    {
        data[number_of_elements] = user_input;
        ++number_of_elements;
        cin >> user_input;
    }

    // Sort the numbers, and print the result with two blanks after each number.
    selectionsort(data, number_of_elements);
    cout << "In sorted order, your numbers are: " << endl;
    for (i = 0; i < number_of_elements; ++i)
        cout << data[i] << BLANK << BLANK;
    cout << endl;

    return EXIT_SUCCESS;
}
```

## （图 13.1 续）

```
void selectionsort(int data[ ], size_t n)
// Library facilities used: algorithm, cstdlib
{
    size_t i, j, index_of_largest;
    int largest;

    if (n == 0)
        return; // No work for an empty array

    for (i = n-1; i > 0; --i)
    {
        largest = data[0];
        index_of_largest = 0;
        for (j = 1; j <= i; ++j)
        {
            if (data[j] > largest)
            {
                largest = data[j];
                index_of_largest = j;
            }
        }
        swap(data[i], data[index_of_largest]);
    }
}
```

## 示例对话

请输入最多 10 个正整数。用零表示列表的结束。

80 10 50 70 60 90 20 30 40 0

按排序顺序，您的数字是：

10 20 30 40 50 60 70 80 90

在选择排序实现中，您会注意到 i 和 n 都是 size_t，因此我们添加了一个额外的 if 语句来处理“排序空数组”的情况（即 n 为零的情况）。在这种情况下，函数无需执行任何操作（没有元素可排序），但由于 size_t 值不能为负数，我们必须避免赋值 i = n-1。

## 选择排序——分析

我们想要分析我们作为函数 selectionsort 实现的选择排序算法的最坏情况运行时间。让我们使用 n 表示要排序的项目数量。在函数 selectionsort 中，n 是 size_t 参数 n 的值。
大致而言，选择排序算法的主要工作如下所示：

```
for (i = n-1; i > 0; --i)
swap(data[i], data[suitable index]);
```

当 i 等于 n-1 时，data[suitable index] 是数组中的最大元素；当 i 等于 n-2 时，data[suitable index] 是数组中的第二大元素，依此类推。

这个 for 循环执行多少次操作？答案并不容易。许多操作是隐藏的。循环控制变量 i 在每次循环迭代开始时与零进行比较。swap 函数使用若干赋值操作，而计算“合适索引”需要一些工作。i 的值在每次循环迭代结束时递减。我们可以确定循环中每个子任务的精确操作数。然而，这比我们需要的更详细。我们只需要一个大 O 近似，这意味着我们不需要常数的精确值。这将显著简化我们的分析。

在每次循环迭代期间，管理循环控制变量涉及若干常数次操作，调用 swap 函数也涉及若干常数次操作。因此，每次循环迭代的操作数是以下各项之和：

某个常数 + 查找合适索引的开销

由于有 n-1 次循环迭代，执行的操作总数由以下乘积给出：

(n - 1) × (某个常数 + 查找合适索引的开销)

要将其转换为用 n 表示的简洁公式，我们需要确定查找“合适索引”的开销。

事实证明，当算法查找要放置在位置 data[i] 的值时，“合适索引”是以下值中最大值的索引：

```
data[0], data[1], ..., data[i]
```

选择排序算法使用一个 for 循环来确定这个最大元素的位置，从而确定“合适索引”的值。这个循环查看这些数组元素中的每一个，并对每个元素执行若干常数次操作。由于 i 可以大到 n-1，在最坏情况下，循环将查看从 data[0] 到 data[n-1] 的所有 n 个数组元素，并对每个元素执行若干常数次操作。因此，我们估计查找这个“合适索引”的操作数最多为常数乘以 n。

将这些信息结合起来，我们看到在选择排序中执行的操作总数如下：

总数 = (n - 1) × (某个常数 + 查找合适索引的开销)
≤ (n - 1) × [某个常数 + (另一个常数) × n]

现在我们需要估计以下数量：

(n - 1) × [某个常数 + (另一个常数) × n]

如果你将其展开，你会得到一个 n² 项、一个 n 项和一个不含 n 的常数项。因此，执行的操作数为：

```
n² × (某个新常数)
+
n × (另一个新常数)
+
(又一个新常数)
```

这是我们对选择排序最坏情况运行时间的估计。因为我们进行的是大 O 分析，我们可以忽略常数，只考虑 n 的最高指数。因此，我们看到选择排序的最坏情况运行时间为 O(n²)。

这种对选择排序运行时间的分析不依赖于数组中的初始值。无论数组中包含什么值，选择排序算法执行的操作数都相同。因此，平均情况运行时间（甚至最好情况运行时间）与最坏情况运行时间相同。

> **选择排序运行时间**
> 
> 选择排序的最坏情况运行时间、平均情况运行时间和最好情况运行时间均为二次时间。

## 编程提示

### 粗略估计足以用于大 O

我们刚刚计算了选择排序算法最坏情况运行时间的大 O 表达式。请注意，在进行大 O 分析时，我们并未计算运行时间的精确公式。例如，在估计算法中主循环一次迭代的操作数时，我们决定算法在每次循环迭代中执行以下数量的操作：

```
某个常数 + 查找合适索引的开销
```

请注意，我们从未计算“某个常数”的精确值。因为大 O 表达式仅在“常数倍数范围内”准确，所以常数的精确值无关紧要。如果我们只需要一个大 O 表达式，就没有理由花时间计算这个常数的精确值。

## 插入排序

另一种简单而自然的排序算法基于对包含以下 10 个整数列表的数组进行排序的示例：

```
( 8, 2, 5, 3, 10, 7, 1, 4, 6, 9 )
```

一种方法是一次取一个数字，构建另一个排序后的值列表。第一个数字是 8，因此创建一个仅包含数字 8 的列表。这当然是一个排序后的列表。接下来取 2，将其与 8 组合以获得更长的排序列表，即 (2, 8)。接下来，添加 5 以获得列表：(2, 5, 8)。

如果你继续向列表中添加数字，最终将获得一个包含所有数字的排序列表。原始列表在每次迭代中减少一个，我们正在构建的列表在每次迭代中增加一个。对于示例列表，此过程的进度如下所示：

- ( ) ( 8, 2, 5, 3, 10, 7, 1, 4, 6, 9 )
- ( 8 ) ( 2, 5, 3, 10, 7, 1, 4, 6, 9 )
- ( 2, 8 ) ( 5, 3, 10, 7, 1, 4, 6, 9 )
- ( 2, 5, 8 ) ( 3, 10, 7, 1, 4, 6, 9 )
- ( 2, 3, 5, 8 ) ( 10, 7, 1, 4, 6, 9 )
- ( 2, 3, 5, 8, 10 ) ( 7, 1, 4, 6, 9 )
- ( 2, 3, 5, 7, 8, 10 ) ( 1, 4, 6, 9 )
- ( 1, 2, 3, 5, 7, 8, 10 ) ( 4, 6, 9 )
- ( 1, 2, 3, 4, 5, 7, 8, 10 ) ( 6, 9 )
- ( 1, 2, 3, 4, 5, 6, 7, 8, 10 ) ( 9 )
- ( 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ) ( )

