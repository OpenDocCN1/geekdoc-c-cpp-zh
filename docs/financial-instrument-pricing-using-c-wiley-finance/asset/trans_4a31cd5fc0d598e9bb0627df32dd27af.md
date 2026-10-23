

double K;
double T;
double r;
double sig;

// Extra data
double D;      // dividend

int type;      // 1 == call, -1 == put

explicit constexpr OptionData(double strike, double expiration,
                              double interestRate,
                              double volatility, double dividend,
                              int PC)
    : K(strike), T(expiration), r(interestRate),
      sig(volatility), D(dividend), type(PC)
{}

template <typename ArgPack> OptionData(const ArgPack& args)
{
    K = args[OptionParams::strike];
    T = args[OptionParams::expiration];
    r = args[OptionParams::interestRate];
    sig = args[OptionParams::volatility];
    D = args[OptionParams::dividend];
    type = args[OptionParams::optionType];

    std::cout << "K " << K << ", T " << T << ", r " << r << std::endl;
    std::cout << "vol " << sig << ", div " << D << ",type "
              << type << std::endl;
}

};

我们可以通过调用其构造函数（参数的位置很重要）来初始化结构体 OptionData 的元素，也可以通过统一初始化或使用 Boost 参数库支持的命名变量来实现。在最后一种情况下，输入参数的相对顺序无关紧要，下面的示例就说明了这一点：

//OptionData opt2 { 100.0, 1.0, 0.06, 0.2, 0.03, 1 };

// Init via named Boost variables
OptionData myOption((OptionParams::strike = 65.0,
                    OptionParams::expiration = 1.0,
                    OptionParams::volatility = 0.001,
                    OptionParams::dividend = 0.0,
                    OptionParams::optionType = -1,
                    OptionParams::interestRate = 0.1));
```

## 14.6.2 测试设计和 Excel 中的展示

我们现在讨论图 14.6 中类的配置和初始化。步骤很容易遵循：

// A. Create basic input data
//OptionData(double strike, double expiration, double interestRate,
// double volatility, double dividend, int PC)
OptionData myOption { 100.0, 10.0, 0.1, 0.9, 0.03, 1 };
double S0 = 20.0;

// B. Get the SDE
// Using factories
std::shared_ptr<Sde<double>> sde = SdeFactory::ChooseSde<double>
(myOption, S0);

// C. Set up the FDM classes; 1 to N relationship between SDE and FDM
std::default_random_engine eng;

std::normal_distribution<double> nor(0.0, 1.0);
std::random_device rd;
eng.seed(rd());

FdmEuler<double> fdm(sde, nor, eng);
FdmHeun<double> fdm2(sde, nor, eng);

// D. Joining up SDE and FDM in Mediator class
long NT = 200;
auto vec = Path(*sde, fdm, NT);
auto vec2 = Path(*sde, fdm2, NT);

double A = 0.0; double B = myOption.T;
auto x = CreateMesh(NT+1, A, B);

// E. 'Report' system; display the graphs in Excel
ExcelDriver xl; xl.MakeVisible(true);

// E_1: Display each curve in its own sheet
xl.CreateChart(x, vec, "Euler method");
xl.CreateChart(x, vec2, "Heun method");

// Names of each vector
std::list<std::string> labels{ "Euler", "Heun"};

// The list of Y values
std::list<std::vector<double> > curves{ vec, vec2};

// E_2: Display all curves in one sheet
xl.CreateChart(x, labels, curves, "Comparing FDM ", "t", "S");
```

## Euler method

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_468_0.png)

# FIGURE 14.7 CIR path with Euler method

图 14.7 显示了显式 Euler 方法的典型输出。在这种情况下，我们模拟 CIR 模型的短期利率（平方根扩散过程），我们可以看到（并且众所周知）Euler 方法会产生负值，这是错误的。我们将在练习 4 中讨论这个问题。

最后，我们展示了实现图 14.6 中中介组件的代码。在这个版本中它是一个自由函数，但在更大更复杂的应用程序中，它可以被建模为一个整体-部分对象（POSA, 1996）以促进可维护性。它将具有以下方法：

