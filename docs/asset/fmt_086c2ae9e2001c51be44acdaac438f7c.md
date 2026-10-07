
结果：指数概率分布
键值：箱体数 = ***** [随机分布] [计算分布]

| 箱体数 | 随机 | 计算 |
| :--- | :--- | :--- |
| Bin 0 | ***************** [100] | [100] |
| Bin 1 | ***************** [73] | [74] |
| Bin 2 | ************ [54] | [55] |
| Bin 3 | ******** [40] | [41] |
| Bin 4 | ****** [31] | [30] |
| Bin 5 | ******* [20] | [22] |
| Bin 6 | **** [16] | [17] |
| Bin 7 | *** [12] | [12] |
| Bin 8 | ** [9] | [9] |
| Bin 9 | ** [7] | [7] |
| Bin 10 | * [4] | [5] |
| Bin 11 | * [3] | [4] |
| Bin 12 | * [3] | [3] |
| Bin 13 | * [2] | [2] |
| Bin 14 | * [2] | [1] |
| Bin 15 | * [1] | [1] |
| Bin 16 | * [1] | [1] |
| Bin 17 | * [1] | [1] |
| Bin 18 | * [1] | [0] |
| Bin 19 | * [0] | [0] |

# 极值分布

极值理论是负责研究分布中极端离值的统计学分支。因此，极值理论对于评估极少数事件（如百年一遇的洪水）至关重要。极值分布通常包含以下族类：

- 类型 1：Gumbel 分布。
- 类型 2：Frechet 分布。
- 类型 3：Weibull 分布。

类型 1 极值分布（Gumbel 分布）的关键特征总结如下 [66]。

参数：$-\infty < \mu < \infty, \sigma > 0$

PDF：$f(x) = \frac{1}{\sigma}\exp(-\frac{x-\mu}{\sigma})\exp(-\exp(-(x-\mu)/\sigma))$

给定从均匀分布 $u(0,1)$ 中抽取的随机变量 $u$，变量 $X = \mu - \sigma\log(u)$ 符合参数为 $\mu$ 和 $\sigma$ 的 Gumbel 分布。下面的代码阐示了如何在 C# 中实现极值分布（Gumbel 类型）：

```csharp
public static double ExponentialPDF(double x, double mu, double sigma)
{
    double w = (x-mu)/sigma;
    return (1.0/sigma) * Math.Exp(-w) * Math.Exp(-Math.Exp(-w));
}
```

```csharp
public static double[] ExtremeValuePDF(double[] x, double mu, double sigma)
{
    double[] tempArr = new double[x.Length];
    for (int i = 0; i < x.Length; i++)
    {
        tempArr[i] = ExtremeValuePDF(x[i], mu, sigma);
    }
    return tempArr;
}
```

```csharp
public static double NextExtremeValue(double mu, double sigma)
{
    return (mu - \sigma*Math.Log(-Math.Log(randObj.NextDouble())));
}
```

## 346 C# 中的数值方法、算法与工具

```csharp
public static double[] NextExtremeValue(double mu, double sigma, int nLen)
{
    double[] tempArr = new double[nLen];
    for (int i = 0; i < nLen; i++)
    {
        tempArr[i] = NextExtremeValue(mu, sigma);
    }
    return tempArr;
}
```

```csharp
static void TestExtremeValue()
{
    int nBins = 20;
    int nPoints = 10000;
    double xmin = -4;
    double xmax = 8;
    double muVal = 1.0;
    double sigmaVal = 0.750;
    double yScaleFactor = 500.0;
    double[] randObj = NextExtremeValue(mu, sigmaVal, nPoints);
    double[] HistogramValues = makeHistogram(randObj, xmin, xmax, nBins);
    double[] xdata = new double[nBins];
    double[] ydata = new double[nBins];
    double[] yCalcDistribution = new double[nBins];
    for (int i = 0; i < nBins; i++)
    {
        xdata[i] = xmin + (i + 0.5) * (xmax - xmin) / nBins;
        ydata[i] = (double)HistogramValues[i];
        yCalcDistribution[i] = ExtremeValuePDF(xdata[i], muVal, sigmaVal);
    }
    double ydataMax = dataMax(ydata);
    double yCalcDistributionMax = dataMax(yCalcDistribution);
    Console.WriteLine("\n正在测试极值概率分布");
    Console.WriteLine("\n图例：箱号 = *****. [随机分布] [计算分布].");
    for (int i = 0; i < nBins; i++)
    {
        // ... 打印逻辑
    }
    Console.WriteLine("\n按回车键继续...");
    Console.ReadLine();
    Console.Clear();
}
```

