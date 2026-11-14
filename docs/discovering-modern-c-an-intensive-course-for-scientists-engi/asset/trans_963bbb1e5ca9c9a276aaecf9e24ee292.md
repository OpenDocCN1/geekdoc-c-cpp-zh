

由于我们为左值参数禁用了该函数，这将是一个错误。较新的编译器会告诉我们关于基于SFINAE的禁用，而较旧的编译器只是声明缺少重载（或无法编译匿名类型参数）。

当然，我们可以用`std::move`将一切声明为右值，并用这样的谎言自取其咎。相反，我们应该创建一个匿名副本，如

```
auto B = normalize(lu(permute(clone(A))));
```

这里，我们首先创建A的副本，所有变换都在此副本上执行。最终，同一副本被B的移动构造函数接管。总的来说，我们只创建了A的一个副本，其转换后的数据最终保留在B中。

### A.9.5 动态展开的基准源

```
=> c++11/vector_unroll_example.cpp
```

以下程序用于第5.4.3节的基准测试：

```
#include <iostream>
#include <chrono>
// ...

using namespace std::chrono;

template <typename TP>
double duration_ms(TP const& from, const TP& to, unsigned rep)
{
    return duration_cast<nanoseconds>((to - from) / rep).count() / 1000.;
}

int main()
{
    unsigned s = 1000;
    if (argc > 1) s = atoi(argv[1]); // read (potentially)
    // from command line
    vector<float> u(s), v(s), w(s);

    for (unsigned i = 0; i < s; ++i) {
        v[i] = float(i);
        w[i] = float(2*i + 15);
    }

    // Load to L1 or L2 cache
    for (unsigned j = 0; j < 3; j++)
        for (unsigned i = 0; i < s; ++i)
            u[i] = 3.0f * v[i] + w[i];

    const unsigned rep = 200000;
    using TP = time_point<steady_clock>;
    TP unr = steady_clock::now();
    for (unsigned j = 0; j < rep; j++)
     for (unsigned i = 0; i < s; ++i)
     u[i] = 3.0f * v[i] + w[i];
    TP unr_end = steady_clock::now();
    std::cout << "Compute time unrolled loop is "
     << duration_ms(unr, unr_end, rep)
     << " µs.\n";
}
```

### A.9.6 矩阵乘积基准

以下后向兼容的基准函数：

```
template <typename Matrix>
void bench(const Matrix& A, const Matrix& B, Matrix& C,
 const unsigned rep)
{
 boost::timer t1;
 for (unsigned j = 0; j < rep; j++)
 mult(A, B, C);
 double t = t1.elapsed() / double(rep);
 unsigned s = A.num_rows();
 std::cout << "Time mult is "
 << 1000000.0 * t << " µs. These are "
 << s * s * (2*s - 1) / t / 1000000.0 << " MFlops.\n";
}
```

在第5.4.7节中使用。

## 附录B 编程工具

在本章中，我们将介绍一些基本的编程工具，它们可以帮助我们实现编程目标。

### B.1 gcc

最流行的C++编译器之一是g++，即C编译器gcc的C++版本。该缩写曾代表Gnu C Compiler，但该编译器支持多种其他语言（Fortran、D、Ada、...），名称已更改为Gnu Compiler Collection，同时保留了缩写。本节简要介绍如何使用它。

以下命令：

```
g++ -o hello hello.cpp
```

将C++源文件hello.cpp编译为可执行文件hello。标志`-o`可以省略。然后可执行文件将命名为a.out（出于奇怪的历史原因，是"assembler output"的缩写）。一旦目录中有多个C++程序，可执行文件不断相互覆盖就会很烦人；因此最好使用输出标志。

最重要的编译器选项是

- `-I directory`: 将目录添加到包含路径；
- `-O n`: 使用级别n进行优化；
- `-g`: 生成调试信息；
- `-p`: 生成分析信息；
- `-o filename`: 将输出文件命名为filename而不是a.out；
- `-c`: 仅编译，不链接；
- `-L directory`: 下一个库的目录；
- `-D macro`: 定义宏；
- `-l file`: 与库libfile.a或libfile.so链接。

稍复杂的示例是

```
g++ -o myfluxer myfluxer.cpp -I/opt/include -L/opt/lib -lblas
```

