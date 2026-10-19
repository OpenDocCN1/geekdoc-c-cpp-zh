

## 步骤 3-5：使用 new 关键字指定日期/时间，添加以下语句：

```
DateTime gradDate = new DateTime(2017, 5, 12);
DateTime gradDateTime = new DateTime(2017, 5, 12, 14, 30, 0);
```

运行程序，观察 gradDate 和 gradDateTime 的值。删除这些语句。

## 步骤 3-6：添加以下代码来声明变量，并从 DateTimePickers 获取毕业日期和时间。

运行窗体，检查变量 gradDate 和 gradTime 的值。

```
DateTime gradDate, gradDateTime, gradTime;
float numberOfDays;

//Get date of graduation:
gradDate = dtpGradDate.Value;
// Get time of graduation:
gradTime = dtpGradTime.Value;
```

## DateTime 的属性

DateTime 结构具有多种属性。表 2-7 显示了一些常用属性。第 3 列显示了按如下方式创建的 DateTime 的属性值：

```
DateTime graduationDate = DateTime.Parse("5/12/17 02:30 PM");
```

表 2-7：DateTime 结构的属性

| 属性 | 说明 | graduationDate 的属性值（5/12/2017 02:30 PM） |
|---|---|---|
| Day | 以整数形式返回日 | graduationDate.Day: 12 |
| Month | 以整数形式返回月 | graduationDate.Month: 5 |
| Year | 以整数形式返回年 | graduationDate.Year: 2017 |
| Now | 返回当前日期和时间 | DateTime.Now：（当前日期和时间） |
| Today | 返回当前日期 | DateTime.Today：（当前日期，默认时间为 12:00:00 AM） |
| Hour | 以整数形式返回小时 | graduationDate.Hour: 2 |
| TimeOfDay | 返回自午夜以来经过的时间，以 TimeSpan 表示（Hours、Minutes、Seconds 等） | TimeOfDay.Hours: 2<br>TimeOfDay.Minutes: 30<br>TimeOfDay.Seconds: 0 |
| 其他属性包括 Minutes、Seconds、DayOfWeek 和 DayOfYear | | |

### Today 与 Now 的对比

Today 属性返回今天的日期，默认时间为 12:00:00 AM；而 Now 返回今天的日期以及当前时间。

## 格式化 DateTime

表 2-8 显示了 DateTime 的常用格式化选项。

表 2-8：DateTime 的格式化选项

| 格式 | 5/12/2017 将显示为 |
|---|---|
| ToShortDateString | 5/12/2017 |
| ToLongDateString | Friday, May 12, 2017 |
| （无格式） | 5/12/2017 12:00:00 AM |
| ToString | 5/12/2017 12:00:00 AM |

## 步骤 3-7：输入以下代码，显示当前日期和时间以及毕业日期：

```
31  // Format and display current date & time and graduation date:
32  lstDisplay.Items.Clear();
33  lstDisplay.Items.Add("Current Date & Time:   " + DateTime.Now);
34  lstDisplay.Items.Add("Date of graduation:   " + gradDate.ToShortDateString());
```

运行程序并观察输出。将 gradDate 的格式改为 ToLongDateString，运行程序并观察输出。然后移除格式，查看默认格式的输出。

## 使用 ToString() 方法格式化日期/时间

就像使用 ToString() 方法格式化数字一样，你可以使用 DateTime 的 ToString 方法格式化日期和时间。例如，你可以显示某个日期的星期名称或月份名称。表 2-9 显示了 ToString() 方法可用的格式代码。

表 2-9：ToString 方法的格式代码

| 代码 | 5/12/2017 2:30 PM 将显示为 |
|---|---|
| "dd" | 12 |
| "ddd" | Fri |
| "dddd" | Friday |
| "MM" | 5 |
| "MMM" | May |
| "MMMM" | May |
| "yy" | 17 |
| "yyyy" | 2017 |
| "hh" | 02 |
| "mm" | 30 |
| "ss" | 00 |

你可以组合上述代码来创建自定义格式，如下所示：

| 格式 | 显示 |
|---|---|
| “dd MMM yyyy hh:mm:ss tt” | 12 May 2017 2:30:00 PM |
| “MM/dd/yy hh:mm tt” | 5/12/17 2:30 PM |

## 步骤 3-8：输入代码，显示 gradDate 中的星期、月份、月份中的日期，以及 gradDate 的毕业时间，如下所示：

