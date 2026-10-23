

```cpp
class WriteOutput
{
public:

public:
    WriteOutput() { }

    void operator ()( const state_type &x , const value_type t )
    {
        std::cout << "Time and value (FO): " << t << " "
                  << x[0] << std::endl;
    }
};
```

一个测试程序是：

```cpp
int main()
{
    namespace Bode = boost::numeric::odeint;

    // Initial condition
    state_type x(1);
    value_type A = value_type(0.0);
    x[0] = A;


    // [L,U]
    value_type L = value_type(0.000000);
    value_type U = value_type(6.0);
    value_type dt = value_type(1.0e-15);

    WriteOutput wo;
    OdeExp ode;

    // std::size_t steps
    //     = Bode::integrate(ode, x, L, U, dt, std::ref(wo));

    // Bode::runge_kutta_dopri5<state_type, value_type> myStepper;
    Bode::bulirsch_stoer<state_type, value_type> myStepper;

    std::size_t steps = Bode::integrate_adaptive (myStepper,ode,x,L,U,dt,
    std::ref(wo));

    std::cout.precision(100);
    std::cout << "Approximate answer, steps: " << x[0] << ", "
              << steps << std::endl;

    return 0;
}
```

```cpp
std::cout << "\n\n";
std::cout << std::setprecision(precision);
for (int n = 0; n<number; ++n)
{
    std::cout << std::generate_canonical<T, bits>(gen) << ", ";
}
std::cout << "\n\n";
}
```

一个测试程序是：

```cpp
// Generate canonical
int number = 4;
CanonicalGenerator<double>(number, 16);

using boost::multiprecision::cpp_dec_float_50;
CanonicalGenerator<double>(number, 50);
```

典型输出是：

```text
0.6443861122559016, 0.9267760353530851, 0.8461941290458814, 0.9296946958489013,

0.80979306562688702086916237021796405315399169921875,
0.86959590730995528495839153038104996085166931152344,
0.6135122815448957878103897201071958989049530029297,
0.244033083049029708710975522831405512988567352294922,
```

算法 *independent_bits_engine* 的输入参数为被包装引擎的类型、生成的数字应具有的位数以及生成的随机数字的类型（应为无符号整数）。一个示例是：

```cpp
std::random_device rd;
const std::size_t W = 32;
std::independent_bits_engine<std::mt19937, W, std::uint_fast64_t>
    generator(rd());

std::cout << "\n\n";
std::cout << std::setprecision(precision);
for (int n = 0; n<number; ++n)
{
    std::cout << generator() << ", ";
}
std::cout << "\n\n";

// Construct the underlying engine with a seed sequence
std::seed_seq seedSeq = { -1,0, 1 };
std::independent_bits_engine<std::mt19937, W, std::uint_fast64_t>
    generator2(rd());
std::cout << "\n\n";

for (int n = 0; n<number; ++n)
{
    std::cout << generator2() << ", ";
}
std::cout << "\n";
```

我们运行此代码时得到的输出如下：

```text
3224128699, 1790518196, 367697637, 3964670867,

1545172431, 2759616371, 502877303, 3738674815,
```

为完整起见，我们给出一些 std::seed_seq 产生的值分布在整个 32 位范围内的示例。这提供了一种方法来为大量随机数引擎播种，或为需要大量熵的生成器播种，而初始种子或初始种子序列分布不良或种子很小：

```cpp
void SeedSequence()
{
    // Initial seed sequence of length 0
    std::seed_seq s1;

    // Iterate over a range
    int a[4] = { 1,2,3,4 };
    std::seed_seq s2(a, a + 4);

    // Initialiser list
    std::seed_seq s3 = { -1,0, 1 };
}
```

## A1.7 总结与结论

在本附录中，我们概述了 *Boost Multiprecision* 库。它支持高精度整数和浮点数据类型。可以对这些类型执行通常的算术运算，并且 std 命名空间中常见的数学函数（<cmath> 库） 在 boost::multiprecision 命名空间中有其等价物。我们还讨论了如何将多精度数据类型与我们在前几章中讨论的 C++ 语言特性和库集成。

在大多数应用中，除非您遇到下溢或上溢问题，否则可能不需要使用多精度数据类型。增加的鲁棒性代价是通常性能的降低。

## A1.8 练习与项目

### 1. （刚性 ODE 和多精度）

我们在第 24 章中看到，显式有限格式（例如欧拉和龙格-库塔方法）对于具有 *多个时间尺度* 的 ODE 表现很差。本练习的目的是确定使用多精度数据类型的效果是否可以弥补这一问题。回答以下问题：

