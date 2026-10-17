
```csharp
enum BiasType { Biased, Unbiased };
static double Variance(double[] data, BiasType type)
{
    double sum = 0.0d;
    for (int i = 0; i < data.Length; i++)
    {
        sum += data[i];
    }
    double mean = sum / data.Length;
    for (int i = 0; i < data.Length; i++)
    {
        sum += Math.Pow(data[i] - mean, 2);
    }
    double variance;
    if (type == BiasType.Biased)
    {
        variance = sum / data.Length;
    }
    else
    {
        variance = sum / (data.Length - 1);
    }
    return variance;
}
```

```csharp
public static double StandardDeviation(double[] data)
{
    return Math.Sqrt(Variance(data, BiasType.Unbiased));
}
```

```csharp
static double StandardDeviation(double[] data, BiasType btype)
{
    return Math.Sqrt(Variance(data, btype));
}
```

### 13.3.11 关于均值的矩

在统计学中，实值变量 `x` 的 `k` 阶中心矩 `μ_k` 定义为

$$\mu_k = E(x - E(x))^k = \frac{1}{N} \sum_{i=1}^{N} (x_i - \overline{x})^k$$

`E(x)` 是 `x` 的期望值。

少数中心矩具有熟悉且直观的解释。第一阶中心矩等于零。关于均值的二阶中心矩称为方差。三阶中心矩称为偏度。四阶中心矩称为峰度。在此之后，它被称为第 `k` 阶矩。下面显示了计算指定阶 `k` 中心矩的建议 C# 代码。

```csharp
public static double CentralMoment(double[] data, int k)
{
    double sum = 0.0d;
    for (int i = 0; i < data.Length; i++)
    {
        sum += data[i];
    }
    double mean = 0.0d;
    for (int i = 0; i < data.Length; i++)
    {
        sum += Math.Pow((data[i]-mean),k);
    }
    return sum/data.Length;
}
```

### 13.3.2 偏度

偏度是分布不对称程度的度量。它与分布的三阶中心矩 `μ_3` 的归一化形式相关。对于包含 `N` 个值的样本，样本偏度由公式给出

$$g_1 = \frac{\frac{1}{N}\sum_{i=1}^{N}(x_i-\bar{x})^3}{(\frac{1}{N}\sum_{i=1}^{N}(x_i-\bar{x})^2)^{3/2}}$$

如果左尾（分布的末端）比右尾（分布大端的尾）长，则该函数具有负偏度。如果反相反，则具有正偏度。如果两者相等，则具有零偏度。与方差和标准差计算与分布的二阶中心矩 `μ_2` 的归一化形式相关一样，偏度也取决于它是偏的还是无偏的。下面的 C# 代码根据指定的偏类型计算给定数据的偏度。

```csharp
static double Skewness(double[] data, BiasType type)
{
    if (data.Length < 3)
    {
        throw new Exception("偏度至少\nat三个元素.*");
    }
    // 计算均值
    double sum = 0.0d;
    for (int i = 0; i < data.Length; i++)
    {
        sum += data[i];
    }
    double mean = sum / data.Length;
    // 三阶和二阶矩
    double second = 0.0d;
    double third = 0.0d;
    double deviation;
    for (int i = 0; i < data.Length; i++)
    {
        deviation = data[i] - mean;
        second += (deviation * deviation);
        third = Math.Pow(deviation, 3);
    }
    // 标准化矩
    double variance;
    if (type == BiasType.Biased)
    {
        variance = second / data.Length;
    }
    else{
        variance = second / (data.Length - 1);
    }
    double standardizedMoment=third/Math.Pow(Math.Sqrt(variance),3);
    // 偏度
    double d = (double)data.Length;
    double skewness;
    if (type == BiasType.Unbiased)
    {
        skewness = (d/(d-1)*(d-2))*standardizedMoment;
    }
    else{
        skewness = standardizedMoment / d;
    }
    return skewness;
}
```

### 13.3.13 峰度

峰度衡量实值变量分布的尖峰程度。它与分布的四阶中心矩 `μ_4` 的归一化形式相关。对于包含 `N` 个值的样本，峰度由公式给出

$$g_2 = \frac{\sum_{i=1}^{N} (x_i - \bar{x})^4}{(\sum_{i=1}^{N} (x_i - \bar{x})^2)^2}$$

高峰度意味着更多的方差来自于极端偏差而非频繁的偏差。高峰度分布具有更尖的峰和更长的尾部，而低峰度分布具有更圆的峰和更细的尾部。与方差和标准差计算与分布二阶中心矩 `μ_2` 的归一化形式相关，峰度也取决于它是偏的还是无偏的。下面的 C# 代码根据偏类型计算给定数据的峰度。

```csharp
static double Kurtosis(double[] data, BiasType type)
{
    if (data.Length < 4)
    {
        throw new Exception("峰度需要四个元素");
    }
    // 均值
    double sum = 0.0d;
    for (int i = 0; i < data.Length; i++)
    {
        sum += data[i];
    }
    double mean = sum / data.Length;

    // 四阶和二阶矩
    double second = 0.0d;
    double fourth = 0.0d;
    double deviation;
    for (int i = 0; i < data.Length; i++)
    {
        deviation = data[i] - mean;
        second += (deviation * deviation);
        fourth += Math.Pow(deviation, 4);
    }

    // 标准化矩
    double variance;
    if (type == BiasType.Biased)
    {
        variance = second / data.Length;
    }
    else {
        variance = second / (data.Length - 1);
    }
    double standardizedMoment=fourth/(variance*variance);

    // 峰度
    double d = (double)data.Length;
    double kurtosis;
    if (type == BiasType.Unbiased)
    {
        double term1 = d*(d+1);
        double term2 = (d-1)*(d-2);
        double term3 = 3*(d-3)/((d-2)*(d-3));
        kurtosis = ((term1/term2)*standardizedMoment)-term3;
    }
    else {
        kurtosis = (standardizedMoment/d);
    }
    return kurtosis;
}
```

