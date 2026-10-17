
$\mu_{dil,\tilde{A}}(x) = (\mu_{\tilde{A}}(x))^{1/2}$

### 示例。
假设为模糊集 $\tilde{H}$ 选择以下隶属函数，对应词语*非常热*：

$\mu_{\tilde{H}}(T) = \frac{T}{40}, \quad T \in [0, 40]$。各种温度的隶度（真值程度）如下表所示：

| T | 0 | 5 | 10 | 15 | 20 | 25 | 30 | 35 | 40 |
|---|---|---|---|---|---|---|---|---|---|

| $\mu_{\tilde{H}}(T)$ | 0 | 0.125 | 0.25 | 0.375 | 0.5 | 0.625 | 0.75 | 0.825 | 1 |

该隶属函数将为 20°C 的温度给出 0.5 的隶度，30°C 给出 0.75，35°C 给出 0.825。*非常热*温度集给出更高的隶度。模糊集*非常热*的隶属函数通过使用模糊化从 $\tilde{H}$ 的隶属函数得到：

$\mu_{very\tilde{H}}(T) = (\mu_{\tilde{H}}(T))^2$。*非常*的隶度如下表所示：

| T | 0 | 5 | 10 | 15 | 20 | 25 | 30 | 35 | 40 |
|---|---|---|---|---|---|---|---|---|---|

| $\mu_{very\tilde{H}}(T)$ | 0 | 0.016 | 0.063 | 0.141 | 0.25 | 0.391 | 0.563 | 0.681 | 1 |

只有 35°C 和 40°C 的温度对于非常热有 0.6 的隶度，而 25°C、30°C、35°C 和 40°C 对于热都有 0.6 级别的隶度。模糊化限制（或压缩）了高温附近的模糊集。

模糊化的数学表达式为：

$\mu_{hedge\tilde{H}} = (\mu_{\tilde{H}})^\kappa$

其中 $\kappa > 1$ 用于压缩，$\kappa < 1$ 用于扩张。我们可以使用示例进行以下压缩和扩张的模糊化分配：

| | |
|---|---|
| vaguely | $\rightarrow$ 0.05 |
| slightly | $\rightarrow$ 0.25 |
| somewhat | $\rightarrow$ 0.5 |
| very | $\rightarrow$ 2 |
| extremely | $\rightarrow$ 3 |
| exactly | $\rightarrow$ $\infty$ |

另一个常用的模糊化是对比增强器：

$\mu_{enh\tilde{H}} = \begin{cases} 2(\mu_{\tilde{H}}(T))^2 & \text{for} \quad \mu_{\tilde{H}}(T) \in [0, 1/2] \\ 1 & \text{otherwise} \end{cases}$

### 18.3.6 量化模糊性

从信息论中我们知道可以通过香农熵定义概率分布的缺失信息：

$S(x) := -\sum_{x\in X} p(x)\log_{\alpha} p(x)$

其中对数的底 $\alpha$ 决定信息的单位。如果 $\alpha = 2$，信息的单位是 $bit$（二进制数字）。如果概率分布是 delta 函数，则缺失信息为 0，因为在这种情况下我们确定解是 $x_0$（概率为 1），因此没有缺失信息。同样，如果概率分布是平坦的，即

$p(x) = \frac{1}{size\ of\ X}$ 对于所有 $x$，则缺失信息最大。因此熵是模糊性的合适度量。

**示例。** 考虑以下离散模糊集：

$\tilde{A} = \{(1,0.4), (2,0.8), (3,1.0), (4,0.7), (5,0.3)\}$ 和

$\tilde{B} = \{(1,0.0), (2,0.1), (3,1.0), (4,0.2), (5,0.1)\}$ 则 $E_2(\tilde{A}) = 3.46$ bits，而 $E_2(\tilde{B}) = 1.66$ bits。正如我们预期的，$\tilde{A}$ 比 $\tilde{B}$ 模糊得多。

### 18.3.7 离散模糊集的 C++ 实现

在下面的头文件 `fuzzy.h` 中，我们将上述函数实现为类 `Fuzzy` 内部的方法。函数 `near` 被替换为 `closeTo`，因为 `near` 在 C++ 编译器中用作关键字。

```
// fuzzy.h
```
```cpp
#include <fstream>
#include <cmath> // for exp, log, pow
using namespace std;
```

## 18. 模糊集的运算符

```cpp
class Fuzzy
{
public:
    Fuzzy(); // 默认构造函数
    Fuzzy(const int size, const double& xMin=0, const double& xMax=1);
    Fuzzy(const Fuzzy& arg);
    void setDomain(const double& xMin, const double& xMax);
    void fillGrades(const double& fillValue);
    void normalize();
    void small(); void large();
    void rectangle(const double& left, const double& right);
    void triangle(const double& left, const double& center,
                  const double right);
    void trapezoid(const double& leftBot, const double& leftTop,
                  const double rightTop, const double& rightBot);
    // 模糊大于
    void greaterThan(const double& arg, const double lambda=0);
    // 模糊小于
    void lessThan(const double& arg, double lambda = 0);
    // 模糊接近
    void closeTo(const double& arg, double sigma = 0);

    int supportMaxGradeIndex() const;
    int supportMinGradeIndex() const;
    double supportMaxGrade() const; double supportMinGrade() const;
    double minGrade() const; double maxGrade() const;
    double centroid() const;
    double cardinality() const;
    double relativeCardinality() const;

    Fuzzy limit(const double& ceiling);
    Fuzzy alphaCut(const double& alpha) const;
    Fuzzy betaCut(const int beta) const;

    double entropy(const double& base = 2) const;
    double xMin() const { return _xMin; }
    double xMax() const { return _xMax; }
    double domainSize() const { return _domainSize; };
    double resolution() const { return _resolution; };

    int isSubset(const Fuzzy& arg) const;

    // 支持度 i 的隶度
    double& operator[](const int i); // 支持度 i 的隶度
    // 通过线性插值获取 x 处的隶度
    double operator()(const double& x) const;
```

