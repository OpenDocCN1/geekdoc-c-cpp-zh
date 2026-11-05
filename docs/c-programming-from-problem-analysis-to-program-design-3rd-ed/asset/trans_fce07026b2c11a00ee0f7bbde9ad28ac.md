
```csharp
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
    Console.WriteLine("Calorie Counter");
    Console.WriteLine("Daily Averages");
    foreach (double avgCalorie in dailyAverage)
    {
        Console.WriteLine("Day {0}: {1,6:N0}", dayNumber,
                          avgCalorie);
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
        Console.WriteLine("{0,-10}: {1,6}", mealTime[c],
                          mealAverage[c].ToString("N0"));
    }
}

public static void DisplayAverageCaloriesPerMeal(int[,] calories)
{
    double sum = 0;
    for (int da = 0; da < calories.GetLength(0); da++)
        for (int ml = 0; ml < calories.GetLength(1); ml++)
            sum += calories[da, ml];
    Console.WriteLine("\nCaloric Average Per Meal: {0:N0}",
                      sum / calories.Length);
}
}
```

示例 8-9 包含三个独立的 Display 方法。DisplayDailyAverage() 方法演示了使用 foreach 循环。由于此循环结构不包含索引，因此定义了一个单独的变量 dayNumber，并在循环体内部递增，以便打印日期编号。此示例产生的输出如 图 8-3 所示。

![](img/e33ae760e23d89eac66541252ad65de8_456_0.png)

图 8-3 WeeklyCalorieCounter 的输出

在查看图 8-3 时，请注意数字已正确对齐。查看示例 8-10 中显示的格式说明符。

### 示例 8-10

```csharp
Console.WriteLine("{0,-10}: {1,6}", mealTime[c],
                  mealAverage[c].ToString("N0"));
```

逗号将占位符索引与宽度说明符分隔开。第一个参数 ({0,-10}) 表示第一个参数应以宽度 10 显示。10 前面的负值表示 mealTime[c] 中存储的值应左对齐。右对齐是默认值。一维数组 mealTime 存储餐食类型（即 Breakfast、Lunch、Dinner）。餐食类型后跟一个冒号，然后实际值以宽度 6 ({1,6}) 个字符位置显示。由于值 6 为正，因此数字右对齐且排列整齐。

在示例 8-10 中，调用 ToString() 方法将存储在 mealAverage[c] 中的 double 值转换为字符串值。格式说明符 N 用于将其转换为带逗号分隔符的数字。N 后面的零表示小数点右侧不应有数字。

## 锯齿数组

当各行的列数必须不同时，可以创建 jagged 或 **ragged array**。**Jagged arrays** 与矩形数组不同，矩形数组始终具有矩形形状，如表格。Jagged arrays 被称为“**arrays of arrays**。”一行可能有五列；另一行有 50 列。要创建 jagged array，可以创建类型为 `Array` 的一维数组，并分别初始化每个一维数组。示例 8-11 说明了 jagged array 的创建。

### 示例 8-11

```csharp
int[][] anArray = new int[4][];
anArray[0] = new int[] {100, 200};
anArray[1] = new int[] {11, 22, 37};
anArray[2] = new int[] {16, 72, 83, 99, 106};
anArray[3] = new int[] {1, 2, 3, 4};
```

GetLength()、GetUpperBound() 和 GetLowerBound() 方法可与 jagged arrays 一起使用。Jagged arrays 的使用方式与矩形数组完全相同，只是各行的元素数量可能不同。

## 多维数组

在 C# 中可以分配数组的维度数量方面，你几乎只受想象力的限制。主要要求是放置在数组中的所有数据值必须为相同的基础类型。二维数组实际上是多维数组；然而，它是一种如此常见的结构类型，通常被归为自己的类别。

要声明三维数组，需要使用三个整数值。它们指定为数组预留的平面数、行数和列数。与单维数组一样，三维数组通过标识符名称引用。

创建三维数组的格式为：

```
type[,,] identifier =
    new type[integral value, integral value, integral value];
```

如果你想创建 calories 表来保存四周的统计数据怎么办？可以定义一个三维数组来保存数据。第一个维度可以表示周数，第二个表示天数，第三个表示餐次。要创建数组在 C# 中保存该额外数据，你写：

```csharp
int[,,] calories = new int[4, 7, 3];
```

![](img/e33ae760e23d89eac66541252ad65de8_458_0.png)

图 8-4 三维数组

这为 84 个元素（4 * 7 * 3）分配存储空间。你会注意到索引的上限为 3、6 和 2；三个的下限均为 0。

通过按示例 8-12 所示的方式对数组进行维度设置，可以添加一列来保存每天的总卡路里。示例 8-12 中的代码将前 3 列相加并将总和放在新的第四列中。

### 示例 8-12

```csharp
int[,,] calories = new int[4, 7, 4];
// Loop to place the row total in the last column, indexed by 3
for (int wk = 0; wk < calories.GetLength(0); wk++)
{
    for (int da = 0; da < calories.GetLength(1); da++)
    {
        for (int ml = 0; ml < calories.GetLength(2) - 1; ml++)
        {
            calories[wk, da, 3] += calories[wk, da, ml];
        }
    }
}
```

![](img/e33ae760e23d89eac66541252ad65de8_459_0.png)

重新检查示例 8-12 中的第一行，注意表示列数的维度已从 3 改为 4。这使得每行的总卡路里可以存储在此列中。

最后一个维度的长度整数值已从 3 改为 4，以保存每天的总量。现在每一行都有早餐、午餐、晚餐的餐次计数以及总计数。

嵌套循环将每一行索引为 0 到 2 的列相加，并将结果存储在索引为 3 的列中。最内层循环的条件表达式使用 (calories.GetLength(2) - 1) 进行求值。GetLength(2) 返回第三个维度或秩的长度。这返回 4，因为现在行中有四列。但请注意，从该值中减去 1，因为最后一列不应被相加。它保存的是总计。因此，循环对 ml = 0、ml = 1 和 ml = 2 执行。当 ml 等于 3 时，ml 不再小于 3（ml < calories.GetLength(2) - 1），并且该迭代的内层循环完成。

calories.GetLength(0) 返回平面数或周数的维度。它返回 4。GetLength(1) 返回每个平面的行数或每周天数的维度。它返回 7。如前所述，GetLength(2) 返回每行的列数或每天餐次数的维度。它返回 4。卡路里计数应用程序的程序列表包含为示例 8-13。
