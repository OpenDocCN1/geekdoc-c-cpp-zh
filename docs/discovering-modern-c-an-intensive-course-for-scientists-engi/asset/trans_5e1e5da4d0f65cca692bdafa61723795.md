

| | | | | | |
|---|---|---|---|---|---|
| C1 | | | | | |
| C2 | a2,1 | | | | |
| C3 | a3,1 | a3,2 | | | |
| ... | ... | | | | |
| Cs | as,1 | as,2 | ... | cs,s-1 | |
| | b1 | b2 | ... | bs-1 | bs |

| | | | | |
|---|---|---|---|---|
| 0 | | | | |
| 0.5 | 0.5 | | | |
| 0.5 | 0 | 0.5 | | |
| 1.0 | 0 | 0 | 1.0 | |
| | 1/6 | 1/3 | 1/3 | 1/6 |

### 图 7-2: 布彻表格（Butcher tableaux）

## 7.1.3 通用实现

在 C++ 中以直截了当的方式实现上面介绍的 Runge-Kutta 方案并不会带来任何困难。例如，我们可以使用 `std::vector<double>` 来表示状态 \(\vec{x}\) 和导数 \(\vec{k}_n\)，并使用模板参数来为右端函数 \(\vec{f}(\vec{x}, t)\) 提供一定的通用性。清单 7-1 中的代码展示了上面介绍的欧拉方案的一个快速简便实现。为保持简单，我们将示例限制在欧拉方案，以使代码片段简短，但以下要点也适用于更复杂 Runge-Kutta 方案的类似实现。

### 清单 7-1: 欧拉方案的基本实现

```
typedef std::vector<double> state_type;

template<class System>
void euler_step(System system, state_type &x,
                const double t, const double dt)
{
    state_type k(x.size());
    system(x, k, t);
    for(int i=0; i<x.size(); ++i)
        x[i] += dt*k[i];
}
```

将右端系统定义为模板参数已经为我们提供了一定的通用性：`euler_step` 函数接受函数指针、仿函数以及 C++ Lambda 对象作为系统参数。唯一的要求是系统对象可按参数结构 `system(x, dxdt, t)` 调用，并且在 `dxdt` 中计算导数。

虽然此实现在许多情况下运行良好，但一旦遇到一些非标准情况，就会出现几个严重问题。此类情况可能包括：

- 不同的状态类型，即可能提供更好性能的固定大小数组（`std::array`）；
- 针对复数的常微分方程；
- 非标准容器，即用于复杂网络上的常微分方程；
- 比 `double` 更高精度的必要性；
- 并行化，例如通过 OpenMP 或 MPI；以及
- 使用 GPGPU 设备。

在接下来的部分，我们将以一种能够处理上述情况的方式推广清单 7-1 中的实现。因此，我们将首先识别 Runge-Kutta 方案的计算要求，然后逐个解决这些要求。结果将是这些算法的高度模块化实现，它将允许我们交换计算的特定部分，从而为上述问题提供解决方案。

### 7.1.3.1 计算要求

为了获得欧拉方案（清单 7-1）的通用实现，我们需要将算法与实现细节分离。为此，我们首先需要识别欧拉方案中涉及的计算要求。通过检查公式 (7.9) 或 (7.10) 以及清单 7-1 中的基本欧拉实现，我们可以识别出计算所需的几个部分。

首先，代码中必须表示数学实体，即常微分方程的状态变量 \(\vec{x}(t)\)、自变量 \(t\) 以及 Runge-Kutta 方案的常数 \(a, b, c\)。在清单 7-1 中，我们分别使用 `std::vector<double>` 和 `double`，但在通用实现中，这将变成模板参数。其次，需要进行内存分配以存储中间结果 \(\vec{k}\)。此外，需要对可能是高维的状态变量进行迭代，最后还需要执行涉及状态变量元素 \(x_i\)、自变量 \(t\)、\(\Delta t\) 以及数值常数 \(a, b, c\) 的标量计算。总结一下，之前介绍的 Runge-Kutta 方案需要以下计算组件：

- 1. 数学实体的表示，
- 2. 内存管理，
- 3. 迭代，以及
- 4. 基本计算。

在识别了这些要求后，我们现在可以设计一个通用实现，其中每个要求都由一段可交换的模块化代码来解决。

### 7.1.3.2 模块化算法