### 13.3.14 协方差和相关性

协方差提供了两个或多个实值变量之间相关性的度量。两个随机变量 `X` 和 `Y`（样本量为 `N`，期望值 `E(X) = μ_X` 和 `E(Y) = μ_Y`）之间的协方差定义为

$$Cov(X, Y) = E((X - \mu_X)(Y - \mu_Y)) = \frac{1}{N} \sum (x_i - \bar{x})(y_i - \bar{y})$$

`E` 是期望值。对于不相关的变量，`Cov(X,Y) = 0`。然而，如果变量以某种方式相关，如果 `cov(X,Y) > 0`，则 `Y` 随 `X` 的增加而增加；`cov(X,Y) < 0`，则 `Y` 随 `X` 的增加而减少。注意，统计上独立的变量总是不相关的，反之并非如此。在 `X = Y` 的特殊情况下，`Cov(X,Y)` 可以很容易简化为 `σ_X^2`，因此协方差简化为通常的方差 `σ_X^2 = Var(X)`。这符号符号 `σ_{XY} = Cov(X,Y)` 提供了一种表示方差 `σ_{XX} = σ_X^2` 的一致方法，其中 `σ_X` 是标准差。因此，派生量

$$Cor(X, Y) = \frac{\sigma_{XY}}{\sigma_X \sigma_Y}$$

计算协方差的代码所示。

```csharp
static double Covariance(double[] datal, double[] data2, BiasType type)
{
    if (datal.Length != data2.Length)
    {
        throw new Exception("测试的两个数据集大小不同");
    }
    if (datal.Length == 0)
    {
        throw new Exception("协方差方法中的数据长度为零");
    }
    // 求和
    double sum1 = 0.0d;
    double sum2 = 0.0d;
    for (int i = 0; i < datal.Length; i++)
    {
        sum1 += datal[i];
        sum2 += data2[i];
    }

    // 均值
    double mean1 = sum1 / datal.Length;
    double mean2 = sum2 / data2.Length;

    // 协方差
    double total = 0.0d;
    for (int i = 0; i < datal.Length; i++)
    {
        total += (datal[i] - mean1) * (data2[i] - mean2);
    }
    return total / datal.Length;
}
```

# C# 中的数值方法、算法与工具

```csharp
{
  total += ((data1[i] - mean1) * (data2[i] - mean2));
}
if type == BiasType.Biased {
  return total / data1.Length;
} else {
  return total / (data1.Length - 1);
}
```

计算相关性的 C 代码如下所示。

```csharp
static double Correlation(double[] data1, double[] data2) {
  if (data1.Length != data2.Length) {
    throw new Exception("The two data sets being tested are of different sizes");
  }
  if (data1.Length == 0) {
    throw new Exception("Data correlation method has zero length.");
  }
  if (data1.Length == 1) {
    throw new Exception("Single data point is insufficient for correlation.");
  }
  // Sum
  double sum1 = 0.0d;
  double sum2 = 0.0d;
  for (int i = 0; i < data1.Length; i++) {
    sum1 += data1[i];
    sum2 += data2[i];
  }
  // Mean
  double mean1 = sum1 / data1.Length;
  double mean2 = sum2 / data2.Length;
  // Covariance
  double total = 0.0d;
  for (int i = 0; i < data1.Length; i++) {
    total += ((data1[i] - mean1) * (data2[i] - mean2));
  }
  double covariance = total / data1.Length;
  // Standard deviation
  double sum1 = 0.0d;
  double sum2 = 0.0d;
  for (int i = 0; i < data1.Length; i++) {
    sum1 += ((data1[i] - mean1) * (data1[i] - mean1));
    sum2 += ((data2[i] - mean2) * (data2[i] - mean2));
```

# 统计函数

```csharp
}
double stdev1 = Math.Sqrt(sum1 / data1.Length);
double stdev2 = Math.Sqrt(sum2 / data2.Length);
if ((stdev1 * stdev2) == 0)
{
    throw new Exception("One of the standard deviations is zero");
    return (covariance / (stdev1 * stdev2));
}
```

# 13.3.15 杂项工具类

某些统计计算（例如确定百分位数或排名的计算）通常需要一些辅助计算，以支持提取所需的信息。因此，下面列出了以下自解释的工具程序，用以支持后文描述的进一步示例。

```csharp
// 计算给定数据集中的最小值
public static double minValue(double[] data)
{
    double minimum = data[0];
    double d;

    for (int i = 1; i < data.Length; i++)
    {
        d = data[i];
        if (d < minimum )
        {
            minimum = d;
        }
    }
    return minimum;
}

// 计算给定数据集中的最小绝对值
public static double minAbsValue(double[] data)
{
    double minimum = Math.Abs(data[0]);
    double d;

    for (int i = 1; i < data.Length; i++)
    {
        d = Math.Abs(data[i]);
        if (d < minimum )
        {
            minimum = d;
        }
    }
    return minimum;
}
```
