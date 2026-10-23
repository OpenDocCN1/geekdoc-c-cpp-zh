

+   - **Fold:** 一个 fold（或 reduction 或 accumulation）函数会遍历集合中的所有元素并在推进过程中累积一个值，例如：

```
a = [1, 2, 3, 4, 5]
print reduce(lambda x,y: x*y, a)
120.
```

在这种情况下会进行如下求值：((((1 × 2) × 3) × 4) × 5 = 120。

## 3.2.6 Eager and Lazy Evaluation

*Lazy evaluation*（或 *call-by-need*）是一种评估策略，它会延迟表达式的求值，直到其值被需要为止（这被称为 *eager* 或 *non-strict evaluation*）。例如，一种 lazy 类型是一个 *thunk* 或某个计算的 *placeholder*。一旦创建，我们就可以像它已被求值一样传递 lazy 值。该值仅在被强制求值时求值一次。Eager evaluation 是许多编程语言中的默认行为，例如 C++。

Lazy evaluation 可以导致内存占用减少，因为值仅在需要时才创建。然而，它很难与命令式语言中的特性结合，例如输入、输出和异常处理，因为操作可能变得不确定。

## 3.2.7 Fold

一个 *fold*（也称为 *reduce*、*accumulate* 或 *compress*）是一组高阶函数族，它们分析递归数据结构并以某种方式重新组合数据结构中的元素。这是通过使用一个操作来构建返回值来实现的。一般来说，一个 fold 由一个合并函数、一个数据结构的上层节点以及在某些情况下可能使用的默认值组成。

Fold 可以被视为结构转换，因为它们一致地用函数和值替换数据结构的结构组件。例如，在 Lisp 中，我们可以从两个原语构建列表，即列表要么为空，要么是通过在另一个列表前面加上一个元素构造而成。另一个例子是对列表 [1,2,3,4,5] 进行折叠，使用某种数学运算符，例如加法（运算符 +）。在这种情况下，值将为 15。我们将在第 17 章和第 18 章中看到 STL 如何支持 fold 操作，特别是当应用于数值算法时。

## 3.2.8 Continuation

一个 *continuation* 是计算机程序控制状态的抽象表示。它 *reifies*（将关于计算机程序的抽象思想转化为显式的数据模型或在编程语言中创建的其他对象）程序控制状态。换句话说，我们可以直接在编程语言中访问创建的数据结构，而不是将其隐藏在运行时环境中。Continuation 可用于编码其他控制机制，例如异常、生成器和协程。一个 *coroutine* 是计算机程序中的一个组件，它将子程序推广以允许在特定位置暂停和恢复执行的多重 *entry points*。协程非常适合实现更熟悉的程序组件，例如协作任务、迭代器、无限列表和管道。在某些语言中（例如 C#）使用 continuation 来允许顺序程序以函数式编程语义进行分析，例如在 LINQ（*Language Integrated Query*）中即可看到。使用 continuation 的缺点是代码可能难以理解。

## 3.3 NEW FUNCTIONALITY IN C++: std::function<>

类 std::function（定义在 <functional> 中）提供了多态包装器，将函数指针概念推广。其起源可以追溯到 Boost C++ Function 库（见 Demming and Duffy, 2010）。主要优点是它可以用作 *bridge* 或 *virtual machine* 来调用 *callable objects*，例如自由函数、成员函数、函数对象和 lambda 函数。为此，类 std::function<> 允许我们将这些可调用对象建模为一等对象。作为示例，我们展示如何将 std::function<> 与自由函数结合使用。让我们先定义三个函数：

```
double Func(double x)
{
    return x*x;
}
```

```
double Func2(double x)
{
    return std::sqrt(x);
}
```

```
double Func3(double x)
{
    return std::exp(x);
}
```

我们看到这些函数接受 double 作为输入参数并返回 double。为了将这些函数包含在一个通用函数包装器中，我们定义：

```
std::function<double (double x)> f;
```

然后我们可以将 f 的一个实例分配给一个自由函数或上述每个自由函数，例如：

```
// Assign to a global function
f = Func;
std::cout << "First function: " << f(2.0) << std::endl;
```

在客户端代码中，我们使用在其他地方实例化的 std::function<> 实例工作。这种方法促进了代码重用，我们将在本章和后续章节中看到更多示例，特别是如何将 std::function<> 与 lambda 函数、函数到对象和成员函数一起使用。

第二个示例是定义一个函数数组然后执行它们。我们将上述每个自由函数添加到 std::function<> 实例的数组中，并使用一个 lambda 函数（在第 3.4 节详细讨论）来执行每个函数：

```
// Create an array of functions
typedef std::function<double (double sx)> Task;
typedef std::vector<Task> Tasks;
Tasks tasks;

tasks.push_back(Func);
tasks.push_back(Func2);
tasks.push_back(Func3);

double val = 10.0;          // Captured variable
std::for_each(tasks.begin(), tasks.end(), [&val] (const Task& t)
    { std::cout << t(val) << std::endl;});
```

这个示例表明使用 std::function<> 可以实现什么。例如，我们可以用它来实现观察者模式（GOF, 1995）中的回调功能。更一般地，我们可以使用 Boost C++ signals2 库作为观察者的实现（Demming and Duffy, 2010）。

## 3.4 NEW FUNCTIONALITY IN C++: LAMBDA FUNCTIONS AND LAMBDA EXPRESSIONS

我们已经在第 3.2.5 节中从语言无关的角度介绍了 lambda 函数。这些是在其他函数作用域内声明的未命名函数。它们是 C++ 中使用全局函数和函数对象（functors）的替代方案。

### 3.4.1 Basic Syntax

lambda 函数的一般语法是：

```
[capture variables] (input arguments) <mutable> -> return type
{
    function implementation
}
```

首先，我们看到方括号 [] 的存在宣布了一个新的 lambda 函数，具有给定的返回类型。其次，lambda 函数具有输入参数以及属于 lambda 函数闭包的捕获变量。这两组变量对应于 lambda 函数的状态。可以按值或按引用捕获变量，具体取决于我们是否希望按值或按引用复制到 lambda 函数体中。我们可以通过使用以下选择来指定选择：

```
[a]      // Capture local variable 'a' by value.
[a, b]    // Capture vars 'a' and 'b' by value
[&a]      // Capture var 'a' by reference
[a, &b]   // Capture 'a' by value, 'b' by reference
[=]       // Capture all used variables by value
[&]       // Capture all used vars by reference
[=, &a]   // 'a' by ref; other vars by value
```

我们还注意到上述规范中可选关键字 mutable 的存在。这有时是必需的，因为 lambda 函数是 const，因此其状态不能被更改。因此，为了使 lambda 函数变为非 const，我们将其声明为 mutable。最后，(lambda 函数被编译成函数对象) lambda 函数的主体是标准 C++，它可以使用其输入和捕获变量。

最简单的 lambda 函数具有以下结构：

```
[]
{
    function implementation
}
```

所有 lambda 函数都有一个返回类型（可以是 void）。除非函数体包含嵌入的 if–else 逻辑，否则不需要显式指定此返回类型。我们说返回类型是推断或推导的，当它缺失时。

### 3.4.2 Initial Examples

我们现在使用 lambda 函数实现第 3.2.5 节中的示例。我们将在第 17 章和第 18 章中看到如何在 STL 中实现这些目标，但目前我们将使用 std::for_each() 算法，该算法允许我们以不同方式访问、处理和修改容器中的元素。我们假设对实现向量和列表的 STL 容器有一定的了解。三个函数（map、filter 和 fold）都从输入产生输出，为此我们使用捕获变量来存储此输出。完整代码如下：

```
#include <algorithm> // e.g. std::for_each
#include <vector>
#include <list>
#include <iostream>

typedef std::vector<int> Vector;
typedef std::list<int> List;

void print(const Vector& vec)
{
    std::for_each(vec.begin(), vec.end(), [] (double d)
        { std::cout << d << ",";});
    std::cout << "\n";
}
void print(const List& list)
```