## 第18 章 模糊集与模糊逻辑

```cpp
Fuzzy operator = (const Fuzzy arg); // 逻辑非
Fuzzy operator ! (const const&);
Fuzzy operator && (const Fuzzy arg) const; // 逻辑与
Fuzzy operator || (const Fuzzy arg) const; // 逻辑或
Fuzzy operator + (const Fuzzy arg) const; // 边界加
Fuzzy operator - (const Fuzzy arg) const; // 边界减
Fuzzy operator % (const Fuzzy arg) const; // 代数加
Fuzzy operator * (const Fuzzy arg) const; // 代数乘
Fuzzy operator & (const Fuzzy arg) const; // 模糊与
Fuzzy operator | (const Fuzzy arg) const; // 模糊或
Fuzzy operator < (const Fuzzy arg) const; // 小于
Fuzzy operator > (const Fuzzy arg) const; // 大于
Fuzzy operator == (const Fuzzy arg) const; // 等于
Fuzzy operator >= (const Fuzzy arg) const; // 大于等于
Fuzzy operator <= (const Fuzzy arg) const; // 小于等于
Fuzzy operator != (const Fuzzy arg) const; // 不等于
// 模糊与与模糊或
double gamma() { return _gamma; }
void setGamma(const double& newGamma) { _gamma = newGamma; }
// 模糊集数组的加权平均值
// 如果省略 arg权重，则使用普通平均值
static Fuzzy mean(const Fuzzy* const * const sets, int nSets,
const double* weights = NULL);

Fuzzy enhanceContrast(const double&);
Fuzzy hedge(const double& hedgeExp) const;
// 模糊算子常量:
static const double extremely;
static const double very;
static const double substantially;
static const double somewhat;
static const double slightly;
static const double vagely;

friend ostream& operator << (ostream&,const Fuzzy&);
friend ostream& operator >> (istream&,Fuzzy&);

public:
double* grades;
int _size;
double _gamma; // 用于模糊与和模糊或。
double _xMin, _xMax, _resolution, _domainSize;
void resize(const int newSize);

private:
// gamma 参数的默认值
static const double _defaultGamma;
double linearInterpolate(const double& x0,const double& y0,
```

## 18.. 模糊集的运算符

```cpp
const double& x1,const double& y1,
const double& x) const;
};
```
```cpp
// 静态类常量
const double Fuzzy::_defaultGamma = 0.5;
// 模糊算子指数:
const double Fuzzy::_extremely = 4.0;
const double Fuzzy::_very = 2.0;
const double Fuzzy::_substantially = 1.5;
const double Fuzzy::_somewhat = 0.5;
const double Fuzzy::_slightly = 0.25;
const double Fuzzy::_vaguely = 0.03;
```

```cpp
// 实现
Fuzzy::Fuzzy() : _gamma(_defaultGamma),_grades(NULL),_size
{ setDomain(0,1); }
```

```cpp
Fuzzy::Fuzzy(const int size,const double& xMin,const double& xMax)
: _gamma(_defaultGamma),_grades(NULL),_size(0)
{ resize(size); setDomain(xMin,xMax); }
```

```cpp
Fuzzy::Fuzzy(const Fuzzy& arg)
: _gamma(_defaultGamma),_grades(NULL),_size(0) { *this=arg; }
```

```cpp
void Fuzzy::setDomain(const double& xMin,const double& xMax)
{
_xMin = xMin,_xMax = xMax;
_domainSize = xMax-xMin;
if(_size != 1)_resolution = _domainSize/(_size-1.0);
else _resolution = 1.0;
}
```

```cpp
void Fuzzy::fillGrades(const double& fillValue)
{ for (int i=0;i<size;i++)_grades[i] = fillValue; }
```

```cpp
void Fuzzy::normalize()
{
double max = maxGrade();
for(int i=0;i<size;i++)_grades[i] /= max;
}
```

```cpp
void Fuzzy::large()
{
double range = xMax-xMin;
double slope = (double)1/range;
double intercept = -slope*xMin;
double dx = range/(_size-1.0);
}
```

```cpp
void Fuzzy::small()
{
double range = xMax-xMin;
double slope = (double)1/range;
double intercept = -slope*xMax;
double dx = range/(_size-1.0);
}
```

```cpp
void Fuzzy::rectangle(const double& left,const double& right)
{
double range = xMax-xMin;
double slope = (double)1/range;
double intercept = -slope*left;
double dx = range/(_size-1.0);
}
```

```cpp
void Fuzzy::triangle(const double& left,const double& center,
const double& right)
{
double range = xMax-xMin;
double slope = (double)1/range;
double intercept = -slope*center;
double dx = range/(_size-1.0);
}
```

```cpp
void Fuzzy::trapezoid(const double& leftBot,const double& leftTop,
const double& rightTop, const double& rightBot)
{
double range = xMax-xMin;
double slope = (double)1/range;
double intercept = -slope*leftTop;
double dx = range/(_size-1.0);
}
```

### 18.3. 模糊集运算符

```cpp
Fuzzy Fuzzy::operator || (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
        if(_grades[i] > arg._grades[i]) result._grades[i] = _grades[i];
        else result._grades[i] = arg._grades[i];
    return result;
}
```
