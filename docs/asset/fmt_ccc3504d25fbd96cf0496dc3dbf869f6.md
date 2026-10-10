
当永远无法边界边界时就会发生无限递归。例如，如果一个函数在没有任何边界情况的情况下调用自身，它将永远执行（直到栈溢出）。设计递归函数时你必须执行以下操作：

a. 理解问题需求。

b. 确定限制。

c. 识别边界情况并提供解决方案。

d. 识别一般情况并提供解决方案。

# 使用递归解决问题

示例 17-1 到 17-3 阐述了如何在 `C++` 中开发和实现递归算法。

## 示例 17-1 数组最大元素

在第 9 章中，我们使用循环查找数组中的最大元素。在这个示例中，我们使用递归算法来查找数组中的最大元素。考虑图 17-2 中的列表。

| [0] | [1] | [2] | [3] | [4] | [5] |
|---|---|---|---|---|---|

| list | 5 | 8 | 2 | 10 | 9 | 4 |

图 17-2 有六个元素的列表

图 17-2 中列表的最大元素是 10。

假设 `list` 是数组名称。同样，假设 `list[a]...list[b]` 代表数组元素 `list[a]`, `list[a + 1]`, ..., `list[b]`。例如，`list[0]...list[5]` 代表数组元素 `list[0]`, `list[1]`, `list[2]`, `list[3]`, `list[4]`, 和 `list[5]`。同样，`list[1]...list[5]` 代表数组元素 `list[1]`, `list[2]`, `list[3]`, `list[4]`, 和 `list[5]`。

为了编写一个在列表中查找最大元素的递归算法，让我们从递归的角度考虑。

如果列表长度为 1，那么列表只有一个元素，它就是最大元素。列表长度大于 1。为了找到 `list[a]...list[b]` 中的最大元素，我们首先找到 `list[a + 1]...list[b]` 中的最大元素，然后将其最大元素与 `list[a]` 进行比较。因此，`list[a]...list[b]` 中的最大元素由以下给出：

```
maximum(list[a], largest(list[a + 1]...list[b]))
```

也就是说，列表中的……元素是 `list[0]` 和 `list[1]...list[5]` 中最大元素的较大值。为了找到 `list[1]...list[5]` 中的最大元素，我们再次使用相同的公式，因为这个列表的长度大于 1。`list[1]...list[5]` 中的最大元素是：

```
maximum(list[1], largest(list[2]...list[5]))
```

依此类推。我们看到，每当我们使用前一个公式找到子列表中的最大元素时，下一次调用中子列表的长度就会减少 1。最终，子列表的长度为 1，此时子列表只包含一个元素，该元素就是该子列表中的最大元素。从这一点开始，我们通过递归调用进行回溯。这一讨论可以转化为以下伪代码

**基础情况（Base Case）：** 列表的大小为 1

列表中的唯一元素就是最大元素

**一般情况（General Case）：** 列表的大小大于 1

要找到 `list[a]...list[b]` 中的最大元素

- 找到 `list[a + 1]...list[b]` 中的最大元素

  并将其称为 `max`

- 比较元素 `list[a]` 和 `max`

  if (`list[a]` >= `max`)

    `list[a]...list[b]` 中的最大元素是 `a`

  否则

    `list[a]...list[b]` 中的最大元素是 `max`

该算法可以转化为以下 `C++` 函数，用于找到数组中的最大元素：

```cpp
int largest(const int list[], int lowerIndex, int upperIndex)
{
  int max;
  if (lowerIndex == upperIndex) //子列表的大小为一
    return list[lowerIndex];
  else
    max = largest(list, lowerIndex + 1, upperIndex);
    if (list[lowerIndex] >= max)
      return list[lowerIndex];
    else
      return max;
}
```

考虑图 17-3 所示的列表。

| [0] | [1] | [2] | [3] |
| :--- | :--- | :--- | :--- |
| list | 5 | 10 | 12 | 8 |

图 17-3 具有四个元素的列表

让我们跟踪以下语句的执行：

```cpp
cout << largest(list, 0, 3) << endl;
```

这里，`upperIndex = 3` 列表有四个元素。图 17-4 跟踪了 `largest(list, 0, 3)` 的执行。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1038_0.png)

图 17-4 `largest(list, 0, 3)` 的执行

表达式 `largest(list, 0, 3)` 返回值为 12，它是列表中的最大元素。

以下 `C++` 程序使用 `largest` 函数来确定列表中的最大元素。

# //数组中的最大元素

```cpp
#include <iostream>

using namespace std;

int largest(const int list[], int lowerIndex, int upperIndex);
int main() {
    int intArray[10] = {23, 43, 35, 38, 67, 12, 76, 10, 34, 88};
    cout << "The largest element in intArray: ";
    cout << largest(intArray, 0, 9);
    cout << endl;
    return 0;
}

int largest(const int list[], int lowerIndex, int upperIndex) {
    int max;
    if (lowerIndex == upperIndex) //子列表的大小为一
        return list[lowerIndex];
    else {
        max = largest(list, lowerIndex + 1, upperIndex);
        if (list[lowerIndex] >= max)
            return list[lowerIndex];
        else
            return max;
    }
}
```

