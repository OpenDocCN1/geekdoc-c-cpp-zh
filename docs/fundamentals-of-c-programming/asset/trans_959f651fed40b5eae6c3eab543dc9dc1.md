

（不要与表示将某事铭记于心的单词 memorization 混淆）。备忘录法是一种算法设计技术，它记录特定计算的结果，以便在算法执行过程中需要时稍后使用该结果。仿佛执行中的程序“给自己做个笔记”或“将结果存储在备忘录中”。当程序未来需要相同计算的结果时，它只需读取之前存储的备忘录中的答案即可。这样一来，程序就避免了重复工作。备忘录法对于由重叠子问题组成且看似需要对相同输入进行多次计算的问题尤其有用。

```cpp
// Returns the nth Fibonacci number. Caches a
// recursively computed result to be used when needed
// in the future. Provides a huge performance improvement
// over the recursive version.
int fibonacci12(int n) {
    // Map for caching the results of the fib function
    // ans is declared static so it retains its value between
    // calls to fibonacci12.
    // Precomputes the results for 0 and 1.
    static unordered_map<int, int> ans({{0, 0}, {1, 1}});
    if (n > 1 && ans[n] == 0) // Need to compute?
        ans[n] = fibonacci12(n - 2) + fibonacci12(n - 1);
    return ans[n];
}
```

fibonacci12 函数使用 unordered map 作为缓存，存储在程序执行期间持续存在的值。由于 ans 局部变量是 static 的，运行时环境在执行 main 函数之前会使用键 0 和 1 创建并初始化它。当调用者调用 fibonacci12 时，如果答案不在 ans 中，它会计算结果并将结果存储在 ans 中以供将来使用。这不仅有助于外部对函数的未来调用，还能加快必须执行相同工作的递归调用。

清单 21.21 (fibonacci.h) 声明了 fibonacci1 和 fibonacci12 的接口，这两个函数用于计算第 n 个斐波那契数：

```cpp
Listing 21.21: fibonacci.h
#ifndef FIBONACCI_H_DEFINED
#define FIBONACCI_H_DEFINED
// Values in the range 0..18,446,744,073,709,551,615 on Windows
using Integer = unsigned long long;
// Returns the nth Fibonacci number using
// recursion without memoization
Integer fibonacci(unsigned n);
// Returns the nth Fibonacci number using recursion
// with memoization. Provides a huge performance improvement
// over the pure recursive version.
Integer fibonacci12(unsigned n);
#endif
```

斐波那契数增长非常快，因此清单 21.21 (fibonacci.h) 中的函数返回 unsigned long long 值。为方便起见，它为 unsigned long long 引入了类型别名 Integer 以简化代码。例如，在 Visual C++ 下，此类型支持 0 到 18,446,744,073,709,551,615（含）范围内的值。清单 21.22 (fibonacci.cpp) 提供了这两个函数的实现。

```cpp
Listing 21.22: fibonacci.cpp
#include <unordered_map>
#include "fibonacci.h"

// Returns the nth Fibonacci number
Integer fibonacci(unsigned n) {
    if (n < 0)
        return 0;
    else if (n == 1)
        return 1;
    else
        return fibonacci(n - 2) + fibonacci(n - 1);
}

// Returns the nth Fibonacci number. Caches a
// recursively computed result to be used when needed
// in the future. Provides a huge performance improvement
// over the recursive version.
Integer fibonacci2(unsigned n) {
    // ans is a map for caching the results of the fibonacci2 function.
    // Declared static so it persists between function calls.
    // Precomputes the results for 0 and 1.
    static std::unordered_map<unsigned, Integer> ans {{0, 0}, {1, 1}};
    if (n > 1 && ans[n] == 0)
        ans[n] = fibonacci2(n - 2) + fibonacci2(n - 1);
    return ans[n];
}
```

与清单 21.22 (fibonacci.cpp) 中的代码一起编译和链接后，清单 21.23 (testfib.cpp) 验证 fibonacci2 函数在给定相同参数时与 fibonacci 函数产生相同的结果。它测试最高达 50 的 unsigned 值。你会观察到，随着参数变大，程序打印结果所需的时间会更长。

```cpp
Listing 21.23: testfib.cpp
#include <iostream>
#include "fibonacci.h"

// Compares the behaviors of the fibonacci and fibonacci2 functions.
int main() {
    // Print the first 50 Fibonacci numbers
    for (unsigned i = 0; i < 50; ++i) {
        std::cout << "i = " << i << " fibonacci(i) " << " "
                  << fibonacci2(i) << "\n";
    }
}
```

以下显示清单 21.23 (testfib.cpp) 输出的前 20 行：

