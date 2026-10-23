

## 第25章

## 高级常微分方程与行进波方法

## 25.1 引言与目标

我们从第24章继续讨论一阶常微分方程组的数值求解问题。在第24章中我们自行开发代码来近似求解常微分方程，而现在我们使用 Boost odeint 库来为我们完成工作。然后我们引入行进波方法（Method of Lines, MOL），它允许我们将第20章到第23章中讨论的时间相关抛物型偏微分方程的解近似为常微分方程组。在这种意义上，MOL 是对手工制作的时间离散化方法（如 BTCS 和 Crank–Nicolson 等）的竞争者。MOL 具有以下若干优点：

- **A1:** 它可以应用于具有多种边界条件的线性时变偏微分方程。
- **A2:** 它可以应用于非线性偏微分方程，如 UVM（Pealat and Duffy, 2011）、CVA（Green, 2016）以及使用惩罚和屏障方法进行美式期权定价。
- **A3:** 我们可以从多种时间推进格式中选择，选择最适合手头问题的格式。例如，我们可能希望产生高度精确的结果，或选择适合刚性方程的格式。
- **A4:** MOL 易于应用于 2 因子和 3 因子偏微分方程，例如二维热方程、篮子期权、Heston 模型以及第23章的锚定问题。
- **A5:** 运行性能。MOL 是一种通用方法，适用于线性和非线性偏微分方程，通常比手工制作的代码慢。然而，这并不总是如此，尤其对于非线性偏微分方程。
- **A6:** MOL 通常比手工制作的有限差分格式更稳健。

在本章的所有情况下，我们都将使用 Boost odeint 作为常微分方程求解器来近似求解时变对流-扩散-反应偏微分方程的解。我们举例说明，并给出若干关于应用 MOL 并将其与第20章到第23章中讨论的有限差分方法进行比较的重要且具有挑战性的练习。

## 25.2 Boost *ODEINT* 库简介

有若干库支持 MOL。例如在 *Mathematica* 中，NDSolve 包使用数值方法近似求解常微分方程组，并且在 NAG 库中也有支持。这些来源可作为背景参考。此外，关于 MOL 及其相关主题的数学和数值基础的良好讨论，可见 Lambert (1991)、Henrici (1962) 和 Crank (1984)。

在本章中我们重点关注 Boost *odeint*。根据在线文档，该库描述如下：

> *odeint 的主要关注点是提供以算法完全独立于用于表示状态的数据结构的方式实现的数值方法。通过这样做，odeint 可应用于广泛的应用，并且可与许多其他库一起使用。除了状态定义为 `std::vector` 或 `boost::array` 的常见情况外，odeint 还为以下库提供支持：*

- *Boost.uBLAS.*
- *Thrust，允许 odeint 在 CUDA 设备上运行。*
- *gsl_vector 以便与 GSL 中的众多数值函数兼容。*
- *Boost.Range.*
- *Boost.Fusion（状态类型可以是 fusion 向量）。* 
- *Boost.Units.*
- *Intel Math Kernel Library 以获得最大性能。*
- *VexCL 用于 OpenCL。*
- *Boost.Graph.*

我们不讨论这些特性，因为我们更感兴趣的是 odeint 支持的 *步进算法* 和 *积分函数*。

### 25.2.1 步进器

*odeint* 中的 *stepper* 执行单步，例如从时间层 *t* 到时间层 *t + dt*，其中 *dt* 是步长。换句话说，它执行常微分方程解 *x(t)* 的单步以得到 *x(t + dt)*，使用给定的步长 *dt*。为此，每个步进器都有 `do_step` 方法的两个重载版本，即 *原地变换* 的当前状态和 *非原地变换*：

- `do_step(sys, inout, t, dt)`
- `do_step(sys, in, t, out, dt)`

分别为，其中：

- `sys`：常微分方程右端 *dy/dt = rhs*。
- `inout`：时间 *t* 处的解，随后变为时间 *t + dt* 的解（前值被覆盖）。
- `in` 和 `out`：分别在时间层 *t* 和 *t + dt* 处的值。

