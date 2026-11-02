

## how_to_1/scores.cpp

```cpp
#include <iostream>

using namespace std;

/**
 * Reads a sequence of floating-point numbers.
 * @param inputs an array containing the numbers
 * @param capacity the capacity of that array
 * @return the number of inputs stored in the array
 */
int read_inputs(double inputs[], int capacity)
{
    int current_size = 0;
    cout << "Please enter values, Q to quit:" << endl;
    bool done = false;
    while (!done)
    {
        double input;
        cin >> input;
        if (cin.fail())
        {
            done = true;
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
 * Gets the minimum value from an array.
 * @param values a partially filled array of size >= 1
 * @param size the number of elements in values
 * @return the smallest element in values
 */
double minimum(double values[], int size)
{
    double smallest = values[0];
    for (int i = 1; i < size; i++)
    {
        if (values[i] < smallest)
        {
            smallest = values[i];
        }
    }
    return smallest;
}

/**
 * Computes the sum of the elements in an array.
 * @param values a partially filled array
 * @param size the number of elements in values
 * @return the sum of the elements in values
 */
double sum(double values[], int size)
{
    double total = 0;
    for (int i = 0; i < size; i++)
    {
        total = total + values[i];
    }
    return total;
}

int main()
{
    const int CAPACITY = 1000;
    double scores[CAPACITY];
    int size = read_inputs(scores, CAPACITY);
    if (size == 0)
    {
        cout << "At least one score is required." << endl;
    }
    else
    {
        double final_score = sum(scores, size) - minimum(scores, size);
        cout << "Final score: " << final_score << endl;
    }
    return 0;
}
```

## 示例 6.1
### 掷骰子

学习如何分析一组掷骰子结果，以判断这枚骰子是否“公平”。请查阅你的电子教材，或访问 wiley.com/go/bcl03。

![](img/d61019b035dd82beb581604273c0ee6b_332_0.png)

![](img/d61019b035dd82beb581604273c0ee6b_332_1.png)

## 6.5 问题解决：通过操作实物来发现算法

在 6.4 节中，你了解了如何通过组合和改编已知算法来解决问题。但是，当标准算法都不足以胜任你的任务时，你该怎么办？在本节中，你将学习一种通过操作实物来发现算法的技巧。

考虑以下任务。给定一个大小为偶数的数组，你需要交换前半部分和后半部分。例如，如果数组包含八个数字 9 13 21 4 11 7 1 3，那么你应该将其改为 11 7 1 3 9 13 21 4。

那么我们需要迭代多少次呢？我们需要交换前半部分中的所有“硬币”。也就是说，我们需要交换 size / 2 个硬币。伪代码如下：

```
i = 0
j = size / 2
While i < size / 2
Swap elements at positions i and j
i++
j++
```

你可以使用回形针作为位置标记或计数器。

对伪代码进行一次走查是个好主意（参见 4.2 节）。你可以用回形针来表示变量 i 和 j 的位置。如果走查成功，我们就知道伪代码中没有“差一错误”。练习 E6.6 要求你将这段伪代码翻译成 C++。练习 R6.19 提出了另一种交换数组两半的算法，即通过反复取出和插入硬币来实现。

许多人发现，操作实物不像画图或在脑中想象算法那样令人生畏。当你需要设计新算法时，不妨试一试！

## 6.6 二维数组

你常常需要存储具有二维布局的值集合。这类数据集常见于金融和科学应用中。由若干行和列的值组成的排列称为二维数组，或矩阵。

![](img/d61019b035dd82beb581604273c0ee6b_335_0.png)

让我们来探讨如何存储图 10 中显示的示例数据：2014 年冬季奥运会花样滑冰比赛的奖牌统计。

![](img/d61019b035dd82beb581604273c0ee6b_335_1.png)

| 国家/地区 | 金牌 | 银牌 | 铜牌 |
|---|---|---|---|
| 加拿大 | 0 | 3 | 0 |
| 意大利 | 0 | 0 | 1 |
| 德国 | 0 | 0 | 1 |
| 日本 | 1 | 0 | 0 |
| 哈萨克斯坦 | 0 | 0 | 1 |
| 俄罗斯 | 3 | 1 | 1 |
| 韩国 | 0 | 1 | 0 |
| 美国 | 1 | 0 | 1 |

图 10 花样滑冰奖牌统计

要访问二维数组中的所有值，你需要使用两个嵌套循环。例如，下面的循环输出 counts 的所有元素。

```
for (int i = 0; i < COUNTRIES; i++)
{
    // Process the ith row
    for (int j = 0; j < MEDALS; j++)
    {
        // Process the jth column in the ith row
        cout << setw(8) << counts[i][j];
    }
    cout << endl; // Start a new line at the end of the row
}
```

### 6.6.3 定位相邻元素

某些处理二维数组的程序需要定位与某个元素相邻的元素。这项任务在游戏中尤其常见。图 12 展示了如何计算一个元素的相邻元素的索引值。

例如，counts[3][1] 左侧和右侧的相邻元素分别是 counts[3][0] 和 counts[3][2]，上方和下方的相邻元素分别是 counts[2][1] 和 counts[4][1]。

在计算数组边界处的相邻元素时，你需要格外小心。例如，counts[0][1] 的上方没有相邻元素。考虑计算元素 counts[i][j] 上方和下方相邻元素之和的任务。你需要检查该元素是位于数组的顶部还是底部：

```
int total = 0;
if (i > 0) { total = total + counts[i - 1][j]; }
if (i < ROWS - 1) { total = total + counts[i + 1][j]; }
```

![](img/d61019b035dd82beb581604273c0ee6b_337_0.png)

### 6.6.4 计算行与列的总和

一项常见任务是计算行或列的总和。在我们的示例中，行总计给出了某个特定国家赢得的奖牌总数。

### 6.6.5 二维数组参数

二维数组参数必须具有固定的列数。

在定义带有二维数组参数的函数时，你必须将列数作为常量与参数类型一起指定。例如，下面的函数计算指定行的总和：

```c
const int COLUMNS = 3;

int row_total(int table[][COLUMNS], int row)
{
    int total = 0;
    for (int j = 0; j < COLUMNS; j++)
    {
        total = total + table[row][j];
    }
    return total;
}
```

这个函数可以计算任意行数的二维数组的行总计，但该数组必须恰好有 3 列。如果你想计算 4 列二维数组的行总计，就必须编写一个不同的函数。

要理解这一限制，你需要了解数组元素在内存中是如何存储的。虽然数组看起来是二维的，但元素仍然以线性序列存储。图 13 展示了 counts 数组逐行存储的方式。

![](img/d61019b035dd82beb581604273c0ee6b_339_0.png)

**图 13**  二维数组按行序列存储

例如，若要访问

`counts[3][1]`

程序必须先跳过第 0、1、2 行，然后在第 3 行中定位偏移量 1。该元素相对于数组起始位置的偏移量为

$$3 \times \text{列数} + 1$$

现在来看 row_total 函数。编译器生成代码来查找元素

`table[i][j]`

通过计算偏移量

`i * COLUMNS + j`

编译器使用你在声明参数时在第二对方括号中提供的值：

```c
int row_total(int table[][COLUMNS], int row)
```

请注意，第一对方括号应为空，这与一维数组的情况相同。

