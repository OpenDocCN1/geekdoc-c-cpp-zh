
## 表 15-2（续）

| 属性 | 用途 |
|---|---|
| DayOfYear | 获取 DateTime 的一年中的第几天，介于 1 到 366 之间。（闰年有 366 天。） |
| Hour | 获取 DateTime 的小时，介于 0 到 23 之间。 |
| Kind | 返回 DateTime 的种类：Local、Utc 或 Unspecified。 |
| Millisecond | 获取 DateTime 时间的毫秒。 |
| Minute | 获取 DateTime 的分钟，介于 0 到 59 之间。 |
| Month | 获取 DateTime 的月份，介于 1 到 12 之间。 |
| Now* | 获取当前日期和时间。 |
| Second | 获取 DateTime 的秒，介于 0 到 59 之间。 |
| TimeOfDay | 获取 DateTime 的时间，不含日期。 |
| Today* | 获取当前日期，不含时间。 |
| UtcNow* | 获取当前 UTC 日期和时间。 |
| Year | 获取 DateTime 的年份。 |

## 时间跨度

DateTime 表示一个时间点（1969 年 7 月 20 日 20:17:40）。TimeSpan 表示经过的时间段（1 天 17 小时 27 分钟 12 秒）。

创建 TimeSpan 的更有用的方法之一是从另一个 DateTime 中减去一个 DateTime，以找到它们之间的时间量。例如，以下代码计算第一次和最后一次载人登月之间的经过时间：

```
DateTime firstLanding = new DateTime(1969, 7, 20, 20, 17, 40);
DateTime lastLanding = new DateTime(1972, 12, 11, 19, 54, 57);
TimeSpan elapsed = lastLanding - firstLanding;
Console.WriteLine(elapsed.ToString());
```

该代码创建 DateTime 值来表示两次登月的时刻。然后它从第一个日期中减去最后一个日期以获取经过时间，并使用 resulting TimeSpan 的 ToString 方法来显示持续时间。以下文本以 days.hours:minutes:seconds 格式显示结果：

1239.23:37:17

表 15-3 总结了 TimeSpan 最有用的属性和方法。

```
        startButton.Enabled = false;
        stopButton.Enabled = true;
        updateLabelTimer.Enabled = true;
    }
```

- 当用户点击停止按钮时，停止 Timer，启用开始按钮，并禁用停止按钮。

1. 在停止按钮的 Click 事件处理程序中添加以下代码：

```csharp
// Stop the Timer.
private void stopButton_Click(object sender, EventArgs e)
{
    startButton.Enabled = true;
    stopButton.Enabled = false;
    updateLabelTimer.Enabled = false;
}
```

- 当 Timer 的 Tick 事件触发时，以 hh:mm:ss.ff 格式显示经过的时间。

1. 使用类似以下的代码。注意代码将毫秒数除以 10 以将其转换为百分之一秒：

```csharp
// Display the elapsed time.
private void updateLabelTimer_Tick(object sender, EventArgs e)
{
    // Subtract the start time from the current time
    // to get elapsed time.
    TimeSpan elapsed = DateTime.Now - StartTime;

    // Display the result.
    elapsedTimeLabel.Text = string.Format(
        "{0:00}:{1:00}:{2:00}.{3:00}",
        elapsed.Hours,
        elapsed.Minutes,
        elapsed.Seconds,
        elapsed.Milliseconds / 10);
}
```

## 练习

1. System.Diagnostics.Stopwatch 类像秒表一样工作。它提供启动、重置和停止计时的方法。复制你在“试一试”中构建的程序并修改它，使其使用 Stopwatch 类而不是 DateTime。提示：
   - 使用 Stopwatch 的 Elapsed 属性查看自手表启动以来经过了多长时间。
   - 让开始按钮调用手表的 Start 方法。
   - 让停止按钮调用手表的 Reset 方法以停止计时并将手表的经过时间重置为 0。

2. [Hard] 复制你在练习 1 中构建的程序并添加一个重置按钮。开始按钮应启动秒表，停止按钮应暂停它，而重置按钮应

## 16

## 使用数组和集合

前几课中描述的每种数据类型都保存单个数据。变量可能保存整数、字符串或时间点。

有时一次性处理一组相关值很方便。例如，假设你是刚刚取得巨大收益的庞大公司的首席执行官。在这种情况下，你可能想给每个小时工颁发一份感谢证书，并给每个高管 15% 的奖金。