- a) 使用多精度数据类型将显式欧拉方法应用于 ODE (24.46)。这与使用 double 相比是否有所改进？
- b) 现在使用多精度数据类型将 Cash–Karp 应用于 ODE (24.46) 并研究潜在的改进。
- c) 根据 a) 和 b) 部分的发现，考虑将 Boost odeint 应用于系统 (24.51)。

完成本练习后，您应该能够对使用多精度数据类型计算刚性 ODE 的数值解的有用性（或没有）发表意见。

### 2. （Boost odeint 用于复状态类型）

系数为复数的微分方程出现在许多应用中，例如傅里叶变换和 PDE 到 ODE 的转换。

求解具有复值系数的 ODE 有两种主要方法。第一种方法是在以下简单示例所示的情况下使用 Boost odeint 处理复数：

```cpp
// C++ types
using value_type = double;
using state_type = std::complex<value_type>;

namespace Bode = boost::numeric::odeint;

// Global parameters of ODE
std::complex<double> a(2,3);   // 2 + 3i
std::complex<double> A(10,0);  // 10

class OdeExp
{
public:

public:
    OdeExp() { }

    void operator() (const state_type &x, state_type &dxdt,
        const value_type t)
    {
        // C++ standard
        dxdt = -a * x;
    }
};

int main()
{
    namespace Bode = boost::numeric::odeint;

    // Initial condition
    state_type x;
    x = A;

    // [L,U]
    value_type L = value_type(0.000000);
    value_type U = value_type(1.0);
    value_type dt = value_type(1.0e-15);

    OdeExp ode;
    std::size_t steps = Bode::integrate(ode, x, L, U, dt);

    std::cout.precision(16);
    std::cout << "Approximate answer, steps: " << x << ", "
              << steps << std::endl;
    std::cout << "Exact answer: " << A*std::exp(-a*U)
              << ", " << std::endl;

    return 0;
}
```

第二种方法是把复 ODE 重新表述为一对实 ODE。为此我们考虑 ODE：

$$\frac{du}{dt}+\lambda u=0, \qquad u(0)=A, \qquad (\lambda,\ A\in\mathbb{C})$$

$$u:[0,T]\to\mathbb{C}$$
$$u(t)=v(t)+iw(t)$$

$$\lambda=\alpha+i\beta$$
$$A=a+ib, \qquad (i=\sqrt{-1}).$$

然后该 ODE 可以解耦为一对 ODE（只需分组实部和虚部）：

$$\frac{dv}{dt}+\alpha v-\beta w=0$$

$$\frac{dw}{dt}+\alpha w+\beta v=0$$

$$v(0)=a,\ w(0)=b$$
$$u(t)=v(t)+iw(t).$$

回答以下问题：

- a) 使用 Boost odeint 实现方程组并将解与本练习中给出的第一个解进行比较。
- b) 将本练习中的两种解推广到第 20、21 和 25 章中讨论的一因子对流-扩散-反应 PDE。在这种情况下，解和 PDE 系数都可以是复值。
- **c)** 在 A1.5 节中，我们将 Fresnel 积分计算为两个实 ODE 的数值解。可以将此类积分写成具有复值被积函数的单个积分：

  $$\psi(x)=\int_0^x e^{\frac{i\pi}{2}t^2}\,dt.$$

  该公式出现在衍射应用中。我们现在可以对该积分求导以产生复 ODE：

  $$\frac{d\psi}{dx}=e^{\frac{i\pi}{2}x^2},\quad x>0$$

  $$\psi(0)=0.$$

  使用上述介绍性代码中的相同代码实现此 ODE。

### 3. （二次方程）

考虑计算二次方程的根：

$$94906265.625x^2-189812534x+94906268.375=0.$$

其根为：

$x_1=1.00000002897958$

$x_2=1.00000000000000$

而使用 IEEE 754 双精度算术对应于 15 和 17 位有效数字的精度时，计算出的根为：

$x_1=1.000000014487979$

$x_2=1.000000014487979$

使用 Boost multiprecision 数据类型计算该二次方程的根。

### 4. （热方程与分离变量）

考虑具有狄利克雷边界条件的有界域上的热方程：

$$\frac{\partial u}{\partial t}=\frac{\partial^2u}{\partial x^2},\quad 0<x<1,\ t>0$$

$$u(0,t)=u(1,t)=0$$

$$u(x,0)=2x,\quad 0\le x\le \frac{1}{2}$$

$$u(x,0)=2(1-x),\quad \frac{1}{2}\le x\le 1.$$

