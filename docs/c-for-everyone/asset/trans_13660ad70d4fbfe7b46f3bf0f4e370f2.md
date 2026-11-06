
```cpp
36      cout << " <= largest value";
37    }
38    cout << endl;
39  }
40
41    return 0;
42 }
```

## 程序运行

```text
Please enter values, Q to quit:
34.5 80 115 44.5 Q
34.5
80
115 <= largest value
44.5
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_289_0.png)

## 自测题

- 8. 使用以下输入时，largest.cpp 程序的输出是什么？

    ```text
    20 10 20 Q
    ```

- 9. 编写一个循环，统计数组中等于零的元素个数。

- 10. 考虑在数组中查找最大元素的算法。为什么我们不将 largest 和 i 初始化为零，像这样：

    ```cpp
    double largest = 0;
    for (int i = 0; i < values.size(); i++)
    {
        if (values[i] > largest)
        {
            largest = values[i];
        }
    }
    ```

- 11. 打印分隔符时，我们跳过了初始元素之前的分隔符。重写循环，使分隔符在每个元素之后打印，但最后一个元素除外。

- 12. 下面这些用于打印带分隔符数组的语句有什么问题？

    ```cpp
    cout << values[0];
    for (int i = 1; i < values.size(); i++)
    {
        cout << ", " << values[i];
    }
    ```

- 13. 搜索匹配项时，我们使用了 while 循环，而不是 for 循环。改用下面这个循环有什么问题？

    ```cpp
    for (pos = 0; pos < values.size() && !found; pos++)
    {
        if (values[pos] == 100)
        {
            found = true;
        }
    }
    ```

- 14. 向数组中插入元素时，我们从末尾开始移动索引值较大的元素。为什么从插入位置开始（像下面这样）是错误的：

    ```cpp
    for (int i = pos; i < values.size() - 1; i++)
        values[i + 1] = values[i];
    ```

**练习一下** 现在你可以尝试本章末尾的这些练习：R6.10、R6.13、P6.6、P6.16。

## 专题 6.1

![](img/5e58fb4c840712efd6ed6fa82bb97f57_290_0.png)

### 使用 C++ 库排序

你经常需要对数组或向量的元素进行排序。专题 6.2 向你展示了一种相对简单但效率不高的排序算法。高效的排序算法要复杂得多。幸运的是，C++ 库提供了一个高效的 sort 函数。

要对含有 size 个元素的数组进行排序，请调用

```cpp
sort(a, a + size);
```

要对向量 values 进行排序，请这样调用：

```cpp
sort(values.begin(), values.end());
```

要完全理解这些调用的奇特语法，你需要了解超出本书范围的高级 C++ 知识。但无论何时需要排序数组或向量，都不要犹豫，直接调用 sort 函数。

要使用 sort 函数，请在程序中包含 `<algorithm>` 头文件。

## 专题 6.2

![](img/5e58fb4c840712efd6ed6fa82bb97f57_290_1.png)

### 一种排序算法

*排序算法*会重新排列序列中的元素，使它们按排序后的顺序存储。这里有一种简单的排序算法，称为选择排序。考虑对以下数组 values 进行排序：

![](img/5e58fb4c840712efd6ed6fa82bb97f57_290_2.png)

显而易见的第一步是找到最小元素。在这个例子中，最小元素是 5，存储在 values[3] 中。你应该将 5 移到数组开头。当然，values[0] 中已经存储了一个元素，即 11。因此，你不能简单地把 values[3] 移到 values[0] 中，而不把 11 移到别处。你还不知道 11 最终应该放在哪里，但你确信它不应该在 values[0] 中。只需通过将它与 values[3] *交换*来把它移开：

![](img/5e58fb4c840712efd6ed6fa82bb97f57_290_3.png)

现在第一个元素已在正确位置。在上图中，较深的颜色表示数组中已经排好序的部分。

接下来取剩余条目 values[1] . . . values[4] 中的最小值。那个最小值 9 已经在正确位置。在这种情况下你不需要做任何事，只需将已排序区域向右扩展一个位置：

![](img/5e58fb4c840712efd6ed6fa82bb97f57_290_4.png)

重复这个过程。未排序区域的最小值是 11，需要将其与未排序区域的第一个值 17 交换：

![](img/5e58fb4c840712efd6ed6fa82bb97f57_290_5.png)

我们仍然没有找到匹配项，因为 15 ≠ 17，而且我们无法进一步划分该子序列。如果我们想把 15 插入序列中，就需要把它插入到 `values[5]` 之前。

这个搜索过程称为**二分搜索**，因为我们在每一步都将搜索规模减半。这种减半之所以有效，只是因为我们知道数值序列已经排序。下面是 C++ 中的实现。

```cpp
bool found = false;
int low = 0;
int high = size - 1;
int pos = 0;
while (low <= high && !found)
{
    pos = (low + high) / 2; // Midpoint of the subsequence
    if (values[pos] == searched_value) { found = true; }
    else if (values[pos] < searched_value) { low = pos + 1; } // Look in second half
    else { high = pos - 1; } // Look in first half
}
if (found) { cout << "Found at position " << pos; }
else { cout << "Not found. Insert before position " << pos; }
```

## 6.3 数组与函数

向函数传递数组时，也要传递数组的大小。

在本节中，我们将探讨如何编写处理数组的函数。

处理数组中值的函数需要知道数组中有效元素的数量。例如，下面是一个计算数组中所有元素之和的 sum 函数：

```cpp
double sum(double values[], int size)
{
    double total = 0;
    for (int i = 0; i < size; i++)
    {
        total = total + values[i];
    }
    return total;
}
```

注意数组参数变量的特殊语法。编写数组参数变量时，在参数名后放一个空的 []。不要在方括号内指定数组大小。

调用函数时，同时提供数组名和大小。例如，

```cpp
const int NUMBER_OF_SCORES = 10;
double scores[NUMBER_OF_SCORES]
    = { 32, 54, 67.5, 29, 34.5, 80, 115, 44.5, 100, 65 };
