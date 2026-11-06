

## 6.2 常见数组算法

在接下来的章节中，我们将讨论处理值序列的一些最常见算法。我们给出这些算法，以便你可以将它们用于完全填充和部分填充的数组以及向量（我们将在第 6.7 节中介绍）。当我们使用表达式 size of values 时，你应该用一个常量或变量来替换它，该常量或变量给出数组中的元素数量（如果 values 是向量，则为表达式 values.size()）。

### 6.2.1 填充

这个循环用零填充数组：

```cpp
for (int i = 0; i < size of values; i++)
{
    values[i] = 0;
}
```

接下来，让我们用数字 0, 1, 4, 9, 16 等填充数组 squares。注意索引为 0 的元素包含 0²，索引为 1 的元素包含 1²，以此类推。

```cpp
for (int i = 0; i < size of squares; i++)
{
    squares[i] = i * i;
}
```

### 6.2.2 复制

> 要复制数组，请使用循环将其元素复制到新数组。

考虑两个数组：

```cpp
int squares[5] = { 0, 1, 4, 9, 16 };
int lucky_numbers[5];
```

现在假设你想将第一个数组中的所有值复制到第二个数组。下面的赋值是错误的：

```cpp
lucky_numbers = squares; // Error
```

在 C++ 中，不能将一个数组赋值给另一个数组。相反，你必须使用循环来复制所有元素：

```cpp
for (int i = 0; i < 5; i++)
{
    lucky_numbers[i] = squares[i];
}
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_283_0.png)

**图 5** 复制元素以复制数组

### 6.2.3 求和与平均值

你已经在第 4.7.1 节中遇到过这个算法。以下是计算数组中所有元素总和的代码：

```cpp
double total = 0;
for (int i = 0; i < size of values; i++)
{
    total = total + values[i];
}
```

要获得平均值，请除以元素数量：

```cpp
double average = total / size of values;
```

请务必检查 size 不为零。

### 6.2.4 最大值和最小值

使用第 4.7.4 节中的算法，该算法保留一个变量来记录到目前为止遇到的最大元素。以下是数组的实现：

```cpp
double largest = values[0];
for (int i = 1; i < size of values; i++)
{
    if (values[i] > largest)
    {
        largest = values[i];
    }
}
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_284_0.png)

注意循环从 1 开始，因为我们用 values[0] 初始化 largest。要计算最小值，反转比较。这些算法要求数组至少包含一个元素。

### 6.2.5 元素分隔符

> 分隔元素时，不要在第一个元素前放置分隔符。

当你显示集合的元素时，通常希望用逗号或竖线分隔它们，例如：

`1 | 4 | 9 | 16 | 25`

注意分隔符比数字少一个。在每个元素*除了第一个元素*（索引为 0）之前打印分隔符：

```cpp
for (int i = 0; i < size of values; i++)
{
    if (i > 0)
    {
        cout << " | ";
    }
    cout << values[i];
}
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_284_1.png)

### 6.2.6 线性搜索

线性搜索按顺序检查元素，直到找到匹配项。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_285_0.png)

要搜索特定元素，依次访问元素，遇到匹配时停止。

你经常需要搜索元素的位置，以便替换或删除它。访问所有元素，直到找到匹配项或到达数组末尾。这里我们搜索第一个等于 100 的元素的位置。

```cpp
int pos = 0;
bool found = false;
while (pos < size of values && !found)
{
   if (values[pos] == 100)
   {
      found = true;
   }
   else
   {
      pos++;
   }
}
```

如果 found 为真，则 pos 是第一个匹配项的位置。

### 6.2.7 删除元素

考虑一个部分填充的数组 values，其当前大小存储在变量 current_size 中。假设你想从 values 中删除索引为 pos 的元素。如果元素的顺序不重要，这个任务很容易完成。只需用最后一个元素覆盖要删除的元素，然后递减跟踪大小的变量。（见图 6。）

```cpp
values[pos] = values[current_size - 1];
current_size--;
```

如果元素的顺序很重要，情况就更复杂了。然后你必须将要删除的元素之后的所有元素移动到一个较低的索引，然后递减保存数组大小的变量。（见图 7。）

```cpp
for (int i = pos + 1; i < current_size; i++)
{
   values[i - 1] = values[i];
}
current_size--;
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_285_1.png)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_285_2.png)

### 6.2.8 插入元素

如果元素的顺序不重要，你可以简单地在末尾插入新元素，递增跟踪大小的变量。（见图 8。）对于部分填充的数组：

在插入元素之前，从最后一个元素开始，将元素向数组末尾移动。

```cpp
if (current_size < CAPACITY)
{
    current_size++;
    values[current_size - 1] = new_element;
}
```

在序列中间的特定位置插入元素需要更多工作。首先，递增保存当前大小的变量。接下来，将所有位于插入位置之上的元素移动到一个更高的索引。最后，插入新元素。以下是部分填充数组的代码：

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

注意移动的顺序：当你删除元素时，你首先将下一个元素向下移动到一个较低的索引，然后是后面的元素，直到你最终到达数组末尾。当你插入元素时，你从数组末尾开始，将该元素移动到一个较高的索引，然后移动它前面的元素，依此类推，直到你最终到达插入位置（见图 9）。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_286_0.png)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_286_1.png)

### 6.2.9 交换元素

你经常需要交换数组的元素。例如，第 263 页专题 6.2 中的排序算法通过反复交换元素来对数组排序。

**图 10**  
交换数组元素

![](img/5e58fb4c840712efd6ed6fa82bb97f57_287_0.png)

考虑交换数组 `values` 中位置 *i* 和 *j* 的元素的任务。我们希望将 `values[i]` 设置为 `values[j]`。但这会覆盖当前存储在 `values[i]` 中的值，所以我们要先保存它：

```cpp
double temp = values[i];
values[i] = values[j];
```

现在我们可以将 `values[j]` 设置为保存的值。

```cpp
values[j] = temp;
```

图 10 展示了该过程。

交换两个元素时使用临时变量。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_287_1.png)

*要交换两个元素，你需要一个临时变量。*

### 6.2.10 读取输入

如果你知道用户将提供多少个输入值，将它们放入数组很简单：

```cpp
double values[NUMBER_OF_INPUTS];
for (i = 0; i < NUMBER_OF_INPUTS; i++)
{
    cin >> values[i];
}
```

但是，如果需要读取任意数量的输入，这种技术就不起作用。在这种情况下，将值添加到数组中，直到到达输入的末尾。

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

现在 values 是一个部分填充的数组，伴随变量 current_size 设置为输入值的数量。

这个循环会丢弃任何不适合数组的输入。更好的方法是在达到容量时将 values 复制到一个新的更大的数组（见 6.2.2 节）。下面的程序解决了我们在本章开头设定的任务，即标记输入序列中的最大值。

# ch06/largest.cpp

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

```

