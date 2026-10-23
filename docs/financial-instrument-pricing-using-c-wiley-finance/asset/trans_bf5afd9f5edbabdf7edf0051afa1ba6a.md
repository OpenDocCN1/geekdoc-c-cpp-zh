

我们应用了单例设计模式（GOF, 1995）在上述代码中创建 Excel 驱动的全局实例。也可以使用以下代码创建实例：

```
ExcelDriver xl; xl.MakeVisible(true);
```

默认情况下，Excel 以不可见模式启动。因此，如果你希望在屏幕上看到数据，可以调用此后者方法。

## 14.4.2 使用标签显示矩阵

在某些情况下，我们可能希望在将矩阵呈现在 Excel 中之前先对其行和列进行注释。此功能提高了所显示数据的可读性和可理解性。一般而言，标签值能更清楚地说明数据的含义。此功能在创建查找表时很有用，例如。

我们举一个例子。首先，我们创建行和列标签：

// Labels for rows and columns of the Excel matrix.
// Only labelled values are printed!!
std::list<std::string> rowLabels{"A","B","C","D","E", "F","K","L"};
std::list<std::string> colLabels{"C1", "C2", "C3", "C4","C5"};

std::string sheetName2("Matrix Labels Case");

ExcelDriver& excel = ExcelDriver::Instance();
excel.MakeVisible(true);            // Default is INVISIBLE!
```

我们现在使用与图 14.1 相同的矩阵数据，使用以下代码呈现带注释的矩阵：

```
long rowPos = 4; long colPos = 3;
excel.AddMatrix<NumericMatrix>(matrix, sheetName2, rowLabels,
colLabels, rowPos, colPos);
```

输出显示在图 14.2 中。

|   | C1 | C2 | C3 | C4 | C5 |   |   |
|---|---|---|---|---|---|---|---|
| A | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| B | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| C | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| D | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| E | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| F | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| K | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| L | 7 | 8 | 9 | 10 | 11 | 12 | 13 |

**图 14.2** 带注释的测试用例 101 矩阵

我们强调，在软件的当前版本中，只有带标签的行才会被显示。在大多数情况下，我们会确保标签的数量与相应的矩阵维度相同，以便查看所有数据。因此我们可以看到，图 14.2 中并非所有图 14.1 中的行都可见。你需要意识到这一事实。

## 14.4.3 查找表、连续函数和离散函数

一个常见的用例是当我们对一元和二元的实值函数进行离散化时。聚焦于后一种情况，我们创建两个离散网格数组，并计算这些点上的函数值。这些值将成为矩阵中的值。作为示例，我们以方便的方式离散化如下定义的二元正态概率密度函数（相关变量为全局）：

```
double rho = 0.5;
double NormalPdf2d(double x, double y)
{ // Bivariate normal density function

double fac= 1.0/(2.0 * 3.14159265359 * std::sqrt(1.0 - rho*rho));
double t = x*x - 2.0*rho*x*y + y*y;
t /= 2.0 * (1.0 - rho*rho);

return fac * std::exp(-t);
}
```

为了离散化此函数，我们使用以下实用函数：

```
template <typename Matrix>
Matrix CreateDiscreteFunction2d(const std::vector<double>& x ,
const std::vector<double>& y,
const std::function<double (double x, double y)>& f)
{ // Create a discrete function from a continuous function m = f(x,y)

std::size_t nr = x.size();
std::size_t nc = y.size();

Matrix m(nr,nc);

for (std::size_t i = 0; i < nr; ++i)
{
for (std::size_t j = 0; j < nc; ++j)
{
m(i, j) = f(x[i],y[j]);
}
}

return m;
}
```

此代码可以并行化，如第 28 章至第 30 章所述。

一个可能更有趣的用例是当我们希望将一个或多个向量作为折线图显示以可视化它们时。这是下一节的主题。

## 14.5.1 单曲线和多曲线

我们有两个函数来显示向量。第一个函数显示一组向量，而第二个函数显示单个向量。接口如下：

// Create chart with a number of functions. The arguments are:
// x:              std::vector<double> with input values
// labels:         labels for output values
// vectorList:     list of vectors with output values.
// chartTitle:     title of chart
// xTitle:         label of x axis
// yTitle:         label of y axis
void CreateChart(const std::vector<double> & x,
                const std::list<std::string> & labels,
                const std::list<std::vector<double>> & vectorList,
                const std::string& chartTitle,
                const std::string& xTitle = "X",
                const std::string& yTitle = "Y");
```

