
-   [时间测量函数执行时间]（※）的实现看似简单 – 我们需要标记开始和结束时间并计算它们的差值。我们将展示如何编写一个包装函数，用于测量任意函数的执行时间。然而，精确测量几行代码或函数执行所消耗的时间并不像表面上看起来那么容易。首先，函数本身不会单独运行；操作鼠标和连接 Internet 等后台进程也在运行。背景条件在每次运行时可能会变化，因此实际中我们测量的是函数及其伴随执行的整体耗时。

在本节中，我们扩展了表 6.4 中介绍的 `fun_perform_timer` 函数。该函数的主要局限是只能测量接受 `int` 参数并返回 `void` 的函数，但我们希望能够测量**任意**函数 – 即能够接受并返回任意参数的函数。C++ 提供了机制，可以传递任意数量、任意类型的参数。

本节将学习以下内容：

- 可变参数（参数包）
- 使用 `std::forward< decltype() >` 进行转发通用引用

众所周知，自 C++17 起，可以在另一个命名空间内定义命名空间，例如在列表 6.11 的第 [1, 4] 行。在嵌套命名空间中，第 [6] 行定义了常量 `kIterations`，它用于控制在测量执行时间时的函数调用次数。`measureFuncAvTiming` lambda 函数的定义用于执行时间测量，起始于第 [22] 行。`kIterations` 常量通过捕获传递给 `iter`。随后传入了两个有趣的参数：

- `func` – 一个转发（通用）引用，表示要执行 `iter` 次的函数对象，用于测量性能；
- `func_params` – 一个 **可变参数列表**，用于传递给 `func` 的任意参数。可变参数列表允许传递任意数量的参数。

在第 [24] 行会进行编译时检查的 compile‑time 不变量检查，确保迭代次数大于零。与运行时检查的 `assert` 不同，`static_assert` 在编译阶段验证，若条件为假则报错并停止编译。

在第 [28] 行，当前时间戳通过调用 `timer::now` 由 `time_start` 对象捕获。该函数及其他时间相关函数在 6.3 节中汇总。

在第 [31] 行的 `for` 循环中，被测试函数被调用 `iter` 次，循环范围由辅助的 `range` 类提供，后者将在 6.5 节中说明。

在第 [32, 34] 行，`func` 与 `func_params` 一起被调用。由于 `func` 与 `func_params` 可能有多种形式，我们使用 `std::forward`，其类型通过 `decltype< func >` 推导得到。类似的构造在第 [34] 行用于转发可变参数。这正是第 4.5.1 节所解释的完美转发（perfect forwarding）。

### 列表 6.11  `measureFuncAvTiming` 函数的定义（用于测量提供函数的执行时间，位于 `CppBookCode, Time.cpp`）

```cpp
namespace CppBook
{
    // 嵌套命名空间
    namespace LTimer
    {
        const int kIterations = 10;

        ////////////////////////////////////////////////////////////////
        // Lambda 用于测量任意参数的函数的执行时间。
        ////////////////////////////////////////////////////////////////
        //
        // 输入：
        //        func - 需要以 func( func_params ) 的形式被调用的函数
        // 输出：
        //        单次 func 执行的时间（毫秒）
        //
        // 备注：
        //        func 会被调用 kIterations 次，执行时间取平均
        //
        auto measureFuncAvTiming = [ iter = kIterations ]
                                   ( auto && func, auto && ... func_params )
        {
            static_assert( kIterations > 0 );     // 编译时检查

            using timer = typename std::chrono::high_resolution_clock;

            auto time_start = timer::now();

            // 执行算法若干次
            for( auto i : range( iter ) )
                std::forward< decltype( func ) >( func )
                (
                    std::forward< decltype( func_params ) >( func_params ) ...
                );

            // 计算 func 单次执行的平均时间（毫秒）
            return std::chrono::duration_cast< std::chrono::milliseconds >
                   ( timer::now() - time_start ).count()
                   /iter;
        };
    }
}
```

简要说明：任何函数 `func` 均可接受任意数量、任意类型的参数。我们的目标是保持每个 lvalue‑ref 参数为 lvalue‑ref，每个 rvalue‑ref 参数为 rvalue‑ref。完美转发正好实现这一点（Meyers 2014），否则 rvalue 参数会被强制为 lvalue‑ref，从而产生不期望的副作用。

