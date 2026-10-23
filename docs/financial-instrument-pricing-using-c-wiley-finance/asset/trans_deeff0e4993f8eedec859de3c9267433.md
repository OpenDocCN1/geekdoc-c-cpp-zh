
// 初始条件
value_type L = 0.0;
value_type T = 20.0;
value_type dt = 0.001;

// 初始条件
state_type x(1);
value_type A = 0.0;
x[0] = A;

std::size_t steps = Bode::integrate(Stiff101, x, L, T, dt);
std::cout << "Number of steps Cash Karp 54: "
          << std::setprecision(16) << steps
          << ", exact: " << exact(T) << ", approximate: "
          << x[0] << '\n';

x[0] = A;
Bode::bulirsch_stoer<state_type, value_type> bsStepper;
steps = Bode::integrate_const(bsStepper, Stiff101, x, L, T, dt);
std::cout << "Number of steps Bulirsch-Stoer: " << steps
          << ", exact: " << exact(T) << ", approximate: " << x[0];

return 0;
}

我们发现 Cash–Karp 在 1,200 次函数求值下给出 4 位精度，而 Bulirsch–Stoer 在 20,000 次函数求值下给出 10 位精度。

## 25.3.2 常微分方程组

我们考察系统 (24.48)（非刚性）和 (24.49)（刚性）作为在 Boost odeint 中实现常微分方程组的良好代表或范例。我们主要关注刚性情形以及合适的方法的讨论。我们定义系统 (24.24) 的雅可比矩阵 J，其元素定义如下：

$$J_{ij} = \frac{\partial f_i}{\partial y_j},\ 1 \le i,j \le n.$$ (25.1)

该公式用作常微分方程求解器的输入，此时索引从 0 开始（C 语言标准）。对于系统 (24.48)，雅可比矩阵为：

$$J = \begin{pmatrix} -2 & 1 \\ 1 & -2 \end{pmatrix}$$ (25.2)

而对于系统 (24.49) 它为：

$$J = \begin{pmatrix} -2 & 1 \\ 998 & -999 \end{pmatrix}.$$ (25.3)

计算每种情况下的特征值将显示系统 (24.49) 为何是刚性的。

我们现在将注意力转向在 C++ 中实现系统 (24.49)（代码中注释了 (24.48)）的问题。扩充的常微分方程类为：

```
using value_type = double;
using vector_type = boost::numeric::ublas::vector<value_type>;
using matrix_type = boost::numeric::ublas::matrix<value_type>;

struct StiffSystem
{
    void operator()(const vector_type& x , vector_type& dxdt ,
                    value_type t)
    { // Lambert page 213

        // Non-stiff form
        /* dxdt[0] = -2.0 * x[0] + 1.0 * x[1] + (2.0*std::sin(t));
           dxdt[1] = 1.0 * x[0] - 2.0 * x[1]
             + (2.0*(std::cos(t) - std::sin(t)));*/

        // Stiff form
        dxdt[0] = -2.0 * x[0] + 1.0 * x[1] + (2.0*std::sin(t));
        dxdt[1] = 998.0 * x[0] - 999.0 * x[1]
            + (999.0*(std::cos(t) - std::sin(t)));
    }
};
```

```
struct StiffSystemJacobi
{
    void operator()(const vector_type& /* x */ , matrix_type& J ,
                    const value_type& t, vector_type& dfdt )
    {
        // Non-stiff form
        /* J(0,0) = -2.0;
        J(0,1) = 1.0;
        J(1,0) = 1.0;
        J(1,1) = -2.0;*/

        // Stiff form
        J(0,0) = -2.0;
        J(0,1) = 1.0;
        J(1,0) = 998.0;
        J(1,1) = -999.0;

        // Derivative wrt t of RHS
        // Non-stiff
        /*dfdt[0] = 2.0 * std::cos(t);
        dfdt[1] = 2.0 * (-std::sin(t) - std::cos(t));*/

        // Stiff
        dfdt[0] = 2.0 * std::cos(t);
        dfdt[1] = 999.0 * (-std::sin(t) - std::cos(t));

}
};
```

你应该检查代码以确保雅可比矩阵计算正确！
为了便于可视化和调试，我们还创建了一个观察者类来存储计算值数组，我们可以在 Excel 中显示：

```
class WriteOutput
{
private:

public:
    std::vector<value_type> tValues;
    std::vector<value_type> y1Values;
    std::vector<value_type> y2Values;
public:
    WriteOutput() : tValues(std::vector<value_type>()),
                    y1Values(std::vector<value_type>()),
                    y2Values(std::vector<value_type>()) {}

    void operator ()(const vector_type &x, const value_type t)
    {
        tValues.push_back(t);
        y1Values.push_back(x[0]);
        y2Values.push_back(x[1]);
    }

    const std::vector<value_type>& xAxis() const
    {
        return tValues;
    }

    const std::vector<value_type>& y1Axis() const
    {
        return y1Values;
    }

    const std::vector<value_type>& y2Axis() const
    {
        return y2Values;
    }
};
```

测试程序为：

```
// Example based on Lambert "Numerical Methods for Ordinary
// Differential Equations" Wiley 1991. page 213
```

