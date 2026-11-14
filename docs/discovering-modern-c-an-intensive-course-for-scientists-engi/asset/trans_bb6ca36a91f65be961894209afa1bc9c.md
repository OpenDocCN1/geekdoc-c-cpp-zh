

### 清单 7-4: 容器代数

```cpp
struct container_algebra
{
    template<class S1, class S2, class S3, class Op>
    void for_each(S1 &s1, S2 &s2, S3 &s3, Op op) const
    {
        using std::begin;
        using std::end;

        auto first1 = begin(s1);
        auto last1 = end(s1);
        auto first2 = begin(s2);
        auto first3 = begin(s3);
        for( ; first1 != last1 ; )
            op(*first1++, *first2++, *first3++);
    }
};
```

最终部分是由一组再次收集在结构体中的仿函数对象组成的基本操作。清单 7-5 展示了这些操作函数的实现。为求简洁，我们再次仅展示可用于 for_each3（清单 7-4）的 scale_sum2 仿函数。然而，扩展 scale_sum5 以配合 for_each5 使用相当直接。如清单 7-5 所示，这些仿函数由若干参数 alpha1、alpha2... 以及一个计算所需乘积和的函数调用运算符组成。

### 清单 7-5: 操作

```cpp
struct default_operations {
    template<class F1=double, class F2=F1>
    struct scale_sum2 {
        typedef void result_type;

        const F1 alpha1;
        const F2 alpha2;

        scale_sum2(F1 a1, F2 a2)
        : alpha1(a1), alpha2(a2) { }

        template<class T0, class T1, class T2>
        void operator()(T0 &t0, const T1 &t1, const T2 &t2) const
        {
            t0 = alpha1 * t1 + alpha2 * t2;
        }
    };
};
```

在收集了所有模块化组件后，我们可以基于上述部分实现龙格-库塔 4 算法。清单 7-6 展示了此实现。请注意，上述引入的所有部分均作为模板参数提供，因此是可配置的。

### 清单 7-6: 泛型龙格-库塔 4

```cpp
template<class state_type, class value_type = double,
         class time_type  = value_type,
         class algebra    = container_algebra,
         class operations = default_operations>
class runge_kutta4
{
public:
    template<typename System>
    void do_step(System& system, state_type &x,
                 time_type t, time_type dt)
    {
        adjust_size(x);
        const value_type one = 1;
        const time_type dt2 = dt/2, dt3 = dt/3, dt6 = dt/6;

        typedef typename operations::template scale_sum2<
            value_type, time_type> scale_sum2;

        typedef typename operations::template scale_sum5<
            value_type, time_type, time_type,
            time_type, time_type> scale_sum5;

        system(x, k1, t);
        m_algebra.for_each3(x_tmp, x, k1, scale_sum2(one, dt2));

        system(x_tmp, k2, t + dt2);
        m_algebra.for_each3(x_tmp, x, k2, scale_sum2(one, dt2));

        system(x_tmp, k3, t + dt2);
        m_algebra.for_each3(x_tmp, x, k3, scale_sum2(one, dt));

        system(x_tmp, k4, t + dt);
        m_algebra.for_each5(x, x, k1, k2, k3, k4,
                            scale_sum5(one, dt6, dt3,
                                       dt3, dt6));
    }

private:
    state_type x_tmp, k1, k2, k3, k4;
    algebra m_algebra;

    void adjust_size(const state_type &x) {
        resize(x, x_tmp); resize(x, k1);
        resize(x, k2); resize(x, k3); resize(x, k4);
    }
};
```

以下代码片段展示了如何实例化此龙格-库塔 4 步进器：

```cpp
typedef runge_kutta4< vector<double>, double, double,
        container_algebra,
        default_operations > rk4_type;
// equivalent shorthand definition using the default parameters:
// typedef runge_kutta4< vector<double> > rk4_type;

rk4_type rk4;
```

### 7.1.3.3 简单示例