在这种情况下，能够将所有小时工的数据存储在一个变量中以便轻松处理会很方便。同样，你可能希望将高管的数据存储在第二个变量中以便轻松管理。

在本课中，你将学习如何创建可以保存多个数据的变量。你将学习如何创建数组和不同种类的集合，例如 List、Dictionary、Stack 和 Queue。

本课解释了如何构建这些对象并向其添加和删除项目。第 19 课解释了如何通过遍历它们来充分利用它们，对它们包含的每个项目执行某些操作。

### 数组

数组是一组具有相同数据类型且共享相同名称的值。要选择数组中的特定项，程序使用索引，即大于或等于 0 的整数。

数组类似于公寓楼中的邮箱。建筑物有一个邮箱组，它们都具有相同的街道地址（数组的名称）。你使用公寓号码来选择邮箱组中的特定隔间。

图 16-1 以图形方式显示数组。此数组名为 values。它包含 8 个条目，索引为 0 到 7。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_273_0.png)

图 16-1

> 注意 数组的最小和最大索引分别称为其下界和上界。在 C# 中，下界始终为 0，上界始终比数组长度少一。

### 创建数组

以下代码显示了如何声明整数数组。方括号表示数组，因此语句 int [] 的第一部分表示变量的数据类型是整数数组：

```
int[] values;
```

声明数组变量后，你可以将其分配给新的未初始化数组。以下代码将变量 values 初始化为可容纳八个元素的新整数数组：

```
values = new int[8];
```

请记住，在 C# 中数组的下界始终为 0，因此此数组的索引为 0 到 7。

与其他变量一样，你可以在单个步骤中声明和初始化数组。以下代码在单个语句中声明并创建 values 数组：

```
int[] values = new int[8];
```

创建数组后，你可以通过使用数组的名称后跟方括号内的索引来访问其成员。例如，以下代码通过将第 N 个条目设为 N² 来初始化 values 数组：

```
values[0] = 0 * 0;
values[1] = 1 * 1;
values[2] = 2 * 2;
values[3] = 3 * 3;
values[4] = 4 * 4;
values[5] = 5 * 5;
values[6] = 6 * 6;
values[7] = 7 * 7;
```

> 注意 大多数程序员将 values[5] 发音为“values of 5”、“values sub 5”或“values 的第 5 个元素”。

将值放入数组后，你可以使用相同的方括号语法读取值。以下代码显示一个消息框，使用数组的一个值：

```
MessageBox.Show("7 * 7 is " + values[7].ToString());
```

为了使初始化数组更容易，C# 提供了简写语法，允许你在一条语句中声明数组并设置其值。只需将变量设为你想要的值，用逗号分隔并用大括号括起来，如以下代码所示：

```
int[] values = { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
```

当你使用此语法时，C# 使用你提供的值的数量来定义数组的大小。在前面的代码中，C# 会给 values 数组 10 个条目，因为代码提供了这么多值。

### 一个斐波那契示例

这是一个使用数组的稍微有趣一点的示例。斐波那契数列由以下三条规则定义：

```
Fibonacci[0] = 0
Fibonacci[1] = 1
Fibonacci[n] = Fibonacci[n - 1] + Fibonacci[n - 2]
```

> 注意 斐波那契数列由意大利数学家 Fibonacci 描述，是无限数列 0、1、1、2、3、5、8、13、21、... 数列中除前两个之外的每个值都是前两个值的和。例如，3 + 5 = 8。

> 斐波那契数列出现在几个奇怪而有趣的数学和自然系统中。例如，它们出现在花瓣排列和向日葵种子数量中。你甚至可以用它们在英里和公里之间转换（尽管这基本上是巧合）。有关更多信息，请参阅 www.mathisfun.com/numbers/fibonacci-sequence.html、math.stackexchange.com/questions/381/applications-of-the-fibonacci-sequence 或 mathworld.wolfram.com/FibonacciNumber.html。

图 16-2 所示的斐波那契程序（作为本课代码下载的一部分提供）使用数组来显示斐波那契数。使用 NumericUpDown 控件选择一个数字并点击计算以查看相应的斐波那契数。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_274_0.png)

当用户点击计算时，程序执行以下代码：

```
// Calculate and display the desired Fibonacci number.
private void calculateButton_Click(object sender, EventArgs e)
{
  int[] values = new int[21];
  values[0] = 0;
  values[1] = 1;