```
// Create chart with a number of functions. The arguments are:
// x:              std::vector<double> with input values
// y:              std::vector<double> with output values.
// chartTitle:     title of chart
// xTitle:         label of x axis
// yTitle:         label of y axis

void CreateChart(const std::vector<double> & x,
                const std::vector<double>& y,
                const std::string& chartTitle,
                const std::string& xTitle = "X",
                const std::string& yTitle = "Y");
```

使用这些函数与第 14.4 节采用的方法类似。我们首先考虑函数 f(x) = x² 的情况。注意，将其定义为存储的 lambda 函数 fun 很方便：

```
long N = 40;

// Create abscissa x array
double A = 0.0; double B = 10.0;
auto x = CreateMesh(N, A,B);

auto fun = [](double x) { return x*x; };
auto vec1 = CreateDiscreteFunction< std::vector<double>>(x, fun);

ExcelDriver xl; xl.MakeVisible(true);
xl.CreateChart(x, vec1, "Test 101 curve");
```

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_456_0.png)

输出显示在图 14.4 中。

在 Excel 表中显示多条曲线的情况下，我们首先定义多个函数，然后将它们各自转换为向量（离散函数）。最后，我们将每个向量附加到一个列表中并调用适当的驱动函数：

```
long N = 40;

// Create abscissa x array
double A = 0.0; double B = 3.0; // Interval
auto x = CreateMesh(N, A, B);

auto fun = [](double x) { return std::log(x + 0.01); };
auto fun2 = [](double x) { return x*x; };
auto fun3 = [](double x) { return x*x*x; };
auto fun4 = [](double x) { return std::exp(x); };
auto fun5 = [](double x) { return x; };

auto vec1 = CreateDiscreteFunction< std::vector<double> >(x, fun);
auto vec2 = CreateDiscreteFunction< std::vector<double> >(x, fun2);
auto vec3 = CreateDiscreteFunction< std::vector<double> >(x, fun3);
auto vec4 = CreateDiscreteFunction< std::vector<double> >(x, fun4);
auto vec5 = CreateDiscreteFunction< std::vector<double> >(x, fun5);
// Now Excel output in one sheet for comparison purposes

// Names of each vector
std::list<std::string> labels
{ "log(x+0.01)", "x^2", "x^3", "exp(x)", "x" };
```

**比较函数**

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_457_0.png)

**图 14.5** 多条曲线

```
// The list of Y values using uniform initialisation
std::list<std::vector<double> > curves{ vec1, vec2, vec3, vec4, vec5 };

std::cout << "Data has been created\n";

ExcelDriver xl; xl.MakeVisible(true);
xl.CreateChart(x, labels, curves, "Comparing Functions", "x", "y");
```

输出显示在图 14.5 中。
为完整起见，我们展示了从函数创建值向量和矩阵的代码：

```
template <typename Vector>
    Vector CreateDiscreteFunction(const std::vector<double>& x,
                                    const std::function<double(double)>& f)
{ // Create a discrete function from a continuous function y = f(x)

    Vector y(x.size());

    for (std::size_t j = 0; j < y.size(); ++j)
    {
        y[j] = f(x[j]);
    }

    return y;
}

template <typename Matrix>
Matrix CreateDiscreteFunction2d(const std::vector<double>& x ,
    const std::vector<double>& y,
    const std::function
        <double (double x, double y)>& f)
{ // Create a discrete function from a continuous function m = f(x,y)

std::size_t nr = x.size();
std::size_t nc = y.size();

Matrix m(nr,nc);

for (std::size_t i = 0; i < nr; ++i)
{
    for (std::size_t j = 0; j < nc; ++j)
    {
        m(i, j) = f(x[i],y[j]);
    }
}

return m;
}
```

## 14.6 随机微分方程的路径生成

前几节中的通用示例被选用来展示 Excel 驱动的工作原理，而不会陷入软件设计决策或数学高级讨论。在本节中，我们采用与计算金融相关的示例。为此，我们模拟由 SDE 定义的量的路径。在大多数情况下，解析解不存在，我们必须求助于数值近似，在此情况下为有限差分法。

我们现在讨论一些用于计算以下非线性自治 SDE 路径的格式：

dX(t) = μ(X(t))dt + σ(X(t))dW(t)    0 < t ≤ T
X(0) = A.                                    (14.1)

一些有限差分格式为：

- 显式欧拉：

  Xₙ₊₁ = Xₙ + μₙΔt + σₙΔWₙ

  其中 μₙ = μ(Xₙ)，σₙ = σ(Xₙ)。                                    (14.2)

