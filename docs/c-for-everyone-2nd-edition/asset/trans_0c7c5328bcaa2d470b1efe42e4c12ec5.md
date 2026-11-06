
## 操作指南 4.1 编写循环

本操作指南将引导你完成实现循环语句的过程。我们将通过以下示例问题来说明这些步骤：

读取十二个温度值（每个月一个），并显示最高温度所在月份的编号。例如，根据 http://worldclimate.com 的数据，死亡谷的平均最高温度（按月顺序）为：

18.2  22.6  26.4  31.1  36.6  42.2  
45.7  44.5  40.2  33.1  24.2  17.6

在这种情况下，最高温度（45.7 摄氏度）对应的月份是七月，程序应显示 7。

![](img/23fb3582e93ebc95909e1de029c3d388_189_0.png)

**第 1 步** 确定必须在循环*内部*完成的工作。

每个循环都需要执行某种重复性工作，例如：

- 读取另一项数据。
- 更新一个值（如银行余额或总计）。
- 递增一个计数器。

如果你无法确定循环内部需要做什么，可以先写下用手工解决问题时你会采取的步骤。例如，对于温度读取问题，你可能会写：

```
Read first value.
Read second value.
If second value is higher than the first, set highest temperature to that value, highest month to 2.
Read next value.
If value is higher than the first and second, set highest temperature to that value, highest month to 3.
Read next value.
If value is higher than the highest temperature seen so far, set highest temperature to that value, highest month to 4.
...
```

现在审视这些步骤，并将它们归结为一组可以放入循环体的*统一*操作。第一个操作很容易：

```
Read next value.
```

下一个操作则更棘手。在我们的描述中，我们使用了“高于第一个值”、“高于第一个和第二个值”、“高于目前所见最高温度”等测试条件。我们需要确定一个适用于所有迭代的测试条件。最后一种表述最为通用。

类似地，我们必须找到一种通用方式来设置最高月份。我们需要一个存储当前月份的变量，其值从 1 到 12。然后我们可以表述第二个循环操作：

```
If value is higher than the highest temperature, set highest temperature to that value, highest month to current month.
```

总之，我们的循环如下：

```
Loop
    Read next value.
    If value is higher than the highest temperature, set highest temperature to that value,
        highest month to current month.
    Increment current month.
```

## 第 2 步

指定循环条件。

你希望在循环中达到什么目标？典型示例有：

- 计数器是否达到了最终值？
- 是否已读取最后一个输入值？
- 某个值是否达到了给定阈值？

在我们的示例中，我们只需让当前月份达到 12。

## 第 3 步

确定循环类型。

我们区分两种主要的循环类型。确定次数循环（或计数控制循环）会执行确定的次数。不确定次数循环（或事件控制循环）的迭代次数事先不知道——循环会一直执行直到某个事件发生。后者一个典型示例是读取数据直到遇到哨兵的循环。

如果你事先知道循环重复的次数，请使用 for 语句。对于其他循环，请考虑循环条件。你是否需要先完成循环体的一次迭代，才能判断何时终止循环？如果是，则应选择 do 循环。否则，使用 while 循环。

在我们的示例中，我们读取 12 个温度值。因此，我们选择 for 循环。

## 第 4 步

为首次进入循环设置变量。

列出循环中使用和更新的所有变量，并确定如何初始化它们。通常，计数器初始化为 0 或 1，总计初始化为 0。

在我们的示例中，变量如下：

```
current month
highest value
highest month
```

我们需要谨慎地设置最高温度值。不能简单地将其设为 0。毕竟，我们的程序需要处理南极洲的温度值，这些温度可能都是负数。

一个好的选择是将最高温度值设置为第一个输入值。当然，这样我们就需要记住只再读取 11 个值，且当前月份从 2 开始。

我们还需要将最高月份初始化为 1。毕竟，在澳大利亚的城市里，我们可能永远找不到比一月更温暖的月份。

## 第 5 步

在循环结束后处理结果。