示例运行：

The largest element in intArray: 76

## 示例 17-2：斐波那契数

在第 5 章中，我们设计了一个程序来确定指定的斐波那契数。在本中，我们写了一个递归函数 `rFibNum` 来确定指定的斐波那契数。函数 `rFibNum` 的参数代表斐波那契序列的前两个数以及一个代表所需的第 $n$ 个斐波那契数的 $n$。函数 `rFibNum` 返回序列中的第 $n$ 个斐波那契数。

回第三个斐波那契数是前两个斐波那契数的和。序列中的第四个斐波那契数是第二个和第三个斐波那契数的和。因此，为了计算第四个斐波那契数，我们将第二个斐波那契数加上第三个斐波那契数（本身本身前两个斐波那契数的和）。以下递归算法计算第 $n$ 个斐波那契数，其中 $a$ 表示第一个斐波那契数，$b$ 表示第二个斐波那契数，$n$ 表示第 $n$ 个斐波那契数。

```
rFibNum(a,b) = \begin{cases} a & \text{如果 } n=1 \\ b & \text{如果 } n=2 \\ rFibNum(a,n-1) + rFibNum(a,n-2) & \text{如果 } n>2 \end{cases} \quad (17-3)
```

假设我们想要确定：

`rFibNum(2, 5, 4)`

这里，$a=2, b=5$， 且 $n=4$。也就是说，我们想要确定第一个数字为 2，第二个数字为 5 的序列的第四个斐波那契数。因为 $n>2$：

1. `rFibNum(2, 5, 4) = rFibNum(2, 5, 3) + rFibNum(2, 5, 2)`

接下来我们要确定 `rFibNum(2, 5, 3)` 和 `rFibNum(2, 5, 2)`。这里，$a=2, b=5$， 且 $n=3$。因为 $n>2$：

1. `rFibNum(2, 5, 3) = rFibNum(2, 5, 2) + rFibNum(2, 5, 1)`

接下来我们要确定 `rFibNum(2, 5, 2)` 和 `rFibNum(2, 5, 1)`。这里，$a=2, b=5$， 且 $n=2$。根据定义：

`rFibNum(2, 5, 2) = 5`

所以：

1. `rFibNum(2, 5, 3) = 5 + rFibNum(2, 5, 1)`

接下来我们要确定 `rFibNum(2, 5, 1)`。这里，$a=2, b=5$， 且 $n=1$。根据定义：

`rFibNum(2, 5, 1) = 2`

所以：

1. `rFibNum(2, 5, 3) = 5 + 2 = 7`

最后：

1. `rFibNum(2, 5, 4) = 7 + 5 = 12`

像之前一样，从递归的角度来思考。让我们首先考虑第一个针子上只有一个盘的情况。在这种情况下，该盘可以直接从 `needle1` 移动到 `needle3`。接着，考虑第一个针子上有两个盘的情况。在这种情况下，我们将第一个盘从 `needle1` 移动到 `needle2`，然后将第二个盘从 `needle1` 移动到 `needle3`。接下来，我们考虑第一个针子上有三个盘的情况，并推广到 64 个盘（实际上是任意数量的盘）。

假设针子上有三个盘。要将第 3 号盘移动到 `needle2`，两个盘必须先移动到 `needle1`，然后将第 3 号盘从 `needle1` 移动到 `needle3`。要将剩下的两个盘从 `needle2` 移动到 `needle3`，我们使用与相同的策略。这一次，我们使用 `needle1` 作为中间针子。图 17-7 显示了三个盘汉诺塔问题的解决方案。![](img/abc25bb50ebb3eb05460d88ce0e0fde1044_0.png) 图 17-7 三个盘的汉诺塔问题

# 使用递归解决问题

现在我们将此问题推广到 64 个盘的情况。首先，第一个针子上有 64 个盘。除非第二个针子上有 63 个盘，否则第 64 号盘无法从 `needle1` 移动。因此，我们将前 63 个盘从 `needle1` 移动到 `needle2`，然后将第 64 号盘从 `needle1` 移动到 `needle3`。现在第二个针子上有 63 个盘。要将第 63 号盘从 `needle2` 移动到 `needle3`，我们将前 62 个盘从 `needle2` 移动到 `needle1`，然后将第 63 号盘从 `needle2` 移动到 `needle3`。这种讨论转化为以下递归算法，假设针子上有 $n$ 个盘（$n \ge 1$）：

1. 使用 `needle3` 作为中间针子，将 $n-1$ 个盘从 `needle1` 移动到 `needle2`。