// Creating a path of an SDE approximated by FDM
template <typename Derived, typename T>
std::vector<T> Path(const Sde<T>& sde, Fdm<typename Derived,
T>& fdm, long NT)
{

std::vector<T> result(NT + 1);

result[0] = sde.ic;

double dt = sde.B / static_cast<T>(NT);
double tn = dt;

for (std::size_t n = 1; n < result.size(); ++n)
{
    result[n] = fdm.advance(result[n - 1], tn, dt);
    tn += dt;
}

return result;
}
```

## 14.7 SUMMARY AND CONCLUSIONS

本章中我们介绍了一个用于在 Excel 中显示数值数据的软件框架。我们专注于在 Excel 电子表格程序中可视化向量、矩阵和曲线。我们阐述了其优势并给出了若干示例。

## 14.8 EXERCISES AND PROJECTS

+   1. (Extensions to the Excel Driver)

可以通过多种方式为 Excel 驱动程序添加新功能。在本练习中我们专注于代码的泛化。我们希望显示一元和二元函数。我们隐藏诸如创建网格数组和其他支持代码之类的低级细节。所需函数具有以下接口：

```
using Function1DType = std::function<double (double x)>;
using Function2DType = std::function<double(double x, vdouble y)>;

void printDiscreteFunctionValues(const Function1DType& f,
double A, double B,long nSteps,
    const std::string& title,
    const std::string& horizontal,
    const std::string& vertical,
    const std::string& legend);

void printDiscreteFunctionValues(const Function1DType& f,
    const std::vector<double>& mesh,
    const std::string& title,
    const std::string& horizontal,
    const std::string& vertical,
    const std::string& legend);

void printDiscreteFunctionValues(const Function2DType& f,
    double A, double B,long xSteps,
    double C, double D,long ySteps,
    const std::string& title,
    const std::string& horizontal,
    const std::string& vertical,
    const std::string& legend);
```

```
void printDiscreteFunctionValues(const Function2DType& f,
    const std::vector<double>& mesh,
    const std::vector<double>& mesh2,
    const std::string& title,
    const std::string& horizontal,
    const std::string& vertical,
    const std::string& legend);
```

请回答以下问题：

+   a) 基于驱动程序中现有的代码编写上述函数的代码。
+   b) 在 Black–Scholes 看涨期权价格及其对应的希腊字母上测试一元函数：
+   Δ_C = ∂C/∂S = e^{(b−r)T} N(d₁)
+   Γ_C ≡ ∂²C/∂S² = ∂Δ_C/∂S = n(d₁)e^{(b−r)T}/(Sσ√T)
+   Vega_C ≡ ∂C/∂σ = S√T e^{(b−r)T} n(d₁)
+   Θ_C ≡ −∂C/∂T = − Sσ e^{(b−r)T} n(d₁)/(2√T) − (b − r) S e^{(b−r)T} N(d₁) − r K e^{−rT} N(d₂).

c) 通过在给定区间上显示双变量 t 分布的概率密度函数来测试二元函数（Nadarajah and Kotz, 2005）：
f(x, y; ν, ρ) = 1/[2π√(1−ρ²)] { 1 + [x² − 2ρxy + y²]/[ν(1−ρ²)] }^{−(ν+2)/2}.

我们将在第 16 章讨论累积概率积分的计算方法时更详细地讨论该分布：
P(x, y; ν, ρ) = ∫_{-∞}^{x} ∫_{-∞}^{y} f(x, y; ν, ρ) dx dy.

+   2. (Finite Difference Schemes for the One-Dimensional Heat Equation)

Excel 驱动程序的一个有趣且有用的应用是在显示使用 FDM 的情况下对热方程近似解的值，如第 13 章所讨论的那样。特别是，我个人发现它在以下情况下很有用：

+   C1: 编写 FD 代码后，我们希望查看其是否产生正确的结果。为此，以易于格式化的方式显示结果非常有帮助。
+   C2: 我们希望比较 ADE 系列格式与 Crank–Nicolson 方法或 PDE 的解析解等基线情况的精度。
+   C3: 显示近似方法的精度作为某个独立变量的函数。一个例子是绘制二项式方法中期权价格作为步数函数的图像。同样的方法也适用于有限差分方法。

请回答以下问题：

+   a) 使用我们在第 13 章中介绍的两种 ADE 格式来近似热方程的解（参见第 13 章中的方程 (13.14)）。