# 随机数值概率分布

结果：极值概率分布
图例：箱号 = *****... [随机分布] [计算分布]

| 箱号 | 随机 | 计算 |
| :--- | :--- | :--- |
| 箱 0 | [0] | [0] |
| 箱 1 | [0] | [0] |
| 箱 2 | [0] | [0] |
| 箱 3 | [0] | [0] |
| 箱 4 | [0] | [0] |
| 箱 5 | [0] | [0] |
| 箱 6 | **** [17] | [16] |
| 箱 7 | *************** [77] | [76] |
| 箱 8 | *************** [100] | [73] |
| 箱 10 | ********** [40] | [21] |
| 箱 11 | ***** [20] | [20] |
| 箱 12 | ** [10] | [9] |
| 箱 13 | * [5] | [4] |
| 箱 14 | * [2] | [2] |
| 箱 15 | [1] | [1] |
| 箱 16 | [0] | [0] |
| 箱 17 | [0] | [0] |
| 箱 18 | [0] | [0] |
| 箱 19 | [0] | [0] |

# 伽分布

伽分布本质上是 Erlang 分布的推广。与指数分布和 Erlang 分布一样，伽分布也用于某些排队网络的建模。伽分布的关键特征总结如下 [65, 66, 49]。

参数：$a > 0, b > 0$

$PDF: f(x) = \begin{cases} \frac{a^b x^{b-1} e^{-ax}}{\Gamma(b)} & \text{if } 0 \leq x < \infty \\ 0 & \text{if } x < 0 \end{cases}$

给定一个从均匀分布 $u[0, 1]$ 中抽取的随机变量 $u$，变量

$X = -\frac{1}{a} \sum_{i=1}^b \log u_i$

是一个参数为 $a$ 和 $b$ 的伽分布。下面的代码演示了如何在 C# 中实现伽分布。

```csharp
public static double Gamma(double x, int b, double a)
{
    return Math.Pow(a, b) * Math.Pow(x, b - 1) * Math.Exp(-a * x) / Gamma(b);
}
```

## 348 C# 中的数值方法、算法与工具

```csharp
public static double[] GammaPDF(double[] x, int b, double a)
{
    double[] tempArray = new double[x.Length];
    for (int i = 0; i < x.Length; i++)
    {
        tempArray[i] = GammaPDF(x[i], b, a);
    }
    return tempArray;
}
```

```csharp
public static double NextGamma(int b, double a)
{
    double temp = 0.0;
    for (int i = 0; i < b; i++)
    {
        temp += -Math.Log(randObj.NextDouble()) / a;
    }
    return temp;
}
```

```csharp
public static double[] NextGamma(int b, double a, int nLen)
{
    double[] tempArray = new double[nLen];
    for (int i = 0; i < nLen; i++)
    {
        tempArray[i] = NextGamma(b, a);
    }
    return tempArray;
}
```