最后，我们展示了一个小示例，说明如何使用上述泛型龙格-库塔 4 实现来积分著名的 Lorenz 系统的轨迹。因此，我们只需定义状态类型，实现 Lorenz 系统的右端（RHS）方程，然后使用上述的 runge_kutta4 类，搭配标准的 container_algebra 和 default_operations。清单 7-7 展示了一个仅需 30 行 C++ 代码的示例实现。

### 7.1.4 展望

我们已抵达龙格-库塔 4 方案的泛型实现。从此，我们可以向众多方向继续拓展。显然，可以添加更多龙格-库塔方案，可能包括步长控制和/或密集输出功能。尽管此类方法可能更难以实现，并且需要后端（代数和操作）提供更多功能，但它们在概念上符合上述概述的泛型框架。此外，还可以扩展到其他显式算法，如多步方法或预测-校正方案，因为本质上所有显式方案仅依赖于此处展示的 RHS 计算和向量操作。然而，隐式方案需要更高阶的代数例程，如求解线性系统，因此需要不同于此处引入的代数类。

此外，除了 container_algebra，我们还可以提供其他后端。一个示例是使用 omp_algebra 或 mpi_algebra 引入并行性。此外，还可以通过 opencl_algebra 及相应的数据结构来处理 GPU 计算。另一个用例是依赖某些线性代数库，该库提供已实现所需操作的向量或矩阵类型。在这种情况下，不需要迭代，应使用一个虚拟代数，它仅将所需计算转发给 default_operations 而不进行迭代。

如您所见，泛型实现提供了丰富的方式来调整算法以适应非标准情况，例如不同的数据结构或 GPU 计算。这种方法的优势在于，实际算法无需更改。这种通用性允许我们替换实现的某些部分以适应不同情况，但算法的实现本身保持不变。

遵循此处所述方法的通用常微分方程（ODE）算法的广泛实现见于 Boost.odeint 库。2 它包含众多数值算法和多个后端，例如用于并行性和 GPU 计算的后端。它积极维护并

### 清单 7-7: Lorenz 系统中的轨迹

```cpp
typedef std::vector<double> state_type;
typedef runge_kutta4< state_type > rk4_type;

struct lorenz {
    const double sigma, R, b;
    lorenz(const double sigma, const double R, const double b)
    : sigma(sigma), R(R), b(b) { }

    void operator()(const state_type &x, state_type &dxdt,
        double t)
    {
        dxdt[0] = sigma * ( x[1] - x[0] );
        dxdt[1] = R * x[0] - x[1] - x[0] * x[2];
        dxdt[2] = -b * x[2] + x[0] * x[1];
    }
};

int main() {
    const int steps = 5000;
    const double dt = 0.01;

    rk4_type stepper;
    lorenz system(10.0, 28.0, 8.0/3.0);
    state_type x(3, 1.0);
    x[0] = 10.0; // some initial condition
    for( size_t n=0 ; n<steps ; ++n ) {
        stepper.do_step(system, x, n*dt, dt);
        std::cout << n*dt << ' ';
        std::cout << x[0] << ' ' << x[1] << ' ' << x[2]
            << std::endl;
    }
}
```

广泛使用和测试。只要有可能，强烈建议使用此库，而不是重新实现这些算法。否则，此处展示的想法和代码可以作为一个良好的起点，以泛型方式实现新的、更针对特定问题的例程。

## 7.2 创建项目

只要程序简短，我们如何设计程序并不关键。对于较大的软件项目，例如超过 100,000 行代码的项目，源代码结构良好至关重要。

首先，程序源代码必须以明确定义的方式分布在文件中。单个文件应有多大或多小因项目而异，超出了本书的范围。在此，我们仅演示基本原则。

### 7.2.1 构建过程

从源文件到可执行文件的构建过程包含四个步骤。尽管如此，许多文件较少的程序可以通过单次编译器调用来构建。因此，“编译”一词被模糊地用于实际编译步骤（§7.2.1.2）以及由单个命令执行的整个构建过程。

图 7-3 描绘了四个步骤：预处理、编译、汇编和链接。以下各节将分别讨论这些步骤。

![](img/ba4defb7bf504868bf19451f3cd4b9bb_358_0.png)

图 7-3: 简单构建

