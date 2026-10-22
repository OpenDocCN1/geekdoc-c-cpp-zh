

![](img/0d5072d8203dcaf6ef50e76a3d9a3203_464_0.png)

图 18.5. NIHCL 的类层次结构

与 C++ 标准库类似，NIHCL 也支持丰富的容器以及迭代器。然而，其实现遵循了 Smalltalk 风格的动态多态：迭代器使用抽象基类 Collection 来操作不同类型的集合：Bag c1; Set c2; ... Iterator i1(c1); Iterator i2(c2); ... 不幸的是，这种方法的代价在运行时间和内存使用方面都很高。运行时间通常比使用 C++ 标准库的等效代码差几个数量级，因为大多数操作最终都需要一次虚函数调用，而在 C++ 标准库中，许多操作都是内联的，并且迭代器和容器接口中不涉及虚函数。此外，由于与 Smalltalk 不同，接口是受限的，内置类型必须包装在更大的多态类中，NIHCL 提供了这样的包装器，这反过来可能导致存储需求急剧

增加。

即使在今天模板盛行的时代，许多项目在处理多态的方法上仍然做出次优选择。显然，在许多情况下，动态多态是正确的选择。异构迭代就是一个例子。然而，同样地，许多编程任务天然且高效地使用模板来解决，而同构容器就是一个例子。

静态多态非常适合代码基础的计算结构。相比之下，需要选择一个共同的基类型意味着动态多态库通常必须做出领域特定的选择。因此毫不奇怪，C++ 标准库的 STL 部分从未包含多态容器，但它包含了一套丰富的容器和迭代器，它们使用静态多态，如第 18.6 节第 380 页所示。

中等和大型 C++ 程序通常需要处理本章讨论的两种多态。在某些情况下，甚至有必要非常紧密地将它们结合起来。在许多情况下，根据我们的讨论，最优的设计选择是明确的，但花一些时间思考长期、潜在的演进几乎总是有回报的。

1 多态一词 literally 指的是具有多种形式或形状的状态，源自希腊语 polymorphos。

2 严格来说，宏也可以被视为一种早期的静态多态形式。然而，它们被排除在考虑之外，因为它们在很大程度上与其它语言机制正交。

3 也就是说，多态基类子对象的编码包含了一些启用这种运行时分派的、 mostly 隐藏的数据。

4 有关多态术语的详细讨论，请参阅 [CzarneckiEiseneckerGenProg] 的第 6.5 至 6.7 节。

5 例如 GCC 7 提供了选项 -fconcepts。

## 第 19 章

## 实现 Traits

模板使我们能够为各种类型参数化类和函数。引入尽可能多的模板参数以实现类型或算法的每个方面的定制似乎很有诱惑力。这样，我们的“模板化”组件就可以实例化以满足客户端代码的精确需求。然而，从实际角度来看，为最大化参数化而引入数十个模板参数很少是可取的。在客户端代码中指定所有相应的参数过于繁琐，并且每个额外的模板参数都会使组件与其客户端之间的契约变得复杂。

幸运的是，我们发现我们将引入的大多数额外参数都有合理的默认值。在某些情况下，额外参数完全由几个主要参数决定，我们将看到此类额外参数可以完全省略。其他参数可以赋予依赖于主要参数的默认值，这将满足大多数情况的需求，但默认值有时必须被覆盖，用于特殊应用。还有一些参数与主要参数无关：从某种意义上说，它们本身就是主要参数，只是存在几乎总是合适的默认值。

Traits 或 traits 模板是 C++ 编程装置，可极大地促进在工业级模板设计中出现的此类额外参数的管理。在本章中，我们展示了它们在许多情况下证明有用的情况，并演示了各种技术，使您能够编写自己的健壮而强大的装置。

这里介绍的大多数 traits 在某种形式下可在 C++ 标准库中使用。然而，为了清晰起见，我们经常展示简化的实现，这些实现省略了工业级实现中存在的一些细节，如标准库中的实现。因此，我们也使用自己的命名方案，它可以轻松映射到标准 traits。

### 19.1 一个示例：累加一个序列

计算一系列值的总和是一个相当常见的计算任务。然而，这个看似简单的问题为我们提供了一个很好的例子来介绍策略类和 traits 可以在不同层面上提供帮助。

### 19.1.1 固定的 Traits

让我们首先假设我们要计算的总和的值存储在一个数组中，并且我们得到一个指向要累加的第一个元素的指针和一个指向要累加的最后一个元素之后位置的指针。因为本书是关于模板的，我们希望编写一个适用于许多类型的模板。以下内容到现在可能看起来很简单：¹

Click here to view code image

traits/accum1.hpp

```
#ifndef ACCUM_HPP
#define ACCUM_HPP

template<typename T>
T accum (T const* beg, T const* end)
{
T total{}; // assume this actually creates a zero value
while (beg != end) {
total += *beg;
++beg;
}
return total;
}

#endif //ACCUM_HPP
```

这里唯一稍微微妙的决定是如何创建正确类型的零值来开始我们的求和。我们在这里使用值初始化，使用 {...} 记法，如第 5.2 节第 68 页所述。它意味着局部对象 total 是通过其默认构造函数初始化的，或者通过零初始化，这意味着指针为 nullptr，布尔值为 false。

为了说明我们的第一个 traits 模板，请考虑以下使用 accum() 的代码： Click here to view code image

traits/accum1.cpp

```
#include "accum1.hpp"
#include <iostream>

int main()
{
// create array of 5 integer values
int num[] = { 1, 2, 3, 4, 5 };

// print average value
std::cout << "the average value of the integer values is "
<< accum(num, num+5) / 5
<< '\n';

// create array of character values
char name[] = "templates";
int length = sizeof(name)-1;

// (try to) print average character value
std::cout << "the average value of the characters in \""
<< name << "\" is "
<< accum(name, name+length) / length
<< '\n';
}
```

在程序的前半部分，我们使用 accum() 对五个整数值求和：

Click here to view code image

```
int num[] = { 1, 2, 3, 4, 5 };
...
accum(num0, num+5)
```

然后平均整数值是通过简单地将结果总和除以数组中的值数量得到的。

程序的后半部分尝试对单词 templates 中的所有字母执行相同的操作，前提是字符 a 到 z 在实际字符集中形成连续序列，这对 ASCII 为真，但对 EBCDIC 不为真。² 结果应该在 a 的值和 z 的值之间。在今天的大多数平台上，这些值由 ASCII 码决定：a 编码为 97，z 编码为 122。因此，我们可能期望结果在 97 到 122 之间。然而，在我们的平台上，程序的输出如下： Click here to view code image

```
the average value of the integer values is 3
the average value of the characters in "templates" is -5
```

问题在于我们的模板被实例化为类型 char，而该类型对于累加即使是相对较小的值来说范围也太小了。显然，我们可以通过引入一个额外的模板参数 AccT 来解决这个问题，该参数描述用于变量 total 的类型，并且因此

