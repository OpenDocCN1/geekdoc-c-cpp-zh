
### 示例 8.6

```csharp
double[] dailyAverage = new double[7];

dailyAverage = CalculateAverageByDay(calories);
```

在示例 8.6 中，调用 `CalculateAverageByDay()` 时，它将二维数组 `calories` 作为参数传入。再次注意，这里没有方括号。该调用发送数组首元素的地址。当方法结束并返回 `Main()` 时，局部数组 `dailyAverage` 首元素的地址通过方法调用返回，然后赋给 `Main()` 方法中定义的局部一维数组 `dailyAverage`。

C# 是一种行主序语言，这意味着引用数组元素时先指定行索引。在前一个示例中，变量 `r` 放在最外层循环。也可以一次处理一列数据。如果你想计算所有早餐、午餐或晚餐期间摄入的平均卡路里数，就把第零列的所有行相加。示例 8.7 中的嵌套循环展示了将列变量放在最外层循环。

### 示例 8.7

```csharp
public static double[] CalculateAverageByMeal(int[,] calories)
{
    int sum = 0;
    double[] mealAverage = new double[3];
    for (int c = 0; c < calories.GetLength(1); c++)
    {
        for (int r = 0; r < calories.GetLength(0); r++)
            sum += calories[r, c];
        mealAverage[c] = (double)sum / calories.GetLength(0);
        sum = 0;
    }
    return mealAverage;
}
```

请注意，在示例 8.7 中，当语句 `sum += calories[r, c]` 引用 `calories` 数组时，行仍然列在前面。与前一个示例一样，`CalculateAverageByMeal()` 方法返回一个一维数组。方法也可以返回二维数组。

有时，使用更能代表数据的标识符来表示行索引和列索引会更具可读性。由于行存储某一天的热量，示例 8.8 使用标识符 `da`（而不是 `r`）来存储行号。每一列保存某一餐的热量；因此，使用标识符 `ml` 来存储列号。与最后两个示例一样，示例 8.8 使用嵌套循环将数组中的每个元素相加。变量 `da` 存储行号，而 `ml` 存储列号。

### 示例 8.8

```csharp
public static void DisplayAverageCaloriesPerMeal(int[,] calories)
{
    double sum = 0;
    for (int da = 0; da < calories.GetLength(0); da++)
        for (int ml = 0; ml < calories.GetLength(1); ml++)
            sum += calories[da, ml];
    Console.WriteLine("\nCaloric Average Per Meal: {0:N0}",
                      sum / calories.Length);
}
```

在此示例中，`sum` 除以 `calories.Length` 属性返回的值。`Length` 属性用于返回所有维度中的元素总数。对于示例 8.8，`Length` 返回 21。

示例 8.9 显示了整个应用程序。它对二维数组进行了编译时初始化。该应用程序显示每天摄入的平均卡路里数、每种餐类型的平均卡路里数，以及每餐的总体平均值。

> **注意**
>
> 当你在 Visual Studio 中创建解决方案时，代码生成器会添加额外的 `using` 语句。为节省篇幅，已从示例 8.9 和其他示例中删除不必要的 `using` 语句。

### 示例 8.9

```csharp
/* CalorieCounter.cs       Author: Doyle
 * Demonstrates usage of a two-dimensional array
 * to calculate the average number of calories
 * intake per day, per meal type, and per meal.
 */

using System;

namespace WeeklyCalorieCounter
{
    public class WeeklyCalorieCounter
    {
        public static void Main()
        {
            int[,] calories = {{900, 750, 1020},
                               {300, 1000, 2700},
                               {500, 700, 2100},
                               {400, 900, 1780},
                               {600, 1200, 1100},
                               {575, 1150, 1900},
                               {600, 1020, 1700}};
            double[] dailyAverage = new double[7];
            double[] mealAverage = new double[3];

            dailyAverage = CalculateAverageByDay(calories);
            mealAverage = CalculateAverageByMeal(calories);

            DisplayDailyAverage(dailyAverage);
            DisplayMealAverage(mealAverage);
            DisplayAverageCaloriesPerMeal(calories);
            Console.ReadKey();
        }

        public static double[] CalculateAverageByDay(int[,] calories)
        {
            int sum = 0;
            double[] dailyAverage = new double[7];
            for (int r = 0; r < calories.GetLength(0); r++)
            {
                for (int c = 0; c < calories.GetLength(1); c++)
                    sum += calories[r, c];
                dailyAverage[r] = (double)sum / calories.GetLength(1);
                sum = 0;
            }
            return dailyAverage;
        }

        public static double[] CalculateAverageByMeal(int[,] calories)
        {
            int sum = 0;
            double[] mealAverage = new double[3];
            for (int c = 0; c < calories.GetLength(1); c++)
            {
                for (int r = 0; r < calories.GetLength(0); r++)
                    sum += calories[r, c];
                mealAverage[c] = (double)sum / calories.GetLength(0);
                sum = 0;
            }
            return mealAverage;
        }

        public static void DisplayDailyAverage(double[] dailyAverage)
        {
            int dayNumber = 1;
            Console.WriteLine("*Calorie Counter*");
            Console.WriteLine("Daily Averages");
            foreach (double avgCalorie in dailyAverage)
            {
                Console.WriteLine("Day {0}: {1,6:N0}", dayNumber, avgCalorie);
                dayNumber++;
            }
        }

        public static void DisplayMealAverage(double[] mealAverage)
        {
            string[] mealTime = {"Breakfast", "Lunch", "Dinner"};
            Console.WriteLine("\n\nCalorie Counter");
            Console.WriteLine("Meal Averages");
            for (int c = 0; c < mealAverage.Length; c++)
            {
                Console.WriteLine("{0,-10}: {1,6}", mealTime[c], mealAverage[c].ToString("N0"));
            }
        }

        public static void DisplayAverageCaloriesPerMeal(int[,] calories)
        {
            double sum = 0;
            for (int da = 0; da < calories.GetLength(0); da++)
                for (int ml = 0; ml < calories.GetLength(1); ml++)
                    sum += calories[da, ml];
            Console.WriteLine("\nCaloric Average Per Meal: {0:N0}", sum / calories.Length);
        }
    }
}
```

