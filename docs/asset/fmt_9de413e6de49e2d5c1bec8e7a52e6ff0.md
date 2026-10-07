
```csharp
static void testUniform()
{
    int nBins = 20;
    int nPoints = 10000;
    double xmin = 0.0;
    double xmax = 20.0;
    double a = 5.0;
    double b = 15.0;
    double displayScaleFactor = 500.0;
    double[] randObj = makeUniformDiscrete(nPoints, a, b);
    double[] HistogramValues = makehistogram(randObj, xmin, xmax, nBins);
    double[] xdata = new double[nBins];
    double[] ydata = new double[nBins];
    double[] yCalDistribution = new double[nBins];
    for (int i = 0; i < nBins; i++)
    {
        xdata[i] = i;
        ydata[i] = (double)HistogramValues[i];
        yCalDistribution[i] = UniformF(i, a, b);
    }
    double ydataMax = dataMax(ydata);
    double yCalDistributionMax = dataMax(yCalDistribution);
    Console.WriteLine("Testing the (Discrete) Probability Distribution\n");
    Console.WriteLine("Key: Bin number = *****... [随机分布] [计算分布]\n");
    for (int i = 0; i < nBins; i++)
    {
        Console.Write("Bin " + i + " = " + i + 1);
        for (int j = 0; j < (Math.Round(ydata[i] * displayScaleFactor / ydataMax, 0)); j++)
        {
            Console.Write("[" + (int)j + "]*" + Math.Round(ydata[i] * 100.0 / yCalDistribution[i] * 100.0 / yCalDistributionMax, 0) + "]");
        }
        Console.WriteLine();
    }
}
```

### 结果：均匀（离散）概率分布

键：箱号 = *****... [随机分布]

| 箱号 | 随机分布 | 计算分布 |
| :--- | :--- | :--- |
| 0 | [0] | [0] |
| 1 | [0] | [0] |
| 2 | [0] | [0] |
| 3 | [0] | [0] |
| 4 | [0] | [0] |
| 5 | ********************* [96] | [100] |
| 6 | ********************* [99] | [100] |
| 7 | ********************* [97] | [100] |
| 8 | ********************* [98] | [100] |
| 9 | *********************** [100] | [100] |
| 10 | ******************** [96] | [100] |
| 11 | ******************** [91] | [100] |
| 12 | ******************** [95] | [100] |
| 13 | ******************** [93] | [100] |
| 14 | ********************* [93] | [100] |
| 15 | ********************* [97] | [0] |
| 16 | [0] | [0] |
| 17 | [0] | [0] |
| 18 | [0] | [0] |
| 19 | [0] | [0] |

## 10.7.2 连续分布

# Beta 分布

Beta 分布广泛应用于贝叶斯统计中。贝叶斯推断是一种统计推断，通过证据或观测结果来更新或推断某个假设为真的概率。“贝叶斯”一词源于推断过程中对贝叶斯定理的频繁使用。Beta 分布也可用于建模受限制在最小值和最大值定义的区间内的事件。由于由于原因，Beta 分布被广泛应用于项目管理系统，用于描述任务完成的时间。

## 随机数 329

```csharp
public static double NextBeta(int a, int b)
{
    double gammal = NextGamma(a, 1);
    double gamma2 = NextGamma(b, 1);
    return gammal / (gammal + gamma2);
}
```

```csharp
public static double[] NextBeta(int a, int b, int nLength)
{
    double[] tempArr = new double[nLength];
    for (int i = 0; i < nLength; i++)
        tempArr[i] = NextBeta(a, b);
    return tempArr;
}
```

```csharp
static void TestBeta()
{
    int nBins = 20;
    int nPoints = 10000;
    double xmin = 0.0;
    double xmax = 1.0;
    double aVal = 2.0;
    double bVal = 5.0;
    double displayScaleFactor = 500.0;

    double[] randObj = NextBeta(aVal, bVal, nPoints);
    double[] histogramValues = makeHistogram(randObj, xmin, xmax, nBins);
    double[] xdata = new double[nBins];
    double[] ydata = new double[nBins];
    double[] yCalDistribution = new double[nBins];
    for (int i = 0; i < nBins; i++) {
        xdata[i] = xmin + (i + 0.5) * (xmax - xmin) / nBins;
        ydata[i] = histogramValues[i];
        yCalDistribution[i] = BetaPDF(xdata[i], aVal, bVal);
    }

    double yMax = dataMax(ydata);
    double yCalDistributionMax = dataMax(yCalDistribution);

    Console.WriteLine("\nTesting Beta Probability Distribution");
    Console.WriteLine("\nKey: *****... [随机分布] [计算分布]");
}
```

# C# 中的数值方法、算法与工具

结果：Beta 概率分布

键值：箱号 = ***** [随机分布] [计算分布]

| 箱号 | 随机分布 | 计算分布 |
| :--- | :--- | :--- |
| Bin 0 | ***** | [25] [28] |
| Bin 1 | ***************** | [67] [68] |
| Bin 2 | ******************* | [92] [90] |
| Bin 3 | ********************* | [99] [100] |
| Bin 4 | ********************* | [100] [100] |
| Bin 5 | ******************** | [89] [94] |
| Bin 6 | ******************* | [82] [83] |
| Bin 7 | ***************** | [67] [70] |
| Bin 8 | ***************** | [57] [57] |
| Bin 9 | **************** | [42] [44] |
| Bin 10 | ****** | [29] [33] |
| Bin 11 | ***** | [25] [23] |
| Bin 12 | **** | [17] [15] |
| Bin 13 | *** | [11] [9] |
| Bin 14 | * | [6] [5] |
| Bin 15 | | [2] [2] |
| Bin 16 | | [1] [1] |
| Bin 17 | | [0] [0] |
| Bin 18 | | [0] [0] |
| Bin 19 | | [0] [0] |

