

```cpp
{
    St[j] = edxud*St[j-1];
}

// Option value at maturity (t = N)
std::vector<double> C(N+1);
for (std::size_t j = 0; j < C.size(); ++j)
{
    if (St[j] > H)
    {
        C[j] = std::max<double>(St[j] - K, 0.0);
    }
    else
    {
        C[j] = 0.0;
    }
}

// Backwards induction phase
for (int i = N-1; i >= 0; --i) // Can't use std::size_t as index
{
    for (std::size_t j = 0; j <= i; ++j)
    {
        St[j] /= edxd;

        if (St[j] > H)
        {
            C[j] = dpd*C[j] + dpu*C[j+1];

            // Early exercise condition
            C[j] = std::max<double>(C[j], St[j] - K);
        }
        else
        {
            C[j] = 0.0;
        }
    }
}

}

// Early exercise down and out call
return C[0];
}
```

一个简单的测试程序如下：

```cpp
int main()
{

    double K = 100.0;
    double S = 100.0;

    double T = 1.0;
    double r = 0.06;
    double q = 0.0;
    double sig = 0.2;

    int N = 3;

    double H = 95;
    double optionPrice = price(K,T,S,sig,r,H,N);

    std::cout << "Price:" << optionPrice << std::endl;

    return 0;
}
```

上述代码不够灵活，我们将看到如何将其泛化。它并非出于可维护性的考虑而编写。另请参见练习1。

## 11.4.1 分层系统模式

从11.4节的代码示例可以清楚地看出，我们需要某种策略来创建一个灵活的软件框架，以支持我们使用格方法实现的一系列期权定价问题。我们已经看到，上述代码不满足我们的需求，因此需要一种新方法。在Duffy (2006A)中，我们将面向对象模型与GOF设计模式结合使用，这种方法提供了一定的灵活性。然而，该设计存在许多局限性，例如：

- 它基于对象，使用了子类型多态和类层次结构。使用对象技术并不总是必要的。
- 类之间的紧耦合。
- 由于缺乏合适的模式以及C++语言本身的限制，如何配置和初始化应用程序并不总是清晰的。
- 随着新需求添加到软件框架中，类的数量会激增。我们创建了类和类层次结构，但函数对象和lambda函数可能更合适。

尽管如此，Duffy (2006A)中的设计方法相对于11.4节中给出的硬编码解决方案是一种改进。该代码可以用作更灵活设计的需求。

我们现在提出一种基于分层系统模式的设计（完整讨论见POSA, 1996）。当前问题可以建模为一组松散耦合且内聚的组件，以使用层次结构的形式组织；给定层级的组件使用相同或更低层级组件的服务，但给定层级的组件不了解更高层级的组件。这种方法促进了松散耦合，并用于许多期权定价问题（属性A1使用整数索引）以及更广义的格，其中属性A1的索引空间可以是更一般的数据类型，例如Boost日期。当我们希望直接使用日期以及处理百慕大期权定价问题时，需要这种灵活性。本书不讨论使用日期作为行索引空间。

*最简单的格* ADT使用整数作为索引。我们使用嵌套的STL向量来实现它：

```cpp
// The Node class contains the values of interest.
// LatticeType == 2 for binomial, 3 for trinomial.

template <class Node, int LatticeType> class Lattice
{ // Generic lattice class

private:

    // Implement as a full nested vector class
    std::vector<std::vector<Node> > tree;

    // ...
};
```

*广义格* ADT有一个额外的模板参数，支持属性A1的非整数索引：

```cpp
template <typename TimeAxis, typename Node, int LatticeType>
    class GeneralisedLattice
    { // Generic lattice class

    // Implement as an STL map
    std::map<TimeAxis, std::vector<Node> > tree;

    // ...
};
```

这里我们将索引空间实现为map。这两种格类具有相似的接口，我们在此总结如下：

- 构造函数，例如创建具有给定行数（时间步数）的格。
- 访问给定行的数据，或访问给定行和给定列的数据。
- 在格中迭代时有用的成员函数。

我们现在给出一些初始示例。首先创建一个二叉树格和一个三叉格：

```cpp
// Create basic lattices
const int TYPEB = 2;    // BinomialLatticeType;
```