在我们的模块化设计中，我们将为之前识别的四个要求引入独立的代码结构。我们从表示数学对象所使用的类型开始：状态 \(\vec{x}\)、自变量（时间）\(t\) 以及算法的参数 \(a, b, c\)（图 7-2(a)）。将算法推广到任意类型的标准方法是引入模板参数。我们也遵循这种方法，因此定义了三个模板参数：`state_type`、`time_type` 和 `value_type`。清单 7-2 显示了带有这些模板参数的 Runge-Kutta-4 方案的类定义。

### 清单 7-2: 带模板类型的 Runge-Kutta 类

```
template<
    class state_type,
    class value_type = double,
    class time_type = value_type
    >
class runge_kutta4 {
    // ...
};
typedef runge_kutta4< std::vector<double> > rk_stepper;
```

注意，我们为 `value_type` 和 `time_type` 使用 `double` 作为默认参数，因此在大多数情况下，用户只需指定 `state_type`。

接下来，我们处理内存分配。在清单 7-1 中，这是通过 `std::vector` 构造函数完成的，该构造函数期望向量大小作为参数。对于通用 `state_type`，这已不再可接受，因为用户可能提供其他类型，例如 `std::array`，它们不是用相同的签名构造的。因此，我们引入了一个模板辅助函数 `resize` 来处理内存分配。用户可以为任何给定的 `state_type` 特化这个模板辅助函数。清单 7-3 显示了针对 `std::vector` 和 `std::array` 的实现，以及它在 `runge_kutta4` 实现中的用法。请注意，`resize` 函数根据输入状态为输出状态分配内存。这是实现此类内存分配的最通用方式；它也适用于所需大小不那么平凡的稀疏矩阵类型。清单 7-3 中的调整大小方法提供了与清单 7-1 中非通用版本相同的功能，因为 `runge_kutta4` 类再次负责其自身的内存管理。它可以立即适用于任何提供 `resize` 和 `size` 函数的向量类型。对于其他类型，用户可以提供 `resize` 重载，从而告诉 `runge_kutta4` 类如何分配内存。

接下来是计算右端方程 \(\vec{f}(\vec{x}, t)\) 的函数调用。这在清单 7-1 中已经通过模板以通用方式实现，我们将保留此解决方案。

最后，我们需要为数值计算找到抽象。如上所述，这涉及对 \(\vec{x}\) 的元素进行迭代以及对这些元素进行基本计算（求和、乘法）。我们通过引入两个代码结构：Algebra 和 Operation，分别处理这两部分。Algebra 将处理迭代，而 Operation 将负责计算。

我们从 Algebra 开始。对于 RK4 算法，我们需要两个函数，分别对三个和六个 `state_type` 实例进行迭代。考虑到 `state_type` 通常是 `std::vector` 或 `std::array`，提供一个可以处理 C++ 容器的 algebra 是合理的。为了确保我们的基本 algebra 尽可能通用，我们将使用 C++11 作为标准库一部分引入的 `std::begin` 和 `std::end` 函数。

### 清单 7-3: 内存分配

```
template<class state_type>
void resize(const state_type &in, state_type &out) {
    // standard implementation works for containers
    using std::size;
    out.resize(size(in));
}

// specialization for std::array
template<class T, std::size_t N>
void resize(const std::array<T, N> &, std::array<T,N> & ) {
    /* arrays don't need resizing */
}

template < ... >
class runge_kutta4 {
    // ...
    template<class Sys>
    void do_step(Sys sys, state_type &x,
                 time_type t, time_type dt)
    {
        adjust_size(x);
        // ...
    }
}

void adjust_size(const state_type &x) {
    resize(x, x_tmp);
    resize(x, k1);
    resize(x, k2);
    resize(x, k3);
    resize(x, k4);
}
}
```

### 建议

在通用库中使用 `std::begin` 等自由函数的正确方法是，通过 `using std::begin` 将它们局部提升到当前命名空间，然后不带命名空间限定符地访问它们，即 `begin(x)`，如清单 7-4 所示。这样，如果需要，编译器还可以通过参数相关名称查找（ADL）利用与 `x` 的类型定义在同一命名空间中的 `begin` 函数。

清单 7-4 显示了这样的 `container_algebra`。迭代在名为 `container_algebra` 的结构体的 `for_each` 函数中执行。这些函数期望若干容器对象以及一个操作对象，然后简单地对所有容器进行迭代并按元素执行给定的操作。对每个元素执行的操作是简单的乘法和加法，将在下一部分描述。

