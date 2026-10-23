

```
std::cout << "MyClass QI: Return pointer to IUnknown.\n";
*ppv = static_cast<IDraw*>(this) ;
}
else if (iid == IID_IDraw)
{
    std::cout << "MyClass QI: Return pointer to IDraw.\n";
    *ppv = static_cast<IDraw*>(this) ;
}
else
{
    std::cout <<"MyClass QI: Interface not supported.\n";
    *ppv = NULL ;
    return E_NOINTERFACE;
}
reinterpret_cast<IUnknown*>(*ppv)->AddRef() ;
return S_OK ;
}

ULONG __stdcall MyClass::AddRef()
{
    // Use InterlockedIncrement to ensure thread-safeness
    return InterlockedIncrement(&m_cRef) ;
}

ULONG __stdcall MyClass::Release()
{
    // Use InterlockedDecrement to ensure thread-safeness
    if (InterlockedDecrement(&m_cRef) == 0)
    {
        delete this ;
        return 0 ;
    }
    return m_cRef ;
}

//
// Creation function
//
IUnknown* CreateInstance()
{ // Factory method pattern in the form of a function
    IUnknown* pI = static_cast<IDraw*>(new MyClass) ;
    pI->AddRef() ;
    return pI ;
}
```

用于展示如何使用该组件的测试程序如下：

```
int main()
{
    HRESULT hr ;
    IUnknown* pIUnknown = CreateInstance() ;

std::cout << "Client: Get interface IDraw.";

IDraw* pIDraw = NULL ;
hr = pIUnknown->QueryInterface(IID_IDraw, (void**)&pIDraw) ;

if (SUCCEEDED(hr))
{
    std::cout <<"Client: Succeeded getting IDraw.";
    pIDraw->display() ;        // Use interface IDraw.
    pIDraw->Release() ;
}

std::cout << "Client: Get interface ISave which MyClass
does _not_ support.\n";

ISave* pISave = NULL ;
hr = pIUnknown->QueryInterface(IID_ISave, (void**)&pISave) ;
if (SUCCEEDED(hr))
{
    std::cout << "Client: Succeeded getting ISave.";
    pISave->save() ;        // Use interface ISave.
    pISave->Release() ;
}

std::cout << "Client: Release IUnknown interface.";
pIUnknown->Release() ;

return 0;
}
```

该代码的输出为：

```
Client: Get interface IDraw.MyClass QI: Return pointer to IDraw.
Client: Succeeded getting IDraw.display
Client: Get interface ISave which MyClass does _not_ support.
MyClass QI: Interface not supported.
Client: Release IUnknown interface.Bye, bye
```

## 14.11 虚函数表

我们现在讨论 COM 中接口的工作原理，并讨论 COM 中所做相关设计选择的一些后果。特别是，COM 接口是使用纯抽象基类实现的，即仅由纯虚成员函数组成且没有成员数据的类。需要注意的重要一点是，此类类定义了 COM 对接口所需的具体内存结构。事实上，我们正在定义一块内存的布局。

让我们以一个建模金融衍生品定价函数及其敏感性（如 delta 和 gamma）的接口为例：

```
interface IOption
{ // Functions related to option pricing

    virtual void __stdcall price(double* myPrice) = 0;
    virtual void __stdcall delta(double* myDelta) = 0;
    virtual void __stdcall gamma(double* myGamma) = 0;
};
```

与 C++ 通常的做法一样，我们创建一个实现这些纯虚成员函数的类（为方便起见，我们尚未实现完整的 Black–Scholes 公式）：

```
class Option : public IOption
{ // All values are simulated, used for motivational purposes

public:
    virtual void __stdcall price(double* myPrice) { *myPrice = 1.0;}
    virtual void __stdcall delta(double* myDelta) { *myDelta = 0.5;}
    virtual void __stdcall gamma(double* myGamma) { *myGamma = 0.0;}
};
```

一个简单的用法如下：

```
// Option class
IOption* opt = new Option;
double value;
opt->price(&value);
std::cout << value << std::endl;
delete opt;
```

所有实现（例如类 Option）都是具有如图 14.9 所示相同基本布局的内存块。抽象类定义了内存结构，

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_482_0.png)

图 14.9 内存布局

它不执行内存分配，这是抽象类的派生类完成的。虚函数表是一个指向纯虚函数实现的指针数组。虚表（vtabl）中的第一个条目包含 price 函数的地址，如派生类中实现的那样。表中的第二个条目是 delta 函数的地址，以此类推。一般来说，COM 接口的布局与 C++ 编译器为抽象基类生成的内存布局相同。因此，抽象类可用于定义 COM 接口。