在许多情况下，所需结果只是循环体中更新的一个变量。例如，在我们的温度程序中，结果就是最高月份。有时，循环会计算对最终结果有贡献的值。例如，假设要求你计算温度的平均值。那么循环应该计算总和，而不是平均值。循环完成后，你就可以计算平均值了：用总和除以输入数量。

数字时钟中的小时和分钟显示就是嵌套循环的一个例子。小时循环 12 次，而每个小时对应分钟循环 60 次。

![](img/23fb3582e93ebc95909e1de029c3d388_193_0.png)

外层循环有 10 行。对于每个 x，程序在内层循环中打印 4 列。因此，总共打印 10 × 4 = 40 个值。下面是完整程序。请注意，我们也使用循环来打印表头。然而，这些循环不是嵌套的。

### ch04/powtable.cpp

```cpp
#include <iostream>
#include <iomanip>
#include <cmath>

using namespace std;

int main()
{
    const int NMAX = 4;
    const double XMAX = 10;

    // Print table header

    for (int n = 1; n <= NMAX; n++)
    {
        cout << setw(10) << n;
    }
    cout << endl;
    for (int n = 1; n <= NMAX; n++)
    {
        cout << setw(10) << "x";
    }
    cout << endl << endl;

    // Print table body

    for (double x = 1; x <= XMAX; x++)
    {
        // Print table row

        for (int n = 1; n <= NMAX; n++)
        {
            cout << setw(10) << pow(x, n);
        }
        cout << endl;
    }

    return 0;
}
```

### 程序运行结果

| 1 | 2 | 3 | 4 |
|---|---|---|---|
| x | x | x | x |
| 1 | 1 | 1 | 1 |
| 2 | 4 | 8 | 16 |
| 3 | 9 | 27 | 81 |
| 4 | 16 | 64 | 256 |
| 5 | 25 | 125 | 625 |
| 6 | 36 | 216 | 1296 |
| 7 | 49 | 343 | 2401 |
| 8 | 64 | 512 | 4096 |
| 9 | 81 | 729 | 6561 |
| 10 | 100 | 1000 | 10000 |

### 表 3 嵌套循环示例

| 嵌套循环 | 输出 | 说明 |
|---|---|---|
| `for (i = 1; i <= 3; i++)`<br>`{`<br>`    for (j = 1; j <= 4; j++)  { cout << "*"; }`<br>`    cout << endl;`<br>`}` | `****`<br>`****`<br>`****` | 打印 3 行，每行 4 个星号。 |
| `for (i = 1; i <= 4; i++)`<br>`{`<br>`    for (j = 1; j <= 3; j++)  { cout << "*"; }`<br>`    cout << endl;`<br>`}` | `***`<br>`***`<br>`***`<br>`***` | 打印 4 行，每行 3 个星号。 |
| `for (i = 1; i <= 4; i++)`<br>`{`<br>`    for (j = 1; j <= i; j++)  { cout << "*"; }`<br>`    cout << endl;`<br>`}` | `*`<br>`**`<br>`***`<br>`****` | 打印 4 行，长度分别为 1、2、3 和 4。 |
| `for (i = 1; i <= 3; i++)`<br>`{`<br>`    for (j = 1; j <= 5; j++)`<br>`    {`<br>`        if (j % 2 == 0) { cout << "*"; }`<br>`        else { cout << "-"; }`<br>`    }`<br>`    cout << endl;`<br>`}` | `-*-*-`<br>`-*-*-`<br>`-*-*-` | 在偶数列打印星号，在奇数列打印短横线。 |
| `for (i = 1; i <= 3; i++)`<br>`{`<br>`    for (j = 1; j <= 5; j++)`<br>`    {`<br>`        if ((i + j) % 2 == 0) { cout << "*"; }`<br>`        else { cout << " "; }`<br>`    }`<br>`    cout << endl;`<br>`}` | `* * *`<br>` * * `<br>`* * *` | 打印棋盘图案。 |

