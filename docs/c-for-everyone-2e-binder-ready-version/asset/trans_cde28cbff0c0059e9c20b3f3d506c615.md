
## 操作指南 4.1 — 编写循环

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_189_0.png)

本操作指南将带你逐步完成实现循环语句的过程。我们将用下面的示例问题来说明这些步骤：

读取十二个温度值（每个月一个），并显示温度最高的月份编号。例如，根据 http://worldclimate.com，死亡谷的平均最高气温为（按月份顺序）：

```
18.2  22.6  26.4  31.1  36.6  42.2
45.7  44.5  40.2  33.1  24.2  17.6
```

在这个例子中，温度最高（45.7 摄氏度）的月份是七月，程序应显示 7。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_189_1.png)

### 第 1 步

确定循环内部必须完成哪些工作。

每个循环都需要执行某种重复性工作，例如

- 读取下一项数据。
- 更新一个值（例如银行余额或总计）。
- 递增计数器。

如果你无法确定循环内部需要放什么，可以先写下手工解决该问题时会采取的步骤。例如，对于温度读取问题，你可能会写：

```
Read first value.
Read second value.
If second value is higher than the first, set highest temperature to that value, highest month to 2.
Read next value.
If value is higher than the first and second, set highest temperature to that value, highest month to 3.
Read next value.
If value is higher than the highest temperature seen so far, set highest temperature to that value,
    highest month to 4.
…
```

现在看看这些步骤，并将它们归纳为一组可以放入循环体的*统一操作*。第一个操作很简单：

```
Read next value.
```

下一个操作更棘手。在我们的描述中，我们使用了“高于第一个值”“高于第一个和第二个值”“高于目前见过的最高温度”等判断。我们需要确定一个适用于所有迭代的判断。最后一种表述最为通用。

同样，我们必须找到一种设置最高月份的通用方法。我们需要一个存储当前月份的变量，其值从 1 到 12。然后我们可以表述第二个循环操作：

```
If value is higher than the highest temperature, set highest temperature to that value,
    highest month to current month.
```

合起来，我们的循环是

```
Loop
    Read next value.
    If value is higher than the highest temperature, set highest temperature to that value,
        highest month to current month.
    Increment current month.
```

### 第 2 步

指定循环条件。

你希望在循环中达到什么目标？典型示例包括：

- 计数器是否已达到最终值？
- 你是否已读取最后一个输入值？
- 某个值是否已达到给定阈值？

在我们的示例中，我们只是希望当前月份达到 12。

### 第 3 步

确定循环类型。

我们区分两种主要循环类型。定数循环或计数控制循环执行确定的次数。在不定循环或事件控制循环中，迭代次数事先未知——循环会一直执行，直到某个事件发生。后者的一个典型例子是读取数据直到遇到哨兵值的循环。

如果你事先知道循环重复多少次，请使用 for 语句。对于其他循环，请考虑循环条件。你是否需要先完成一次循环体迭代，才能判断何时终止循环？在这种情况下，应选择 do 循环。否则，使用 while 循环。

在我们的示例中，我们读取 12 个温度值。因此，我们选择 for 循环。

### 第 4 步

为首次进入循环设置变量。

列出循环中使用和更新的所有变量，并确定如何初始化它们。通常，计数器初始化为 0 或 1，总计初始化为 0。

在我们的示例中，变量有

```
current month
highest value
highest month
```

我们需要谨慎设置最高温度值。不能简单地将其设为 0。毕竟，我们的程序需要处理来自南极洲的温度值，而这些值可能全是负数。

一个好的选择是将最高温度值设为第一个输入值。当然，这样我们就需要记住只再读取 11 个值，并让当前月份从 2 开始。

我们还需要将最高月份初始化为 1。毕竟，在澳大利亚的某个城市，我们可能永远找不到比一月更温暖的月份。

### 第 5 步

在循环结束后处理结果。

在许多情况下，所需结果只是一个在循环体中更新过的变量。例如，在我们的温度程序中，结果是最高月份。有时，循环会计算对最终结果有贡献的值。例如，假设要求计算温度的平均值。那么循环应计算总和，而不是平均值。循环完成后，就可以计算平均值：用总和除以输入数量。

下面是我们的完整循环：

```
Read first value; store as highest value.
highest_month = 1
for (current_month = 2; current_month <= 12; current_month++)
    Read next value.
    If value is higher than the highest value, set highest value to that value,
        highest_month to current_month.
```

### 第 6 步：用典型示例跟踪循环

按照 4.2 节所述，手工跟踪你的循环代码。选择不太复杂的示例值——执行循环 3～5 次就足以检查最常见的错误。在首次和最后一次进入循环时要特别注意。

有时，你可能想做一点小修改，以便能够进行跟踪。例如，在手工跟踪投资翻倍问题时，使用 20% 的利率而不是 5%。在手工跟踪温度循环时，使用 4 个数据值，而不是 12 个。

假设数据是 22.6 36.6 44.5 24.2。下面是跟踪过程：

| 当前月份 | 当前值 | 最高月份 | 最高值 |
| --- | --- | --- | --- |
| 2 | 36.6 | 2 | 22.6 |
| 3 | 44.5 | 3 | 36.6 |
| 4 | 24.2 | | 44.5 |

跟踪过程表明，**最高月份**和**最高值**已正确设置。

### 第 7 步：用 C++ 实现循环

下面是我们的示例对应的循环。练习 P4.4 要求你完成该程序。

```
double highest_value;
cin >> highest_value;
int highest_month = 1;
for (int current_month = 2; current_month <= 12; current_month++)
{
    double next_value;
    cin >> next_value;
    if (next_value > highest_value)
    {
        highest_value = next_value;
        highest_month = current_month;
    }
}
cout << highest_month << endl;
```

### 工作示例 4.1 信用卡处理

本工作示例使用循环从信用卡号中删除空格。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_191_0.png)

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_191_1.png)

## 4.8 嵌套循环

> 当一个循环的循环体包含另一个循环时，这些循环就是嵌套的。嵌套循环的一个典型用途是打印带行和列的表格。

在 3.4 节中，你看到了如何嵌套两个 if 语句。同样，复杂的迭代有时需要**嵌套循环**：一个循环位于另一个循环语句内部。处理表格时，嵌套循环会自然出现。外层循环遍历表格的所有行。内层循环处理当前行中的列。

本节你将看到如何打印表格。为简单起见，我们将只打印幂 x^a，如右表所示。

| x^1 | x^2 | x^3 | x^4 |
| --- | --- | --- | --- |
| 1 | 1 | 1 | 1 |
| 2 | 4 | 8 | 16 |
| 3 | 9 | 27 | 81 |
| ... | ... | ... | ... |
| 10 | 100 | 1000 | 10000 |

下面是打印该表格的伪代码：

```
Print table header.
For x from 1 to 10
    Print table row.
    Print endl.
```

如何打印表格的一行？你需要为每个指数打印一个值。这需要第二个循环：

```
For n from 1 to 4
    Print x^n.
```

这个循环必须放在前一个循环内部。我们说内层循环*嵌套*在外层循环中（见图 7）。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_192_0.png)