| 问题 | 输出 |
|---|---|
| 毕业是星期几？ | Friday |
| 现在是几月？ | May |
| 月份中的第几天？ | 12 |
| 什么时间？ | 2:30:00 PM |

以下是要添加的代码。注意格式代码 “dddd” 和 “MMM” 如何用于显示日期中的星期和月份：

```
// Display the month & day of graduation:
lstDisplay.Items.Add("");
lstDisplay.Items.Add("What day is the graduation?" + gradDate.ToString("dddd"));
lstDisplay.Items.Add("What month is it?" + gradDate.ToString("MMM"));
lstDisplay.Items.Add("What day of the month?" + gradDate.Day);

//Format and display the time of graduation:
lstDisplay.Items.Add("What time?" + gradTime.ToLongTimeString());
```

修改第 38 行，使显示三个字母的星期缩写（例如，Fri）。

## 步骤 3-9：你可以使用表 2-8 中的不同格式代码进行实验，并观察输出。

接下来，将第 43 行的语句改为以下内容，以便不使用格式：`lstDisplay.Items.Add("What time?" + gradTime)`。运行窗体。注意，时间会与今天的日期一起显示，这是默认日期。

## 使用日期/时间进行计算

DateTime 结构提供了多种方法，用于查找两个日期/时间之间的差值以及向日期/时间添加间隔。表 2-10 显示了这些方法。

表 2-10：DateTime 的方法

| 方法 | 说明 | 方法返回的值 |
|---|---|---|
| AddDays(days) | 向 DateTime 添加指定天数后得到的 DateTime | graduationDate.AddDays(3)：返回 5/15/17 02:30 PM |
| AddMonths(months) | 向 DateTime 添加指定月数后得到的 DateTime | graduationDate.AddMonths(3)：返回 8/12/17 02:30 PM |
| AddHours(hours) | 向 DateTime 添加指定小时数后得到的 DateTime | graduationDate.AddHours(3)：返回 5/12/17 05:30 PM |
| 注意：可以使用相同语法的其他方法来添加年、分钟和秒。 | | |
| Subtract(DateTime) | 通过减去指定的 DateTime 得到一个 TimeSpan | graduationDate.Subtract(DateTime.Now)：返回一个 TimeSpan，表示现在与毕业日期之间的天数、小时数等。 |
| Add(TimeSpan) | 向 DateTime 添加指定的 TimeSpan 后得到的 DateTime | DateTime.Now.Add(fillTime)*：返回将 3 天、2 小时和 30 分钟添加到当前日期和时间后得到的 DateTime 值。<br>*fillTime: (3, 2, 30, 0, 0) |

## 计算两个日期之间的差值

.NET Framework 使用 TimeSpan 结构来表示两个 DateTime 值之间的时间间隔。

### TimeSpan 结构

要获取两个 DateTime 值之间的差值，你可以将一个值减去另一个值。例如，毕业前的时间可以计算并存储在一个 TimeSpan 变量中，如下所示：

```
TimeSpan timeToGraduate = gradDate-DateTime.Now;
```

表 2-11 显示了 TimeSpan 结构的常用属性。

表 2-11：TimeSpan 结构的属性

| TimeSpan 的属性 | 说明 |
|---|---|
| Days、Hours、Minutes、Seconds、Milliseconds、Ticks | 时间间隔中的整天数以及剩余的整小时、分钟、秒、毫秒和刻度数。<br>例如，表示（#12/19/2017 4:40:45 PM# - #12/18/2017 1:10:30 PM#）的 TimeSpan，其属性值如下：<br>Days - 1<br>Hours - 3<br>Minutes - 30<br>Seconds - 15 |
| TotalDays、TotalHours、TotalMinutes、TotalSeconds、TotalMilliseconds | 每个属性返回以特定单位（如天、小时或分钟）表示的整个时间间隔。例如，表示（#12/19/2015 4:30:45 PM# - #12/18/2015 1:20:40 PM#）的 TimeSpan，其属性值如下：<br>TotalDays - 1.146（0.146 表示小数天数）<br>TotalHours - 27.504（包括 27 小时和 .504 小数小时）<br>TotalMinutes - 1650.25 |

也可以使用 new 关键字创建 TimeSpan：

```
TimeSpan variableName = new TimeSpan(days, hours, minutes, seconds, milliseconds);
```

下面是一个具体的 TimeSpan 示例，表示填写订单所需的时间：2 天、3 小时和 30 分钟：

```
TimeSpan fillTime = new TimeSpan(2, 3, 30, 0, 0);
```