我们现在讨论在实现多个接口的类 CA 的情况下内存布局的工作方式，该类在第 14.9 节中介绍。我们注意到这些接口都派生自 IUnknown。布局如图 14.10 所示。

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_483_0.png)

# 图 14.10 具有多重继承的类的内存布局

最后一点说明；一旦客户端从组件获取接口指针，那么客户端和组件之间唯一的联系就是接口的二进制布局。在这种意义上，客户端实际上是在请求组件接口时请求了一块内存。

## 14.12 COM 与面向对象范式的差异

我们以对 COM 方法与 C++ 面向对象模型之间差异的一般讨论来结束本章。首先，COM 仅依赖于接口继承，这意味着类只能从接口派生。这与 C++ 实现继承形成对比，在实现继承中，派生类可以从一个或多个基类继承功能和数据。后一种方法可以而且确实会导致维护问题，有时称为脆弱基类问题（我们指的是基类中的

# 第 15 章

# 单变量统计分布

## 15.1 引言、目标和目的

在本章中，我们介绍了 *单变量统计分布*、其属性以及一些初步应用。我们重点关注 C++ `<random>` 库和 *Boost Statistics* 库。我们认为这种方法的优势在于我们使用标准化和事实上的标准库。主要主题是：

- C++ 和 Boost 如何支持单变量分布。
- 使用 C++11 误差函数进行 Black–Scholes–Merton 期权定价。计算期权敏感性。
- 使用随机数生成器为数值过程生成输入数据。
- 创建通用类以在 `<random>` 和 Boost 中的各种分布类型之间封装功能。

代码的很大灵活性可归因于 C++ 支持的特性，例如变长参数、元组和模板-模板参数。我们还在回调函数的上下文中引入了 *命令* 设计模式（GOF, 1995）和事件触发机制。

## 15.2 误差函数及其普适性

*误差函数*（也称为 *高斯误差函数*）定义为：

```
erf(x) = 1/√π ∫_{-x}^{x} e^{-t²} dt = 2/√π ∫_{0}^{x} e^{-t²} dt.    (15.1)
```

在统计学中，该函数具有以下解释：设 X 为均值为 0、方差为 1/2 的正态分布随机变量。则 erf(x) 描述了 X 落在区间 [−x, x] 内的概率，其中 x ≥ 0。*余误差函数* 定义为：

```
erfc(x) = 1 − erf(x) = 2/√π ∫_{x}^{∞} e^{-t²} dt.    (15.2)
```

C++11 同时支持误差函数和余误差函数。两个函数都接受 float、double、long double 和整数参数：

```
// Error functions
int i = 1;
float f = 3.0F;
double d = 3.14;
long double d2 = 2.71;
std::cout << "i, erf(x): " << i << ", " << std::erf(i) << '\n';
std::cout << "f, erf(x): " << f << ", " << std::erf(f) << '\n';
std::cout << "d, erfc(x): " << d << ", " << std::erfc(d) << '\n';
std::cout << "d2, erfc(x): " << d2 << ", " << std::erfc(d2) << '\n';
```

在图 15.1 中，我们给出了误差函数在参数特殊情况下的值。

|  | Erf | Erf c |
| +1 | +1 | + 0 |
| i 1 | -1 | 2 |
| Na N | NaN | NaN |

# 图 15.1 误差函数的错误处理和极值

误差函数与累积分布 Φ（标准正态分布的积分）通过以下公式相关：

Φ(x) ≡ N(x) = 1/2 + 1/2 erf(x/√2). (15.3)

我们可以验证以下关系：

erf(x) = 2Φ(x√2) − 1

erfc(x) = 2Φ(−x√2) = 2(1 − Φ(x√2)). (15.4)

误差函数在统计学、概率论和偏微分方程中有许多应用。

### 15.2.1 误差函数的近似

由于 C++11 正式支持误差函数，我们建议使用它而不是其他近似，除非有充分的理由不这样做。可以基于多项式或有理函数使用其他近似（Abramowitz and Stegun, 1965）。例如，Abramowitz and Stegun, 1965 中称为“26.2.16”的五阶多项式近似，适用于自变量的非负值，给出为：

```
const double SQRT2PI = std::sqrt(2.0*3.14159);
const double p = 0.33267;
const double a1 = 0.4361836;
```