double total_score = sum(scores, NUMBER_OF_SCORES);
```

你也可以向函数传递较小的大小：

```cpp
double partial_score = sum(scores, 5);
```

这个调用计算 scores 数组前五个元素的和。记住，函数无法知道数组有多少个元素。它只依赖调用者提供的大小。

> 数组参数始终是引用参数。

数组参数*始终是引用参数*。（你将在第 7 章看到原因。）函数可以修改数组实参；这些修改会影响传入函数的数组。例如，下面的 `multiply` 函数会更新数组中的所有元素：

```cpp
void multiply(double values[], int size, double factor)
{
    for (int i = 0; i < size; i++)
    {
        values[i] = values[i] * factor;
    }
}
```

在这种情况下，你*不要*使用 `&` 符号来表示引用参数。

> 函数的返回类型不能是数组。

尽管数组可以作为函数参数，但它们不能作为函数返回类型。如果函数计算多个值，函数的调用者必须提供一个数组参数变量来保存结果。

```cpp
void squares(int n, int result[])
{
    for (int i = 0; i < n; i++)
    {
        result[i] = i * i;
    }
}
```

> 当函数修改数组的大小时，它需要告诉调用者。

当函数改变数组的大小时，它应该向调用者指出调用后数组有多少个元素。最简单的方法是返回新的大小。下面是一个例子——一个将输入值添加到数组的函数：

```cpp
int read_inputs(double inputs[], int capacity)
{
    int current_size = 0;
    double input;
    while (cin >> input)
    {
        if (current_size < capacity)
        {
            inputs[current_size] = input;
            current_size++;
        }
    }
    return current_size;
}
```

> 向数组添加元素的函数需要知道其容量。

注意，这个函数还需要知道数组的容量。通常，向数组添加元素的函数需要知道其容量。你会这样调用这个函数：

```cpp
const int MAXIMUM_NUMBER_OF_VALUES = 1000;
double values[MAXIMUM_NUMBER_OF_VALUES];
int current_size = read_inputs(values, MAXIMUM_NUMBER_OF_VALUES);
// values is a partially filled array; the current_size variable specifies its size
```

或者，你可以将大小作为引用参数传递。这对于修改现有数组的函数更合适：

```cpp
void append_inputs(double inputs[], int capacity, int& current_size)
{
    double input;
    while (cin >> input)
    {