```csharp
static void TestGamma()
{
    int nBins = 20; int nPoints = 10000;
    double xmin = 0.0; double xmax = 15.0;
    double aVal = 0.6; int bVal = 2;
    double displayScaleFactor = 500.0;
    double[] randObj = NextGamma(bVal, aVal, nPoints);
    makeHistogram(randObj, xmin, xmax, nBins);
    double[] xdata = new double[nBins];
    double[] ydata = new double[nBins];
    double[] yCalcDistribution = new double[nBins];
    for (int i = 0; i < nBins; i++)
    {
        xdata[i] = xmin + (i + 0.5) * (xmax - xmin) / nBins;
        ydata[i] = (double)HistogramValues[i];
        yCalcDistribution[i] = GammaPDF(xdata[i], bVal, aVal);
    }
    double ydataMax = dataMax(ydata);
    double yCalcDistributionMax = dataMax(yCalcDistribution);
    Console.WriteLine("\n正在测试伽概率分布");
    Console.WriteLine("\n图例：箱号 = *****. [随机分布] [计算分布].");
    for (int i = 0; i < nBins; i++)
    {
        // ... 打印逻辑
    }
}
```

# 365 随机数

拉普拉斯分布（Laplace distribution）是一种由两个指数分布组成的连续概率分布。拉普拉斯分布的一个主要特征是与正态分布相比具有更尖锐的峰值和更重的尾部。

```csharp
for (int j = 0; j < nBins; j++)
{
    ydata[j] = (double)HistogramValues[j];
    yCalcDistribution[j] = LaplacePDF(xdata[j], sigmaVal);
}
// ...
Console.WriteLine("\n按回车键继续...");
Console.ReadLine();
Console.Clear();
```

# 随机数

结果：拉普拉斯概率分布
键：箱数 = *****... [随机分布.]

- Bin 0 = * [4] [4]
- Bin 1 = ** [5] [6]
- Bin 2 = *** [8] [8]
- Bin 3 = **** [12] [12]
- Bin 4 = ***** [17] [17]
- Bin 5 = ****** [24] [24]
- Bin 6 = ******* [38] [35]
- Bin 7 = ********* [47] [49]
- Bin 8 = ************ [68] [70]
- Bin 9 = ***************** [93] [98]
- Bin 10 = ******************* [99] [100]
- Bin 11 = ***************** [71] [70]
- Bin 12 = ******************* [49] [49]
- Bin 13 = *********************** [33] [35]
- Bin 14 = ******************** [26] [24]
- Bin 15 = ********************* [17] [17]
- Bin 16 = ********************** [13] [12]
- Bin 17 = *********************** [8] [8]
- Bin 18 = ******************** [5] [6]
- Bin 19 = ********************************** [4] [4]

# C# 中的数值方法、算法和工具

# 逻辑斯分布

逻辑斯分布已应用于许多不同的领域。例如，在生物学中，它被用于模拟某些物种在竞争中的增长。在流行病学中，它被用于模拟疾病的传播。逻辑斯分布的主要特征总结如下 [66]。

参数：-∞ < a < ∞ 和 b > 0

范围：-∞ < x < ∞

```
PDF: $f(x) = \frac{\exp(\frac{x-a}{b})}{b(1+\exp(\frac{x-a}{b}))}$
```

使用逆变换法，我们可以得到一个从逻辑斯分布中生成随机变量 X 的方程，如下所示。

```
$X = a+b \log(\frac{u}{1-u})$
```

其中 **u** 是从均匀分布 u[0, 1] 中抽取的随机变量。以下代码演示了如何在 C# 中实现逻辑斯分布。

```sharp
public static double LogisticPDF(double x, double b, double a)
{
    return Math.Exp(-(x-a)/b)/Math.Pow((1.0+Math.Exp(-(x-a)/b)),2.0);
}
```

```sharp
public static double[] NextLogistic(double[] x, double b, double a)
{
    double[] tempArr = new double[x.Length];
    for (int i = 0; i < x.Length; i++)
    {
        tempArr[i] = LogisticPDF(x[i], b, a);
    }
    return tempArr;
}
```

```sharp
public static double NextLogistic(double b, double a)
{
    double u = randObj.NextDouble();
    return a + b * Math.Log(u / (1 - u));
}
```

```sharp
public static double[] NextLogistic(double b, double a, int nLen)
{
```
