
# 第7 章 数组

创建一个应用程序，用于监测特定水道内海牛的数量。一个研究小组每月会在某区域性水道上进行四至六次飞行，并记录海牛的目击情况。研究人员会记录日期、地点以及该地点出现的海牛数量。

确定特定地点哪一天的目击次数最高。打印该日期以及月份的实际名称。还要包含与最高目击次数相关的计数。规划你的应用程序，以便能够确定特定地点的平均目击次数。

设计一个面向对象的解决方案。使用两个类。对于海牛观测类（`ManateeSighting` class），应包含位置、观测日期、海牛数量、平均目击次数和最高目击日期等特征。确定平均值、最高目击日期以及相关月份名称的方法应该是该类的一部分。

在第二个类中，实例化海牛观测类的对象。允许用户输入关于特定地点的数据。测试海牛观测类的成员。

![](img/45e6f245af31396d967c3186f196d331_425_0.png)

图 7-11 海牛示例问题规范

## 分析问题

你应该审查图 7-11 中的问题规范，并确保你理解了问题定义。程序将输入多个值来代表地点、日期和目击的海牛数量。这些日期和计数将输入到数组中，并用于实例化 `ManateeSighting` 类的对象。

表 7-2 列出了海牛观测问题所需的数据字段成员。

| 数据项目描述 | 类型 | 标识符 |
|---|---|---|
| 目击地点 | string | location |
| 飞行日期 | string [ ] | sightDate |
| 目击到的海牛数量 | int [ ] | manateeCount |
| 每个地点的平均计数 | double | avg |
| 单个地点最大目击数 | int | maxCnt |
| 单个地点最大目击的日期 | string | maxDate |
| 与最高目击日期对应的月份名称 | string | monthWithMostSightings |

# 编程示例：海牛应用程序

将创建第二个类来测试 `ManateeSighting` 类。为了实现这一点，需要使用 `ManateeSighting` 类的额外数据。如问题规范所述，应用程序类允许用户输入值，以便实例化 `ManateeSighting` 类。应用程序类中声明了位置的局部变量以及日期和计数的数组。这两个数组的维度将设置为最大 20 个条目。实际记录的数量将用于构建 `ManateeSighting` 对象。为了测试目的，将输入单个地点。可以修改应用程序以创建用于关于多个地点的数据数组。

## 设计解决方案

预期的输出是显示地点、最活跃月份的目击次数，以及目击海牛数量最多的日期（包括月份名称）。图 7-12 显示了最终输出可能外观的原型。

![](img/45e6f245af31396d967c3186f196d331_426_0.png)

图 7-12 原型

类图用于帮助设计和记录数据及行为特征。图 7-13 显示了海牛应用程序示例的类图。

![](img/45e6f245af31396d967c3186f196d331_427_0.png)

图 7-13 类图

类图没有显示特定方法可能需要的属性或局部变量。表 7-3 列出了定义了属性的数据成员，这些指示了是否需要 get 和/或 set。表中也显示了属性的名称。

# 表 7-3 ManateeSighting 类的属性

| 数据成员标识符 | 属性标识符 | Set | Get |
|---|---|---|---|
| location | Location | ✓ | |
| monthWithMostSightings | monthWithMostSightings | | ✓ |
| avg | Avg | | ✓ |
| maxCnt | MaxCnt | | ✓ |
| maxDate | MaxDate | | ✓ |

属性 `MonthWithMostSightings`、`MaxDate` 和 `Avg` 是只读的。这是因为它们是通过计算得到的。

