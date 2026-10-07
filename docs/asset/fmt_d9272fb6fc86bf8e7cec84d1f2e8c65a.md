
```cpp
Fuzzy Fuzzy::operator % (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
        result._grades[i] = arg._grades[i]+ - _grades[i]*arg._grades[i];
    return result;
}
```

```cpp
Fuzzy Fuzzy::operator + (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        double rslt = _grades[i]+arg._grades[i];
        if(rslt < 1.0) result._grades[i] = rslt; else result._grades[i] = 1.0;
    }
    return result;
}
```

```cpp
Fuzzy Fuzzy::operator * (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
        result._grades[i] = _grades[i]*arg._grades[i];
    return result;
}
```

```cpp
Fuzzy Fuzzy::operator - (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        double rslt = _grades[i] + arg._grades[i] - 1.0;
        if(rslt > 0.0) result._grades[i] = rslt;
        else result._grades[i] = 0.0;
    }
    return result;
}
```

```cpp
Fuzzy Fuzzy::operator & (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        double g1 = _grades[i], g2 = arg.grades[i];
        double rslt;
        if(g1 < g2) rslt = _gamma*g1; else rslt = _gamma*g2;
        rslt += 0.5*(1.0-_gamma)+(g1+g2);
        result._grades[i] = rslt;
    }
    return result;
}
```

```cpp
Fuzzy Fuzzy::operator | (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        double g1 = _grades[i], g2 = arg.grades[i];
        double rslt;
        if(g1 > g2) rslt = _gamma*g1; else rslt = _gamma*g2;
        rslt += 0.5*(1-_gamma)+(g1+g2);
        result._grades[i] = rslt;
    }
    return result;
}
```

```cpp
Fuzzy Fuzzy::operator > (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        if(_grades[i] > arg.grades[i]) result[i] = 1.0;
        else result[i] = 0.0;
    }
    return result;
}
```

```cpp
Fuzzy Fuzzy::operator < (const Fuzzy& arg) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        if(_grades[i] < arg.grades[i]) result[i] = 1.0;
        else result[i] = 0.0;
    }
    return result;
}
```

```cpp
Fuzzy::operator == (const Fuzzy& arg) const
{
    Fuzzy result(size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        if(grades[i] == arg.grades[i]) result[i] = 1.0;
        else result[i] = 0.0;
    }
    return result;
}
```

```cpp
Fuzzy::operator >= (const Fuzzy& arg) const
{
    Fuzzy result(size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        if(grades[i] >= arg.grades[i]) result[i] = 1.0;
        else result[i] = 0.0;
    }
    return result;
}
```

```cpp
Fuzzy::operator <= (const Fuzzy& arg) const
{
    Fuzzy result(size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        if(grades[i] < arg.grades[i]) result[i] = 1.0;
        else result[i] = 0.0;
    }
    return result;
}
```

```cpp
Fuzzy::operator != (const Fuzzy& arg) const
{
    Fuzzy result(size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        if(grades[i] != arg.grades[i]) result[i] = 1.0;
        else result[i] = 0.0;
    }
    return result;
}
```

```cpp
void Fuzzy::greaterThan(const double& arg, double lambda)
{
    double range = _xMax-_xMin;
    if(lambda < 0.0) lambda = 0.1*range;
    double dx = range/(size-1);
    double x = _xMin;
    for(int i=0;i<size;i++)
    {
        _grades[i] = 1.0/(1.0+exp(-(x-arg)));
        x += dx;
    }
}
```

```cpp
void Fuzzy::lessThan(const double& arg, double lambda)
{
    double range = _xMax-_xMin;
    if(lambda <= 0.0) lambda = 0.1*range;
    double dx = range/(size-1);
    double x = _xMin;
    for(int i=0;i<size;i++)
    {
        _grades[i] = 1.0/(1.0+exp((arg-x)/lambda));
        x += dx;
    }
}
```

```cpp
void Fuzzy::closeTo(const double& arg, double sigma)
{
    double range = _xMax-_xMin;
    if(sigma <= 0.0) sigma = 0.1*range;
    double expDenom = 2.0*sigma*sigma;
    double dx = range/(size-1);
    double x = _xMin;
    for(int i=0;i<size;i++)
    {
        _grades[i] = exp(-pow(arg-x,2)/expDenom);
        x += dx;
    }
}
```

```cpp
Fuzzy::mean(const Fuzzy* fuzzy, const Fuzzy* sets, int nSets, const double* weights)
{
    const int size = sets[0]->size;
    Fuzzy result(sets[0]->size,sets[0]->xMin,sets[0]->xMax);
    for(int ng=0;ng<size;ng++)
    {
        double rslt = 0.0;
        for(int ns=0;ns<nSets;ns++)
        {
            if(weights[ns]) rslt += sets[ns]->grades[ng]*weights[ns];
            else rslt += sets[ns]->grades[ng];
        }
        if(weights[ng]) rslt /= nSets;
        result.grades[ng] = rslt;
    }
    return result;
}
```

```cpp
double Fuzzy::entropy(const double& base) const
{
    double result = 0.0;
    for(int ng=0;ng<size;ng++)
    {
        double grade = _grades[ng];
        if(grade) result -= grade*log(grade);
        grade = 1.0-grade;
        if(grade) result -= grade*log(grade);
    }
    return result/log(base);
}
```