```
0: 0 0
1: 1 1
2: 1 1
3: 2 2
4: 3 3
5: 5 5
6: 8 8
7: 13 13
8: 21 21
9: 34 34
10: 55 55
11: 89 89
12: 144 144
13: 233 233
14: 377 377
15: 610 610
16: 987 987
17: 1597 1597
18: 2584 2584
19: 4181 4181
20: 6765 6765
```

总共，所有 50 行都匹配，这让我们确信我们的备忘录版本是正确的。

清单 21.24 (timefib.cpp) 揭示了备忘录函数相比非备忘录版本执行快了多少。

### 清单 21.24: timefib.cpp

```cpp
#include <iostream>
#include <ctime>
#include <functional>

#include "Fibonacci.h"

// f is a function that accepts a single parameter, n is a number
// to pass to the function.
// Measures the time for function f to execute given parameter n.
// Returns the cumulative elapsed time in milliseconds.
unsigned time_it(const std::function<Integer(unsigned)>& f, unsigned n) {
  clock_t start_time = clock();
  f(n);
  clock_t end_time = clock();
  return static_cast<unsigned>(end_time - start_time); // Return elapsed time
}

// Tests the performance of the fibonacci and fibonacci2 functions.
int main() {
  auto t1 = time_it(fibonacci, 50);
  auto t2 = time_it(fibonacci2, 50);
  std::cout << "Time: " << "fibonacci = " << t1 << " msec, fibonacci2 = "
            << t2 << " msec\n";
}
```

运行清单 21.24 (timefib.cpp) 一次会打印

图 21.1 由调用 fibonacci2(5) 产生的递归函数调用层次结构。请注意，树右侧的 fibonacci(2) 和 fibonacci(3) 调用不需要递归调用；这是因为树左侧较早的调用已将它们的结果存储在 map 中以便即时检索。

![](img/e84ad11adb18201d71595b31ce6c9eff_746_0.png)

```
Time: fibonacci = 111430 msec, fibonacci2 = 1 msec
```

原始递归版本需要超过 111 秒（近两分钟），而备忘录递归版本仅需 1 毫秒。在此次运行中，备忘录版本快了超过 100,000 倍。fibonacci2 函数之所以如此快，是因为它避免了 fibonacci 函数必须计算的所有冗余递归调用。

清单 21.24 (timefib.cpp) 提供了一个诚实的测试，因为它强制 fibonacci2 立即计算第 50 个斐波那契数，且没有先前的 fibonacci2 调用。完成 fibonacci2(n) 的调用后，0...n 范围内的所有斐波那契数都将出现在该函数的 unordered_map 预计算值缓存中。这意味着未来涉及该范围内任何值的调用都将非常快。任何在执行期间需要多次计算斐波那契数的程序都将特别受益于备忘录版本。

图 21.1 显示了我们的备忘录斐波那契函数计算第五个斐波那契数的递归树。该图仅显示了 fibonacci2 的九次调用，而非备忘录 fibonacci 函数则有 15 次调用。如果将清单 21.20 (fibonacciinstrumented.cpp) 中使用的函数调用计数插桩添加到 fibonacci2，你会发现它报告的数字与图 21.1 一致。

## 第 22 章

### 异常处理

![](img/e84ad11adb18201d71595b31ce6c9eff_748_0.png)

在迄今为止的编程经验中，我们遇到了几种运行时错误。到目前为止，所有运行时错误都导致执行中的程序终止。C++ 提供了一个异常处理框架，允许程序员处理某些类型的运行时错误。异常处理基础设施并非始终终止程序的执行，而是使程序员能够检测问题并执行代码以纠正问题或以其他方式管理它。本章探讨 C++ 的异常处理机制。

### 22.1 动机

算法设计可能很棘手，因为细节至关重要。编写解决一般情况问题的算法可能很简单，但可能存在许多特殊情况，都必须在算法中加以处理，算法才能正确。这些特殊情况中的一些可能在最非同寻常的情况下很少发生。为了使实现算法的代码健壮，必须正确处理这些异常情况；然而，向算法添加必要的细节可能会使其过于复杂且难以正确构建。这种过于复杂的算法对其他人来说难以阅读和理解，也更难调试和扩展。

理想情况下，开发者会以算法的一般形式表达算法，包括任何常见的特殊情况。那些应该很少发生的异常情况，以及处理它们的策略，可以出现在其他地方，也许作为算法的注释。这样，算法就专注于解决当前问题，而处理异常情况的措施则在其他地方处理。

C++ 的异常处理基础设施允许程序员将实现专注算法的代码与处理算法可能面临的异常情况的代码清晰地分开。这种方法更加模块化，并鼓励开发更清晰、更易于维护和调试的代码。

异常是程序执行期间发生的异常事件。异常始终是可能的，但它应该是一个相对罕见的事件。如果它不罕见，那它就是习惯性的或预期的事件，程序应将其作为正常处理的一部分来处理。

异常几乎总是代表一个问题，通常是某种运行时错误。假设我们有