通过结束时间与开始时间相减，`measureFuncAvTiming` 返回 `func` 单次调用的平均时长（毫秒）。可以通过调用 `std::chrono::duration_cast` 将结果转换为其他时间单位（6.3 节）。

接下来需要编写类似下面的简单函数：

```cpp
void MathFun_RandTest( int iters, double eps, double & result )
{
    // 初始化 Mersenne 双生成器
    std::mt19937 mtRandomEngine( (random_device())() );
    std::bernoulli_distribution bern( 0.7 );    // 0 或 1，概率 p=0.7

    result = 0.0;
    for( int i = 0; i < iters; ++ i )
        result += bern( mtRandomEngine );

    result /= static_cast< double >( iters ) + eps;
}
```

并使用以下代码测量其每次调用的平均执行时间：

```cpp
auto funTimer { CppBook::LTimer::measureFuncAvTiming };

double result {};

auto run_time = funTimer( MathFun_RandTest, 1234567, 1e-5, result );

cout << "MathFun_RandTest last result: " << result << endl;
cout << "MathFun_RandTest run-time: " << run_time << " [ms]" << endl;
```

在第 [62] 行，`funTimer`（即 `CppBook::LTimer::measureFuncAvTiming` 的简化别名）会多次调用 `MathFun_RandTest`，该函数计算 1 234 567 条来自伯努利分布的随机数的平均值。为此，Mersenne 随机引擎在第 [49] 行通过 `random_device` 的功能调用初始化（参见 3.17.3 节）。最终在屏幕上输出最后的平均值（应接近 0.7）以及平均单次执行时间，示例如下：

```text
MathFun last result: 0.699677
MathFun run-time: 177 [ms]
```

由此可见，返回值 0.699677 与第 [50] 行设定的 0.7 非常接近。

## 6.5  Range 类

C++11 引入了非常有用的新型 for 循环 —  — 范围 for（range for），如 3.13.2.2 节所讨论。配合 `auto` 关键字（3.7 节），它极大简化了遍历容器（如 `std::vector`、`std::list`）的操作。现在可以很容易地遍历一组值，例如：

```cpp
for( auto c : { 1, 2, 3 } )
    cout << c;
```

但如果我们想遍历由更复杂公式生成的值集合，情况会稍显繁琐。例如，从 0.0 开始，生成所有不超过 100.0 且步长为 2.56 的连续值。使用传统的 for 循环写法如下：

```cpp
for ( double f = 0.0; f < 100.0; f += 2.56 )
    cout << f << endl;
```

更便利的做法是利用新的 for 循环语法，同时能够生成各种序列。为此，我们需要一个满足以下语法的迭代器：

```cpp
range( from, to, step )
```

其中 `from` 为起始值，`to` 为结束值（不包含），`step` 为每一步的增量。还可以使用简写：

```cpp
range( from, to )          // 步长默认为 1
```

或

```cpp
range( to )                // 起始值默认为 0，步长默认为 1，生成 [0, to)
```

遗憾的是，标准库并未提供此类 helper（在某些框架中称为 linspace）。我们只能使用 `std::iota` 向 STL 容器填充递增的值。为了弥补这一不足，`range` 类被设计出来。下面在列表 6.12 中展示了 `range` 类的用法示例。

### 列表 6.12  使用 `range` 类的示例（位于 `CppBookCode, range_test.cpp`）

```cpp
#include "range.h"

void RangeTest( void )
{
    ofstream ostr( "RangeTest.txt" );
    if( ostr.is_open() == false )
        return;

    // 1:
    ostr << "1st test:" << endl;

    vector< float > v = range( 256.0f );
    copy( v.begin(), v.end(), ostream_iterator< float >( ostr, ", " ) );
```

在第 [1] 行引入 `range` 类的头文件。第 [6–11] 行创建文件并检查是否成功打开；随后生成一个 `vector<float>` 并使用 `range( 256.0f )` 初始化，得到 0、1、…、255 的连续浮点数。由于 `range` 实现了向 `std::vector` 的转换运算符，这一步骤可直接完成。最后在第 [14] 行将整个向量复制（即流式输出）到文件中。

