

## 6.2.8 插入元素

如果元素的顺序无关紧要，可以直接在末尾插入新元素，并将记录数组大小的变量加一。（见图 8。）对于部分填充的数组：

```c
if (current_size < CAPACITY)
{
    current_size++;
    values[current_size - 1] = new_element;
}
```

> 插入元素之前，从最后一个元素开始，将元素向数组末尾移动。

在序列中间的特定位置插入元素要复杂一些。首先，增加保存当前大小的变量。接着，将插入位置之后的所有元素移到更大的索引位置。最后，插入新元素。下面是针对部分填充数组的代码：

```c
if (current_size < CAPACITY)
{
    current_size++;
    for (int i = current_size - 1; i > pos; i--)
    {
        values[i] = values[i - 1];
    }
    values[pos] = new_element;
}
```

注意移动元素的顺序：删除元素时，先将下一个元素移到较小的索引位置，再移动后一个元素，依此类推，直到数组末尾。插入元素时，则从数组末尾开始，将该元素移到较大的索引位置，然后移动它前面的元素，依此类推，直到到达插入位置（见图 9）。

![](img/23fb3582e93ebc95909e1de029c3d388_286_0.png)

**图 8**

在无序数组中插入元素

**图 9**

在有序数组中插入元素

## 6.2.9 交换元素

你经常需要交换数组中的元素。例如，第 263 页专题 6.2 中的排序算法，就通过反复交换元素来对数组排序。

**图 10**

交换数组元素

![](img/23fb3582e93ebc95909e1de029c3d388_287_0.png)

考虑交换数组 `values` 中位置 `i` 和 `j` 处元素的任务。我们希望将 `values[i]` 设为 `values[j]`。但这样会覆盖当前存储在 `values[i]` 中的值，因此我们需要先保存它：

![](img/23fb3582e93ebc95909e1de029c3d388_287_1.png)

*要交换两个元素，需要使用一个临时变量。*

交换两个元素时使用临时变量。

```cpp
double temp = values[i];
values[i] = values[j];
```

现在可以将保存的值赋给 `values[j]`。

```cpp
values[j] = temp;
```

图 10 展示了这一过程。

## 6.2.10 读取输入

如果知道用户会提供多少个输入值，就可以轻松地将它们放入数组：

```cpp
double values[NUMBER_OF_INPUTS];
for (i = 0; i < NUMBER_OF_INPUTS; i++)
{
    cin >> values[i];
}
```

不过，如果需要读取数量不定的输入，这种方法就行不通了。这时，可以将输入值逐个添加到数组中，直到到达输入末尾。

```cpp
double values[CAPACITY];
int current_size = 0;
double input;
while (cin >> input)
{
    if (current_size < CAPACITY)
    {
        values[current_size] = input;
        current_size++;
    }
}
```

此时，`values` 是一个部分填充的数组，而配套变量 `current_size` 的值就是输入值的数量。

这个循环会丢弃无法放入数组的输入。更好的方法是在数组容量用尽时，将 `values` 复制到一个更大的新数组中（见第 6.2.2 节）。

下面的程序实现了本章开篇提出的任务：标记输入序列中的最大值：

ch06/largest.cpp

```cpp
#include <iostream>

using namespace std;

int main()
{
    const int CAPACITY = 1000;
    double values[CAPACITY];
    int current_size = 0;

    cout << "Please enter values, Q to quit:" << endl;
    double input;
    while (cin >> input)
    {
        if (current_size < CAPACITY)
        {
            values[current_size] = input;
            current_size++;
        }
    }

    double largest = values[0];
    for (int i = 1; i < current_size; i++)
    {
        if (values[i] > largest)
        {
            largest = values[i];
        }
    }

    for (int i = 0; i < current_size; i++)
    {
        cout << values[i];
        if (values[i] == largest)
        {
            cout << " <== largest value";
        }
        cout << endl;
    }

    return 0;
}
```

## 程序运行