```cpp
double Fuzzy::centroid() const // 使用梯形积分法
{
    double numer = (_xMin*_grades[size-1]+_xMax)/2.0;
    double denom = (_grades[0]+_grades[size-1])/2.0;
    double x = _xMin;
    for(int i=1;i<=size;i++)
    {
        x += _resolution;
        numer += x*_grades[i];
        denom += _grades[i];
    }
    return numer/denom; // 步长抵消
}
```

```cpp
Fuzzy Fuzzy::hedge(const double& hedgeExp) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++) result._grades[i] = pow(_grades[i],hedgeExp);
    return result;
}
```

```cpp
Fuzzy Fuzzy::enhanceContrast() const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
    {
        double grade = _grades[i];
        if(grade < 0.5) result._grades[i] = 2.0*pow(grade,2);
        else result._grades[i] = 1.0-2.0*pow(1-grade,2);
    }
    return result;
}
```

```cpp
Fuzzy Fuzzy::alphaCut(const double& alpha) const
{
    Fuzzy result(_size,_xMin,_xMax);
    for(int i=0;i<size;i++)
        if(_grades[i] >= alpha) result._grades[i] = 1.0;
        else result._grades[i] = 0.0;
    return result;
}
```

```cpp
Fuzzy Fuzzy::betaCut(const int beta) const
{
    // 实现
}
```

# 第 18 章 模糊集与模糊逻辑

```
Fuzzy optimalSpeed(201,0,200);
optimalSpeed.triangle(100,110,120);
optimalSpeed.limit(0.5);
```

集合 `optimalSpeed` 的隶属函数是一个顶点坐标为 (100.0), (105.0), (115.0), (120.0) 的梯形。`alphaCut` 和 `betaCut` 方法实现了 $\alpha$-切算和 $\beta$-切算子。`entropy` 方法估算模糊度。默认对数基数取 2。

`xMin()`、`xMax()` 和 `domainSize()` 是简单的查询函数，后者返回支持域的大小。由于这是离散集的实现，因此在支持域上具有有限的分辨率。可以通过 `resolution` 方法查询该分辨率率。如果调用 `isSubset` 方法的集合是作为参数传入集合的子集，则返回 `true`（即 1）。

我们提供了两个运算符来查询给定支持值的隶属度。第一个是数组元素运算符 `[]`，它接受索引作为参数。它简单地返回指定数组索引处支持值的隶属度，即离散化点。该运算符也可用于更改该点的隶属度。第二个运算符是函数调用运算符 `()`。该运算符可以查询 `xMin` 和 `xMax` 之间任何支持值的隶属度，而不仅仅是离散网格点。该方法使用线性插值来获取格点之间的隶属度。赋值运算符允许我们将一个模糊集赋值给另一个模糊集。它通过引用返回对象本身，以便允许连续的 C 风格赋值。

```
set1 = set2 = set3 = set4;
```

其余大部分运算符都是模糊集算子的直接实现。关系运算符

```
< > >= <= !=
```

每个运算符都返回一个清晰集（隶属度全为 0 或 1）。例如，大于运算符 `>` 返回一个模糊集，对于当前调用该方法的集合，其所有支持值比作为参数传入的集合具有更大的支持度。所有其他支持值的隶属度均为 0。关系运算符以类似的方式作用。

对于 `fuzzy-AND` 和 `fuzzy-OR` 算子，我们需要为 $\gamma$ 指定一个值。可以通过 `gamma` 和 `setGamma` 方法查询 $\gamma$ 的值。

输入/输出流运算符 `>>` 和 `<<` 用于从输入流（例如文件或键盘）读取模糊集，或向输出流（例如文件或屏幕）写入模糊集。

# 18. 模糊集的运算符

静态成员函数 `mean()` 计算一个模糊集数组的加权平均值。如果提供权重数组，则返回标准算术平均值。成员函数是静态的意味着可以在不引用类对象的情况下调用它。它实际上是一个具有类作用域的全局函数。我们可以如下调用它：

```
Fuzzy::mean(setsArray,weights);
```

注意，两个参数都是 `const` 的，即所有指针及其所指向的内容都声明为常量。

最后，我们实现了语言修饰符和对比增强。我们允许任何连续的修饰符值。为了引入语言修饰符，我们为以下术语定义了静态类常量：`extremely`（极其）, `very`（非常）, `substantially`（大幅）, `稍微`（略微）, `vaguely`（模糊地）。

可以使用定义语言概念 `large`（大），然后使用修饰符引入概念 `verylarge`（非常大）：

```
Fuzzy large(50);
large.large();
fuzzy veryLarge = large.hedge(Fuzzy::very);
```

**应用 1.** 下面的 C++ 程序 `mfuzzy.cpp` 示例了 `fuzzy.h` 文件中离散模糊类 `Fuzzy` 的用法。我们使用了以下文件 `fuzzy.dat`：

| 5 | 1 | 5 |

|---|---|---|

| 0.4 | 0.8 | 1.0 | 0.7 | 0.7 |

| 5 | 1 | 5 |

| 0.0 | 0.1 | 1.0 | 0.2 | 0.1 |

| 5 | 1 | 5 |

| 0.1 | 0.2 | 0.5 | 0.2 | 0.4 |