```
// Initial condition
vector_type x(2);
x[0] = 2.0; x[1] = 3.0;

// Error tolerances
value_type absErr = 1.0e-6;
value_type relErr = 1.0e-6;

// Integration range
value_type L = 0.0;
value_type T = 10.0;
value_type dt = 0.001;

WriteOutput wo;
std::size_t steps = Bode::integrate_const
(Bode::make_dense_output<Bode::rosenbrock4<value_type>>
(absErr,relErr), std::make_pair(StiffSystem(),
StiffSystemJacobi()), x , L, T, dt, std::ref(wo));

// std::size_t steps = Bode::integrate(StiffSystem(), x, L, T, dt,
// std::ref(wo));

std::cout << steps << std::endl;
```

我们注意到使用生成器函数 make_dense_output 来从更简单的步进器创建稠密输出步进器。在这里我们看到如何将绝对误差和相对误差引入步进器。

为完整起见，我们包含精确解 (24.50) 以便给出误差估计：

```
// Post processing: computing error and displaying the values in Excel
value_type f1 = 2.0 * std::exp(-T); value_type f2 = f1;
double exact1 = f1 + std::sin(T);
double exact2 = f2 + std::cos(T);
std::cout << "Exact: [" << std::setprecision(16)
<< exact1 << ", " << exact2 << "]\n";
std::cout << "Approximate: [" << x[0] << ", " << x[1] << "]\n";
std::cout << "Errors: " << exact1 - x[0] << ", "
<< exact2 - x[1] << '\n';
```

最后，我们可以在 Excel 中显示值：

```
// Display in Excel Driver
ExcelDriver xl; xl.MakeVisible(true);
xl.CreateChart(wo.xAxis(), wo.y1Axis(), std::string("y1 values"));
xl.CreateChart(wo.xAxis(), wo.y2Axis(), std::string("y2 values"));
```

本节的设计和代码可作为模板（cookie cutter），当你设计类似系统时可以使用。

## 25.4 矩阵微分方程

Boost *odeint* 库可用于求解矩阵常微分方程，例如：

$$\frac{dY}{dt} = AY + YB \tag{25.4}$$

其中 $A$、$B$ 和 $Y$ 都是 $n \times n$ 矩阵。

可以证明系统 (25.4) 的解可以写成（参见 Brauer 和 Nohel，1969）：

$$Y(t) = e^{At} C e^{Bt}, \text{where } Y(0) = C \text{ and } C \text{ is a given matrix.} \tag{25.5}$$

一个特例是当：

$$\begin{aligned}
B &= 0 \text{（零矩阵）} \\
C &= 1 \text{（单位矩阵）}
\end{aligned} \tag{25.6}$$

此时我们有解即矩阵的 *指数*：

$$Y(t) = e^{At}. \tag{25.7}$$

结论是我们现在可以通过求解矩阵常微分方程来计算矩阵的指数。我们使用 C++ 讨论这一主题。为此，我们考察系统：

$$\begin{cases}
\dfrac{dY}{dt} = AY \\
Y(0) = C
\end{cases} \tag{25.8}$$

其中 $C$ 是给定的向量。

我们用以下 C++ 类对该系统进行建模：

```
namespace ublas = boost::numeric::ublas;

using value_type = double;
using state_type = boost::numeric::ublas::matrix<value_type>;

class MatrixOde
{
private:
    // dB/dt = A*B, B(0) = C;
    ublas::matrix<value_type> A_;
    ublas::matrix<value_type> C_;
public:
    MatrixOde(const ublas::matrix<value_type>& A,
              const ublas::matrix<value_type>& IC)
        : A_(A), C_(IC) {}
```

```
void operator()(const state_type &x , state_type &dxdt,
    double t ) const
{
    for( std::size_t i=0 ; i < x.size1();++i )
    {
        for( std::size_t j=0 ; j < x.size2(); ++j )
        {
            dxdt(i, j) = 0.0;
            for (std::size_t k = 0; k < x.size2(); ++k)
            {
                dxdt(i, j) += A_(i,k)*x(k,j);
            }
        }
    }
};
```

一个初始示例为：

```
namespace Bode = boost::numeric::odeint;

std::size_t N = 2;
ublas::identity_matrix<value_type> C(N);
ublas::matrix<value_type> A(N,N);
A(0, 0) = 6.0;  A(0, 1) = -1.0; A(1,0) = 9.0; A(1, 1) = 0.0;

ublas::matrix<value_type> B(N,N);

// Initialise the solution matrix B
B = C;

MatrixOde ode(A, C);
double L = 0.0;
double T = 3.0;
double dt = 0.001;

std::size_t steps = Bode::integrate(ode, B, L, T, dt, write_out);

std::cout << "Value at time: " << T << '\n';
std::cout << B << '\n';

// Computing the exact matrix
ublas::matrix<value_type> check(N, N);
double e = std::exp(3.0*T);
check(0, 0) = (1.0 + 3.0*T)*e;
check(0, 1) = -T*e;
check(1, 0) = 9.0*T*e;
check(1, 1) = (1.0 - 3.0*T)*e;
std::cout << check << '\n';
```