```text
Please enter values, Q to quit:
34.5 80 115 44.5 Q
34.5
80
115 <== largest value
44.5
```

![](img/23fb3582e93ebc95909e1de029c3d388_289_0.png)

- 8. 对于以下输入，`largest.cpp` 程序会输出什么？

  20 10 20 Q

- 9. 编写一个循环，统计数组中有多少个元素等于零。

- 10. 考虑在数组中查找最大元素的算法。为什么我们不将 `largest` 和 `i` 初始化为零，如下所示？

```cpp
double largest = 0;
for (int i = 0; i < size of values; i++)
{
    if (values[i] > largest)
    {
        largest = values[i];
    }
}
```

- 11. 输出分隔符时，我们跳过了初始元素前面的分隔符。请重写循环，使分隔符在每个元素之后输出，但最后一个元素之后除外。

- 12. 使用以下语句输出带分隔符的数组有什么问题？

```cpp
cout << values[0];
for (int i = 1; i < size of values; i++)
{
    cout << ", " << values[i];
}
```

- 13. 查找匹配项时，我们使用了 `while` 循环，而不是 `for` 循环。用下面这个循环有什么问题？

```cpp
for (pos = 0; pos < size of values && !found; pos++)
{
    if (values[pos] == 100)
    {
        found = true;
    }
}
```

- 14. 在数组中插入元素时，我们从末尾开始移动索引较大的元素。为什么不能像下面这样从插入位置开始移动？

```cpp
for (int i = pos; i < size of values - 1; i++)
{
    values[i + 1] = values[i];
}
```

**动手练习** 现在可以尝试本章末尾的这些练习：R6.10、R6.13、P6.6、P6.16。

## 专题 6.1 — 使用 C++ 库排序

![](img/23fb3582e93ebc95909e1de029c3d388_290_0.png)

你经常需要对数组或向量中的元素进行排序。专题 6.2 将介绍一种相对简单但效率不高的排序算法。高效排序算法要复杂得多。幸运的是，C++ 库提供了高效的排序函数。要对含有 `size` 个元素的数组排序，可以调用：

```cpp
sort(a, a + size);
```

要对向量 `values` 排序，可以这样调用：

```cpp
sort(values.begin(), values.end());
```

要完全理解这些调用看似奇特的语法，需要了解本书范围之外的高级 C++ 知识。不过，在需要对数组或向量排序时，不妨直接调用 `sort` 函数。

要使用 `sort` 函数，请在程序中包含 `<algorithm>` 头文件。

## 专题 6.2 — 排序算法

![](img/23fb3582e93ebc95909e1de029c3d388_290_1.png)

*排序算法*会重新排列序列中的元素，使它们按顺序存储。下面介绍一种简单的排序算法，称为**选择排序**。考虑对以下数组 `values` 排序：

![](img/23fb3582e93ebc95909e1de029c3d388_290_2.png)

显而易见的第一步是找出最小元素。本例中，最小元素是 5，存储在 `values[3]` 中。你应该将 5 移到数组开头。当然，`values[0]` 中已经存储了一个元素，即 11。因此，不能直接将 `values[3]` 移到 `values[0]`，否则就得先把 11 移到别处。虽然你不知道 11 最终应该放在哪里，但可以确定它不该留在 `values[0]` 中。只需先把它移开：将它与 `values[3]` 交换即可：

![](img/23fb3582e93ebc95909e1de029c3d388_290_3.png)

现在第一个元素已经处于正确位置。在上图中，较深的颜色表示数组中已经排好序的部分。

接下来，从剩余元素 `values[1]`……`values[4]` 中找出最小值。这个最小值 9 已经处于正确位置，因此无需进行任何操作，只需将已排序区域向右扩展一格：

![](img/23fb3582e93ebc95909e1de029c3d388_290_4.png)

继续重复这一过程。未排序区域中的最小值是 11，需要将它与未排序区域的第一个值交换：

![](img/23fb3582e93ebc95909e1de029c3d388_290_5.png)