## STOP 标志

STOP 标志是道路交通中重要的禁止标志，要求驾驶人在交叉路口前将车辆完全停下，观察周边交通情况后再通行。

- 必须在停止线前完全停车
- 让行右侧来车
- 确认安全后方可通行

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_353_0.png)

```cpp
// Generate edge values
lattice1(j,0) = lattice1(j-1,0);
lattice1(j,lattice1.MaxIndex(j)) = lattice1(j-1,lattice1.MaxIndex(j-1));

// Generate the interior values
for (std::size_t i = 1; i < lattice1[j].size()-1; ++i)
{
    lattice1(j,i)=lattice1(j-1,i)+lattice1(j-1,i-1);
}
LatticeMechanisms::print(lattice1);
```

这些示例展示了如何创建格以及访问和修改其值。你可以运行代码并检查输出。

我们现在创建一个广义格，其行索引集为Boost日期类型。首先创建一组将构成行轴的固定日期：

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>

// Dates as axis
namespace Dates = boost::gregorian;

// Simple dates for illustrative purposes
std::set<Dates::date> fixingDates;
Dates::date myDate(2014, Dates::May, 16);
fixingDates.insert(myDate);
Dates::date myDate2(2014, Dates::May, 26);
fixingDates.insert(myDate2);
Dates::date myDate3(2014, Dates::Jun, 2);
fixingDates.insert(myDate3);
Dates::date myDate4(2014, Dates::Jun, 12);
fixingDates.insert(myDate4);
```

然后我们基于这些固定日期创建一个广义格：

```cpp
GeneralisedLattice<Dates::date,double, 3> lattice2(fixingDates);
GeneralisedLatticeMechanisms::print(lattice2);
```

一个有用的项目是扩展功能以支持日期。

## 11.4.3 第2层：格上的操作

第1层的功能主要涉及对格结构进行建模的泛型类。总体而言，重点在于为这些结构分配内存，并使用运算符重载来访问格的元素。此功能符合SRP。这些ADT可用于多种应用（在本书中，我们主要关注期权定价）。我们开发代码以在格中迭代、在应用中使用格以及访问格中的元素。为此，我们在第2层创建了实现这些特性的泛型代码。过去（Duffy, 2006A），我们使用了面向对象的方法，导致代码有些不够灵活，并给框架引入了耦合。随着C++11的出现，我们现在有机会提高框架的通用性和可维护性。在本章中，我们讨论以下特性：

- 元组，我们将其用作函数的返回类型或函数的输入参数。
- 函数类型包装器 `std::function<>`。这是一个*基于签名的特性*，它减少了组件之间的耦合，因为它是一个规范，其实现被推迟到第3层的代码中。我们在第3章和第4章中已经看到，函数类型包装器可以实现为*可调用对象*，如自由函数、静态成员函数、对象成员函数（与`std::bind<>`结合）、函数对象和lambda函数。
- Lambda函数，用于框架的第3层。
- 使用关键字 `auto` 进行自动类型推导。此功能有助于使代码更具可读性，并减轻编程的枯燥性。

我们还指出，可以创建输入参数和返回类型均为元组的函数包装器。也可以创建元素为函数包装器的元组。

创建格之后，我们接着讨论使用或修改其元素的算法。为了缩小范围，我们专注于著名的*前向*和*后向归纳算法*（参见Clewlow and Strickland, 1998; Duffy, 2006A; Duffy and Germani, 2013）。通常，我们以不同方式访问和修改二叉树格和三叉格，例如：

- U1：前向归纳（使用*向上*和*向下*参数创建格）。
- U2：计算每个最终节点（到期日/行权日）的收益。
- U3：后向归纳（从到期日开始计算更早节点的期权价值）。

其他一些用例包括：

- U4：计算对冲敏感性。
- U5：针对支付股息资产的格模型。
- U6：为路径依赖期权定价。
- U7：计算美式看跌期权的价格。
- U8：双因子格方法。

为此，我们创建了四个自由函数来实现前向和后向归纳，一组用于普通期权，另一组用于美式期权。我们还对二叉树格和三叉格进行了区分。还有机会使代码更加优雅。我们还使用了函数包装器和元组。