它编译文件myfluxer.cpp，并将其与目录/opt/lib中的BLAS库链接。除标准包含路径外，还在/opt/include中搜索包含文件。

为了生成快速的可执行文件，我们必须至少使用以下标志。

- `-O3 -DNDEBUG`

`-O3`是g++中的最高优化级别。`-DNDEBUG`定义一个宏，通过条件编译（`#ifndef NDEBUG`）使`assert`在可执行文件中消失。禁用断言对性能非常重要：例如，MTL4几乎慢一个数量级，因为每次访问都会进行范围检查。相反，我们也应该为调试使用某些编译器标志：

- `-O0 -g`

`-O0`关闭所有优化并全局禁用内联，以便调试器可以逐步执行程序。标志`-g`让编译器在二进制文件中存储所有函数和变量的名称以及源代码行的标签，以便调试器可以将机器代码与源代码关联起来。关于使用g++的简短教程可在http://tinf2.vub.ac.be/~dvermeir/manual/utntr0/gpp.html上找到。

### B.2 调试

对于那些玩数独的人来说，让我们尝试做一个比较。调试程序有点像修复数独中的错误：要么快速而容易，要么非常烦人，很少介于两者之间。如果错误是最近犯的，我们可以迅速发现并修复它。当错误长时间未被发现时，它会导致错误的假设并引发一连串的后续错误。因此，在查找错误的过程中，我们会发现许多结果错误和/或自相矛盾但内部自洽的部分。原因是它们建立在错误的前提之上。对我们之前花费大量思考和工作所创造的一切表示怀疑，这非常令人沮丧。在数独的情况下，通常最好直接放弃并重新开始。对于软件开发，这并不总是一个选项。

采用精巧错误处理的防御性编程——不仅针对用户错误，也针对我们自身潜在的编程错误——不仅能带来更好的软件，而且通常也是时间上的绝佳投资。检查我们自己的编程错误（使用断言）需要相应比例的额外工作（例如，5–20%），而当错误隐藏在大型程序深处时，调试工作量可能会无限增长。

### B.2.1 文本调试器

有几种调试工具。一般来说，图形化工具更用户友好，但它们并不总是可用或可用（尤其是在远程机器上工作时）。在本节中，我们将描述gdb调试器，它对于追踪运行时错误非常有用。

以下使用GLAS [29]的小程序将作为案例研究：

```
#include <glas/glas.hpp>
#include <iostream>

int main()
{
  glas::dense_vector< int > x( 2 );
  x(0) = 1; x(1) = 2;

  for (int i= 0; i < 3; ++i)
    std::cout << x(i) << std::endl;

  return 0;
}
```

在gdb中运行该程序会产生以下输出：

```
> gdb myprog
1
2
hello: glas/type/continuous_dense_vector.hpp:85:
T& glas::continuous_dense_vector<T>::operator() (ptrdiff_t) [with T = int]:
Assertion ‘i<size_’ failed.
Aborted
```

程序失败的原因是我们无法访问x(2)，因为它超出了范围。以下是使用该程序的gdb会话输出：

```
(gdb) r
Starting program: hello
1
2
hello: glas/type/continuous_dense_vector.hpp:85:
T& glas::continuous_dense_vector<T>::operator() (ptrdiff_t) [with T = int]:
Assertion ‘i<size_’ failed.

Program received signal SIGABRT, Aborted.
0xb07ce8b3 in raise () from /lib/tls/i686/cmov/libc.so.6
(gdb) backtrace
#0  0xb7ce28b3 in raise () from /lib/tls/i686/cmov/libc.so.6
#1  0xb7ce3fa2 in abort () from /lib/tls/i686/cmov/libc.so.6
#2  0xb7cdc2df in __assert_fail () from /lib/tls/i686/cmov/libc.so.6
#3  0x08048c4e in glas::assert::continuous_dense_vector<int>::operator() (
    T&x=0xbfffdae14, i=2) at continuous_dense_vector.hpp:85
#4  0x08048ba2 in main () at hello.cpp:10
(gdb) break 7
Breakpoint 17 at 0x8048a67: file hello.cpp, line 7.
(gdb) rerun
The program being debugged has been started already.
Start it from the beginning? (y or n) y
```