示例 8.9 包含三个独立的 `Display` 方法。`DisplayDailyAverage()` 方法演示了如何使用 `foreach` 循环。由于此循环结构不包含索引，因此定义了一个单独变量 `dayNumber`，并在循环体内部递增，以便打印天数。此示例产生的输出如图 8.3 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_488_0.png)

**图 8.3** WeeklyCalorieCounter 的输出

查看图 8.3 时，注意数字已正确对齐。请查看示例 8.10 中所示的格式说明符。

### 示例 8.10

```csharp
Console.WriteLine("{0,-10}: {1,6}", mealTime[c],
                  mealAverage[c].ToString("N0"));
```

逗号将占位符索引与宽度说明符分隔开。第一个占位符（`{0,-10}`）表示第一个参数应以宽度 10 显示。10 前面的负值表示 `mealTime[c]` 中存储的值应左对齐。右对齐是默认设置。一维数组 `mealTime` 存储餐类型（即 Breakfast、Lunch、Dinner）。餐类型后跟一个冒号，然后实际值以 6 个字符位置（`{1,6}`）的宽度显示。由于值 6 为正数，数字右对齐并正确对齐。

在示例 8.10 中，调用 `ToString()` 方法将 `mealAverage[c]` 中存储的 double 值转换为字符串值。格式说明符 `N` 用于将其转换为带逗号分隔符的数字。`N` 后面的 0 表示小数点右侧不应有数字。

> **注意**
>
> 使用 `new` 关键字创建数组元素时，C# 会将数组元素初始化为 null 值。测试是否已存储值的一种方法是测试是否为 `null`。当数组尚未引用任何值时，以下代码返回 true。
>
> ```csharp
> string[] name = new string[10];
> if (name[0] == null)
> ```

## 交错数组

当各行中的列数必须不同时，可以创建交错数组（或称不规则数组）。交错数组与矩形数组的区别在于，矩形数组始终具有像表格一样的矩形形状。交错数组被称为“数组的数组”。一行可能有五列；另一行可能有 50 列。要创建交错数组，可以创建一个 `Array` 类型的一维数组，并分别初始化每个一维数组。示例 8.11 演示了交错数组的创建。

### 示例 8.11

```csharp
int[][] anArray = new int[4][];
anArray[0] = new int[] {100, 200};
anArray[1] = new int[] {11, 22, 37};
anArray[2] = new int[] {16, 72, 83, 99, 106};
anArray[3] = new int[] {1, 2, 3, 4};
```

`GetLength()`、`GetUpperBound()` 和 `GetLowerBound()` 方法可用于交错数组。交错数组的用法与矩形数组完全相同，只是各行可能具有不同数量的元素。

## 多维数组

在 C# 中，你能为数组分配多少维，实际上只受想象力的限制。主要要求是，放入数组的所有数据值必须具有相同的基类型。二维数组实际上是一种多维数组；然而，它是一种非常常见的结构类型，因此通常被单独归为一类。

要声明三维数组，需要使用三个整数值。它们指定为数组预留的平面数、行数和列数。与一维数组一样，三维数组通过标识符名称引用。

创建三维数组的格式为：

```csharp
type[,,] identifier =
    new type[integral value, integral value, integral value];
```