通常，你不需要了解这一层细节，因为它由我们在第 25.2.3 节中讨论的各种 *积分函数* 处理。主要步进器特化如下。

- *显式步进器*：常微分方程的新状态可以直接从当前状态计算得出，而无需求解隐式（通常是非线性）方程。
- *辛步进器*：这些步进器用于 *哈密顿系统*，超出本书范围。
- *隐式步进器*：这些是适用于 *刚性系统* 的步进器，后者通常具有两个或多个数量级截然不同的时间尺度。我们在第24章看到经典 Runge–Kutta 方法不适用于刚性系统。通常，我们使用非线性求解器（如 Newton–Raphson 方法），因此我们需要计算系统雅可比矩阵。
- *受控步进器*：这些步进器具有使用 *自适应步长控制* 的能力。我们可以根据当前误差是否小于或大于给定容差来减小或增大步长。一个例子是 bulirsch_stoer。
- *稠密输出步进器*：这些步进器可能采取较大步长并在两个连续点之间插值解。一个例子是 euler。
- *误差步进器*：计算常微分方程解 x(t) 的一步，步长为 dt，以产生 x(t + dt)，同时计算结果的误差估计。

一些具体步进器为：

- runge_kutta4
- euler
- runge_kutta_cash_karp54
- runge_kutta_dopri5
- runge_kutta_fehlberg78
- modified_midpoint
- rosenbrock4

典型的 C++ 代码为（便于参考）：

```
// Steppers: a stepper maps the solution x(t) -> x(t+dt) ->
// x(t + 2dt) -> ...
Bode::modified_midpoint<state_type, value_type> mmpStepper;          // O(2)
Bode::bulirsch_stoer<state_type, value_type> bsStepper;             // Variable
Bode::runge_kutta_fehlberg78<state_type, value_type> rkfStepper;     // O(8)
Bode::runge_kutta_dopri5<state_type, value_type> rkdopiStepper;     // O(5)
Bode::euler<state_type, value_type> eulerStepper;                   // O(1)
Bode::runge_kutta_cash_karp54<state_type, value_type> rkccStepper;  // O(5)
Bode::runge_kutta4<state_type, value_type> rk4Stepper;              // O(4)
Bode::rosenbrock4<value_type> rosenbrock4Stepper;                   // O(4)
```

参数 state_type 和 value_type 是用户可定义的类型，如我们将看到的那样。例如，前者类型可以是 std::vector<double>，而后者类型可以是 double。

我们现在讨论如何使用步进器与 *积分函数*。有关数学和数值背景，请参阅 Press et al. (2002)、Henrici (1962) 以及尤其是 Lambert (1991)。

### 25.2.2 步进器示例

步进器可以看作是 odeint 的构建块，因为它们实现了常微分方程的一步求解器。它们类似于我们在第24章中创建的步进器。了解它们的工作方式很有用，包括在子区间 [t, t + dt] 中估计误差的能力。我们通过定义一个具体的常微分方程（负指数函数）来举例：

```
using value_type = double;
using state_type = std::vector<value_type>;

// Simple ODE system (scalar (vector of length 1))
struct Ode01
{ // du/dt = -u, u(0) = 1; u(t) = exp(-t)

    void operator() (const state_type &x, state_type &dxdt,
                     const value_type t)
    {
        dxdt[0] = -x[0];
    }
};
```

然后我们可以使用步进器计算近似解。以下是一个使用三个步进器（四阶 Runge–Kutta、修正中点和 Cash–Karp）的示例：

```
int main()
{
    namespace Bode = boost::numeric::odeint;

    state_type x(1); // state, vector of 1 element (scalar problem)
    x[0] = 1.0;

    state_type y(1);
    state_type z(1);
    state_type err(1);

    // Integration parameters
    value_type t = 0.0;
    value_type dt = 0.1;
    size_t nSteps = 7;

    // Create stepper
    Bode::runge_kutta4<state_type> rk4;
    Bode::modified_midpoint<state_type> mmp;
    Bode::runge_kutta_cash_karp54<state_type> rkck54;
```