# Beta 概率分布

Beta 原始分布（Beta prime distribution）是一种定义在 $x > 0$ 的概率分布，具有两个参数 $a$ 和 $b$，具有以下特征 [65, 66, 49]：

参数：$a > 0, b > 0$

> PDF: $f(x) = \frac{x^{a-1}(1+x)^{-a-b}}{\beta(a,b)} \quad x > 0$

该分布也称为第二类 Beta 分布，与其相关的分布相比。随机变量 Beta 原始分布可以从其对应的 Beta 分布变量非常容易生成：$X_{beta prime} = X_{beta}/(1 - X_{beta})$。以下代码演示了如何在 C# 中实现 Beta 概率密度分布。

```csharp
public static double BetaPrimePDF(double x, double a, double b)
{
    return Math.Pow(x,a-1) * Math.Pow(1+x,-a-b) / Beta(a,b);
}

public static double[] BetaPrimePDF(double[] x, double a, double b)
{
    double[] tempArray = new double[x.Length];
    for (int i = 0; i < x.Length; i++) {
        tempArray[i] = BetaPrimePDF(x[i], a, b);
    }
    return tempArray;
}
```

## 随机数 331

```csharp
public static double NextBetaPrime(int a, int b)
{
    double betaVariate = NextBeta(a, b);
    return betaVariate / (1.0 - betaVariate);
}
```

```csharp
public static double[] NextBetaPrime(int a, int b, int nLen)
{
    double[] tempArr = new double[nLen];
    for (int i = 0; i < nLen; i++) {
        tempArr[i] = NextBetaPrime(a, b);
    }
    return tempArr;
}
```

```csharp
static void TestBetaPrime()
{
    int nBins = 20;
    int nPoints = 10000;
    double xmin = 0.0;
    double xmax = 1.0;
    double aVal = 3;
    double bVal = 6;
    double displayScaleFactor = 500.0;
    double[] randObj = NextBetaPrime(aVal, bVal, nPoints);
    double[] HistogramValues = makehistogram(randObj, xmin, xmax, nBins);
    double[] xdata = new double[nBins];
    double[] ydata = new double[nBins];
    double[] yCalcDistribution = new double[nBins];
    for (int i = 0; i < nBins; i++) {
        xdata[i] = xmin + (i + 0.5) * (xmax - xmin) / nBins;
        ydata[i] = HistogramValues[i];
        yCalcDistribution[i] = BetaPrimePDF(xdata[i], aVal, bVal);
    }
    double ydataMax = dataMax(ydata);
    double yCalcDistributionMax = dataMax(yCalcDistribution);
    Console.WriteLine("\nTesting Beta Probability Distribution");
    Console.WriteLine("\nkey: Bin number = *****. [随机分布]");
    Console.WriteLine("[计算分布]");
    for (int i = 0; i < nBins; i++) {
        Console.Write("Bin ({0}) = ", i + 1);
        for (int j = 0; j < Math.Round(ydata[i] * displayScaleFactor / ydataMax, 0); j++) 
            Console.Write("*");
        Console.WriteLine("{0}]", Math.Round(yCalcDistribution[i] * 100.0 / yCalcDistributionMax, 0));
    }

    Console.WriteLine("\n按 ENTER 继续...");
    Console.ReadLine();
    Console.Clear();
}
```

# C# 中的数值方法、算法与工具

结果：Beta 原始分布

键值：箱号 = ******* [随机分布] [计算分布]

| 箱号 | 随机分布 | 计算分布 |
| :--- | :--- | :--- |
| Bin 0 | ** | [8] [6] |
| Bin 1 | *********** | [37] [35] |
| Bin 2 | ********** | [55] [64] |
| Bin 3 | ***************** | [83] [84] |
| Bin 4 | ******************* | [87] [96] |
| Bin 5 | ********************* | [100] [100] |
| Bin 6 | ******************* | [88] [99] |
| Bin 7 | ****************** | [87] [94] |
| Bin 8 | ***************** | [81] [88] |
| Bin 9 | **************** | [73] [80] |
| Bin 10 | *************** | [75] [83] |
| Bin 11 | ***************** | [58] [65] |
| Bin 12 | ************ | [57] [58] |
| Bin 13 | ************ | [46] [52] |
| Bin 14 | ********** | [42] [46] |
| Bin 15 | ********* | [40] [40] |
| Bin 16 | ******** | [37] [36] |
| Bin 17 | ******* | [30] [31] |
| Bin 18 | ******* | [25] [28] |
| Bin 19 | ******* | [24] [24] |

# Cauchy 分布

柯西分布（也称为洛伦兹分布、Breit-Wigner 分布或洛伦兹函数）与共振行为研究密切相关的连续概率分布。在物理学中，共振是指系统在某些频率下比其他频率以更大幅度振动的倾向。这些被称为系统的共振频率。在共振频率下，小的周期驱动力即可导致大幅振动。共振现象在所有类型的振动或波中都会出现。例如，机械共振、声学共振、电磁共振、核磁共振 (NMR)、电子自旋共振 (ESR) 以及量子波函数的共振。共振系统可以产生特定频率的振动，或者从包含许多频率的复杂振动中提取出特定频率。柯西分布的主要特征总结如下 [65, 66, 49]：

参数：$a > 0, b > 0$