```csharp
using System;

namespace ManateeSighting
{
    public class ManateeSighting
    {
        private string location;
        private string[] sightDate;
        private int[] manateeCount;
        private double avg;
        private int maxCnt;
        private string maxDate;
        private string monthWithMostSightings;
        // 默认构造函数
        public ManateeSighting()
        {
        }
        // 构造函数
        public ManateeSighting(string loc, string[] date, int[] cnt, int numEntries)
        {
            sightDate = new string[numEntries];
            manateeCount = new int[numEntries];
            Array.Copy(date, 0, sightDate, 0, numEntries);
            Array.Copy(cnt, 0, manateeCount, 0, numEntries);
            location = loc;
        }
        // 属性
        public string Location
        {
            get
            {
                return location;
            }
            set
            {
                location = value;
            }
        }
        public string MonthWithMostSightings
        {
            get
            {
                DetermineMax();
                return monthWithMostSightings;
            }
        }
        public double Avg
        {
            get
            {
                CalculateAvg();
                return avg;
            }
        }
        public int MaxCnt
        {
            get
            {
                DetermineMax();
                return maxCnt;
            }
        }
        public string MaxDate
        {
            get
            {
                DetermineMax();
                return maxDate;
            }
        }
        private void CalculateAvg()
        {
            int total = 0;
            for (int i = 0; i < manateeCount.Length; i++)
            {
                total += manateeCount[i];
            }
            if (manateeCount.Length > 0)
                avg = (double)total / manateeCount.Length;
        }
        private void DetermineMax()
        {
            int max = -1;
            int maxIndex = 0;
            for (int i = 0; i < manateeCount.Length; i++)
            {
                if (manateeCount[i] > max)
                {
                    max = manateeCount[i];
                    maxIndex = i;
                }
            }
            if (max != -1)
            {
                maxCnt = max;
                maxDate = sightDate[maxIndex];
                // 这里处应该是确定月份名称的逻辑
            }
        }
    }
}
```

```csharp
// 用于确定实际日期的数组。
// 调用方法设置月份名称。
public void DetermineMax() {
    int maxCntIndex = manateeCount.Length;
    for(int i = 1; i < manateeCount[i]; i++)
        if(manateeCount[i] > manateeCount[maxCntIndex])
            maxCntIndex = i;
    maxCnt = manateeCount[maxCntIndex];
    maxDate = sightDate[maxCntIndex];
    monthWithMostSightings = ReturnMonth(maxDate);
}
// 给定月份数，计算给定位置的平均值。
public double ComputeMonthAvg(string mon) {
    int total = 0;
    int days = 0;
    double monAverage;
    for(int i = 0; i < sightDate.Length; i++) {
        if(sightDate[i].StartsWith(mon)) {
            total += manateeCount[i];
            days++;
        }
    }
    if (days > 0)
        monAverage = total / days;
    else
        monAverage = 0;
    return monAverage;
}
// 给定 mm/dd/yyyy 格式的日期
// 返回月份名称。
public string ReturnMonth(string startDate) {
    string [] monthName = {"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};
    string [] dateParts = someDate.Split('/');
    dateParts[0] = dateParts[0].TrimStart('0');
    return monthName[Convert.ToInt32(dateParts[0]) - 1];
}
}
```

# 编程示例：海牛应用程序 399

```csharp
/** 
 * ManateeApp.cs    作者: Doyle
 * 这是一个使用 ManateeSighting 类的客户端程序。
 * 用户会被提示位置、日期和观测数量。
 * 通过调用许多方法和属性，
 * 对 ManateeSighting 类string了测试。
 */
using System;

namespace ManateeApp
{
    public class ManateeApp
    {
        static void Main(string[] args)
        {
            string location;
            int sightingCnt;
            string [] dArray = new String[20];
            int [] manateeCnt = new int[20];
            sightingCnt = GetData(out location, dArray, manateeCnt);
            ManateeSighting m = new ManateeSighting(location, dArray, manateeCnt, sightingCnt);
            Console.WriteLine();
            Console.WriteLine();
            Console.WriteLine("Location: {0}", m.Location);
            Console.WriteLine("Average number of Sightings: {0}", m.Avg);
            Console.WriteLine();
            Console.WriteLine("Month Name for Date with Most Sightings: {0}", m.MonthWithMostSightings);
            Console.WriteLine("Date of the Most Sightings : {0}", m.MaxDate);
            Console.WriteLine("Count for {0}: {1}", m.MaxDate, m.MaxCnt);
        }
        public static int GetData(out string location, string [] dArray, int [] manateeCnt)
        {
            int i;
```

# 第 7 章 数组

```csharp
Console.Write("Location: ");
location = Console.ReadLine();
Console.Write("How many records for {0}? ", location);
string inValue = Console.ReadLine();
int loopCnt = Convert.ToInt32(inValue);
for (int i = 0; i < loopCnt; i++)
{
    Console.Write("Date (mm/dd/yyyy): ");
    dArray[i] = Console.ReadLine();
    Console.Write("Number of Sightings: ");
    inValue = Console.ReadLine();
    manateeCnt[i] = Convert.ToInt32(inValue);
}
return i;
```
