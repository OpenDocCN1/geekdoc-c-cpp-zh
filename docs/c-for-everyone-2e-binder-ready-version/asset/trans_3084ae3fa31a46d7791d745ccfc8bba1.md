
### 6.2.8 插入元素

如果元素的顺序无关紧要，你可以直接在末尾插入新元素，并递增用于跟踪大小的变量。（参见图 8。）对于部分填充的数组：

```cpp
if (current_size < CAPACITY)
{
    current_size++;
    values[current_size - 1] = new_element;
}
```

在序列中间某个特定位置插入元素要做的工作更多。首先，增加保存当前大小的变量。接着，将插入位置之上的所有元素移到更高的索引。最后，插入新元素。以下是部分填充数组的代码：

> 插入元素之前，从最后一个元素开始，将元素移到数组末尾。

```cpp
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

注意移动的顺序：删除元素时，你先将下一个元素下移到更低的索引，然后移动再下一个元素，直到最终到达数组末尾。插入元素时，你从数组末尾开始，将该元素移到更高的索引，然后移动它前面的元素，依此类推，直到最终到达插入位置（参见图 9）。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_286_0.png)

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_286_1.png)

### 6.2.9 交换元素

你经常需要交换数组中的元素。例如，第 263 页专题 6.2 中的排序算法通过反复交换元素来对数组排序。

**图 10**
交换数组元素

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_287_0.png)

考虑交换数组 `values` 中位置 `i` 和 `j` 处元素的任务。我们希望将 `values[i]` 设为 `values[j]`。但那样会覆盖当前存储在 `values[i]` 中的值，所以我们要先保存它：

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_287_1.png)

> 交换两个元素时使用临时变量。

```cpp
double temp = values[i];
values[i] = values[j];
```

现在我们可以将 `values[j]` 设为保存的值。

```cpp
values[j] = temp;
```

图 10 展示了这一过程。

*要交换两个元素，你需要一个临时变量。*

### 6.2.10 读取输入

如果你知道用户将提供多少个输入值，将它们放入数组就很简单：

```cpp
double values[NUMBER_OF_INPUTS];
for (i = 0; i < NUMBER_OF_INPUTS; i++)
{
   cin >> values[i];
}
```

```cpp
36        cout << " <== largest value";
37    }
38    cout << endl;
39  }
40 }
41    return 0;
42 }
```

## 程序运行

```
Please enter values, Q to quit:
34 5 80 115 44.5 Q
34 5
80
115 <== largest value
44.5
```

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_289_0.png)

- 8. 在以下输入下，largest.cpp 程序的输出是什么？

    ```
    20 10 20 Q
    ```

- 9. 编写一个循环，统计数组中有多少个元素等于零。

- 10. 考虑在数组中查找最大元素的算法。为什么我们不把 largest 和 i 初始化为零，像这样？

    ```cpp
    double largest = 0;
    for (int i = 0; i < size; i++)
    {
       if (values[i] > largest)
       {
          largest = values[i];
       }
    }
    ```

- 11. 打印分隔符时，我们跳过了第一个元素前的分隔符。请重写循环，使每个元素之后都打印分隔符，但最后一个元素除外。

- 12. 下面这些用于打印带分隔符的数组的语句有什么问题？

    ```cpp
    cout << values[0];
    for (int i = 1; i < size; i++)
    {
       cout << ", " << values[i];
    }
    ```

- 13. 搜索匹配项时，我们使用的是 while 循环，而不是 for 循环。改用下面这个循环有什么问题？

    ```cpp
    for (pos = 0; pos < size && !found; pos++)
    {
       if (values[pos] == 100)
       {
          found = true;
       }
    }
    ```

- 14. 向数组中插入元素时，我们从末尾开始移动索引值较大的元素。为什么像下面这样从插入位置开始是错误的：

数组参数始终是引用参数。

数组参数*始终是引用参数*。（你将在第 7 章看到原因。）函数可以修改数组实参，而这些修改会影响传入函数的数组。例如，下面的 multiply 函数会更新数组中的所有元素：

```cpp
void multiply(double values[], int size, double factor)
{
    for (int i = 0; i < size; i++)
    {
        values[i] = values[i] * factor;
    }
}
```

在这种情况下，你*不*使用 & 符号来表示引用参数。

虽然数组可以作为函数参数，但它们不能作为函数返回类型。如果函数计算多个值，函数的调用者必须提供一个数组参数变量来保存结果。

函数的返回类型不能是数组。

```cpp
void squares(int n, int result[])
{
    for (int i = 0; i < n; i++)
    {
        result[i] = i * i;
    }
}
```

当函数改变数组的大小时，它应当告知调用者在调用之后数组有多少个元素。最简单的方法是返回新的大小。下面是一个例子——一个将输入值添加到数组中的函数：

当函数修改数组的大小时，它需要告诉调用者。

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

注意，这个函数还需要知道数组的容量。通常，向数组添加元素的函数需要知道其容量。你会这样调用这个函数：

```cpp
const int MAXIMUM_NUMBER_OF_VALUES = 1000;
double values[MAXIMUM_NUMBER_OF_VALUES];
int current_size = read_inputs(values, MAXIMUM_NUMBER_OF_VALUES);
// values is a partially filled array; the current_size variable specifies its size
```

向数组添加元素的函数需要知道其容量。

或者，你可以将大小作为引用参数传递。这对于修改现有数组的函数更合适：

```cpp
void append_inputs(double inputs[], int capacity, int& current_size)
{
    double input;
    while (cin >> input)
    {
        if (current_size < capacity)
        {
            inputs[current_size] = input;
            current_size++;
        }
    }
}
```

这个函数的调用方式如下：

```cpp
append_inputs(values, MAXIMUM_NUMBER_OF_VALUES, current_size);
```

调用之后，current_size 变量包含新的大小。

下面的示例程序从标准输入读取值，将它们翻倍，并打印结果。该程序使用了三个函数：

- read_inputs 函数用输入值填充数组。它返回读取到的元素个数。
- multiply 函数修改它接收到的数组内容，这演示了数组是按引用传递的。
- print 函数不修改它接收到的数组内容。

## ch06/functions.cpp

```cpp
#include <iostream>

using namespace std;

/**
   Reads a sequence of floating-point numbers.
   @param inputs an array containing the numbers
   @param capacity the capacity of that array
   @return the number of inputs stored in the array
*/
int read_inputs(double inputs[], int capacity)
{
   int current_size = 0;
   cout << "Please enter values, Q to quit:" << endl;
   bool more = true;
   while (more)
   {
      double input;
      cin >> input;
      if (cin.fail())
      {
         more = false;
      }
      else if (current_size < capacity)
      {
         inputs[current_size] = input;
         current_size++;
      }
   }
   return current_size;
}

/**
   Multiplies all elements of an array by a factor.
   @param values a partially filled array
   @param size the number of elements in values
```