2. 将第 $n$ 号盘从 `needle1` 移动到 `needle3`。

3. 使用 `needle1` 作为中间针子，将 $n-1$ 个盘从 `needle2` 移动到 `needle3`。

此递归算法转化为以下 `C++` 函数：

```cpp
void moveDis(int count, int needle1, int needle2, int needle3) {
  if (count > 0) {
    moveDis(count - 1, needle1, needle3, needle2);
    cout << "Move " << count << " from " << needle1 
         << " to " << needle3 << endl;
    moveDis(count - 1, needle2, needle1);
  }
}
```

# 汉诺塔分析

让我们确定将 64 个盘从 `needle1` 移动到 `needle3` 需要多久。如果第一个针子上有 3 个盘，将三个盘从 `needle1` 移动到 `needle3` 需要的移动次数为 $2^3-1 = 7$。同样，如果第一个针子上有 64 个盘，将 64 个盘从 `needle1` 移动到 `needle3` 需要的移动次数为 $2^{64}-1$。因为 $2^{10} = 1024 \approx 10^3$，我们得到：

$2^{64} = 2^4 \times 2^{60} \approx 16 \times (10^3)^6 = 1.6 \times 10^{19}$

一年的秒约为 $3.2 \times 10^7$。如果每秒移动一次且不休息：

$1.6 \times 10^{19} = 5 \times 3.2 \times 10^{18} = 5 \times (3.2 \times 10^7) \times 10^{11} = (3.2 \times 10^7) \times (5 \times 10^{11})$

将 64 个盘从 `needle1` 移动到 `needle3` 需要的时间大约是 $5 \times 10^{11}$ 年。据估计，我们的宇宙约为 150 亿年（$1.5 \times 10^{10}$ 年）。此外，$5 \times 10^{11} = 50 \times 10^{10} \approx 33 \times (1.5 \times 10^{10})$。这个计算表明，宇宙的寿命将比现在长 33 倍。

假设计算机每秒可以产生 10 亿（$10^9$）次移动。那么计算机一年内可以产生的移动次数为：

$(3.2 \times 10^7) \times 10^9 = 3.2 \times 10^{16}$

所以将 64 个盘从 `needle1` 移动到 `needle3` 需要的时间大约是 $5 \times 10^{11}$ 年。据估计，我们的宇宙约为 150 亿年（$1.5 \times 10^{10}$ 年）。此外，$5 \times 10^{11} = 50 \times 10^{10} \approx 33 \times (1.5 \times 10^{10})$。这个计算表明，宇宙的寿命将比现在长 33 倍。

为了编写一个将二进制数转换为等效十进制数的程序，我们注意到两点：(1) 必须知道二进制数中每个位的权重，(2) 权重是从右到左分配的。由于我们预先不知道二进制数中有多少位，因此必须从右到左处理这些位。处理完一个位后，我们可以将其权重加 1，即其紧邻左侧位的权重。此外，每个位都必须通过乘以 2 的权次幂从二进制数中提取出来。要提取一个位，我们可以使用模运算符。以下是用伪代码给出的递归算法。

```
if (binaryNumber > 0) {
  bit = binaryNumber % 10; //提取最右位
  decimal = decimal + bit * power(2, weight);
  binaryNumber = binaryNumber / 10; //移除最右位
}
weight++;
convert binaryNumber into decimal
```

该算法假设内存位置 `decimal` 和 `weight` 已经初始化为 0。该算法转换为以下 `C++` 递归函数：

```cpp
void binToDec(int binaryNumber, int& decimal, int& weight) {
  int bit;
  if (binaryNumber > 0) {
    bit = binaryNumber % 10;
    decimal += bit * static_cast<int>(pow(2.0, weight));
    binaryNumber = binaryNumber / 10;
    weight++;
    binToDec(binaryNumber, decimal, weight);
  }
}
```

在这个函数中，`decimal` 和 `weight` 都是引用参数。实际参数被初始化为 0。在提取最右位后，该函数更新十进制数和下一个位的权重。假设 `decimalNumber` 和 `bitWeight` 是变量。考虑以下语句：

```cpp
decimalNumber = 0;
bitWeight = 0;
binToDec(1101, decimal, weight);
```

图 17-8 追踪了最后一条语句 `binToDec(1101, decimal, weight)` 的执行过程，它显示了在每次函数调用时变量 `decimalNumber` 和 `weight` 的内容。

## 编程示例：二进制转十进制

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1049_0.png)

图 17-8 `binToDec(1101, decimal, weight)` 的执行。在图 17-8 中，每个箭头代表连续的函数调用。因为 `binToDec` 函数的最后语句是一个函数调用，在该语句执行后什么都没有发生。语句 `binToDec(1101, decimal, weight)` 执行后，变量 `decimal` 的值为 1。

以下 `C++` 程序测试了 `binToDec` 函数：
