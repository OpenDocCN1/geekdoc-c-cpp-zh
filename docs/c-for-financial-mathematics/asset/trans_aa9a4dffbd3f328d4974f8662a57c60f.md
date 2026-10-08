
class BlackScholesModel {
public:
 double stockPrice;
 double data;
 double volatility;
 double riskFreeRate;
 BlackScholesModel();
 BlackScholesModel( double stockPrice ); // 关键行
};

这样做意味着 C++ 将自动把 double 类型转换为 BlackScholesModel 的实例。这是一种非常奇怪的做法，通常是不希望出现的。为了防止这种非预期的行为，你应该将接受单个参数的构造函数标记为 explicit。

class BlackScholesModel {
public:
 double stockPrice;
 double data;
 double volatility;
 double riskFreeRate;
 BlackScholesModel();
 explicit BlackScholesModel( double stockPrice ); // 关键行
};

上面的代码阻止了自动类型转换。只有在极少数自动转换有用的情况下（例如对于字符串），才可以省略 explicit。

如果你忘记了使用 explicit，也不是世界末日。在实践中，因忘记使用 explicit 而导致的困惑是相当罕见的。

## 练习

- 8.8.1 为你迄今创建的每个类编写一个默认构造函数。使用构造函数的两种语法形式，以便熟悉这些选项。
- 8.8.2 编写一个类 Polynomial，表示多项式 $a_{0}+a_{1}x+a_{2}x^{2}+...+x^{n}.$ 其中系数 $a_{i}$ 是与多项式本身关联的双精度浮点数，但 $x$ 是未知数。

类 Polynomial 应具备以下特性：

- 它应使用 vector 存储系数 $a_i$。
- 它应有一个函数 **evaluate**，该函数以 $x$ 为参数，计算多项式在 $x$ 处的值。
- 它应有一个构造函数，接受一个系数向量作为参数。
- 它应有一个函数 **add**，可用于将两个多项式相加。
- 它应有一个默认构造函数，生成常数零多项式。
- 它应有一个构造函数，接受单个双精度浮点数 $c$ 作为参数，生成常数多项式，其中 $a_0 = c$，且其他所有系数为 0。

## 8.9 摘要

- 我们学习了如何编写将数据聚合在一起的类。
- 我们学习了如何为我们的类添加成员函数。
- 我们看到使用类可以使库用户的操作变得更简单。
- 我们学习了如何使用关键字 **public** 和 **private** 来向库用户隐藏数据。
- 我们学习了术语“封装”。
- 我们学习了如何使用 `const` 关键字来指示对象是否会被调用其某个成员函数而改变。
- 我们了解到，类通常应有构造函数来初始化数据。

# 第 9 章

# C++ 中的蒙特卡洛定价

在本章中，我们将暂时从扩展我们的 C++ 知识中抽身出来，转而深入探讨一个金融示例的细节，该示例阐明了我们迄今为止所学的一切。基于此，让我们回顾一下所学内容的要点。在练习中，我们在文件 `matlib.cpp` 中编写了大量基础数学功能。特别是我们可以：

- i) 使用 `randUniform` 和 `randn` 生成随机数（练习 7.7.5 和 7.7.6）
- ii) 使用 `plot` 和 `hist` 生成图表（练习 7.7.8 和 7.7.10）。
- iii) 使用 `min`、`mean`、`prctile` 等计算向量的统计量（练习 7.7.2、7.7.4 和 7.7.9）

我们还学习了如何编写简单的类。

如果你尚未完成这些练习，应该尝试去做。你可以在 FMLib9 中找到文件 `matlib.cpp`，其中包含所有这些函数的可用版本。

在本章中，我们将执行以下操作：

- i) 为 `BlackScholesModel` 添加一个模拟股价的函数。
- ii) 使用 `mean` 等测试我们的模拟结果，并使用 `plot` 绘制图表。
- iii) 编写一个类 `MonteCarloPricer`，该使用 `BlackScholesModel` 模拟股价，然后使用无风险定价法通过蒙特卡洛方法对 `CallOption` 进行定价。

通过这样做，我们将看到所学习的所有 C++ 知识如何应用于解决实际的金融数学问题。

当然，使用蒙特卡洛方法对欧式看涨期权进行定价是不必要的，因为人们已经知道 Black–Scholes 公式。然而，这是一个有价值的练习，因为它阐明了蒙特卡洛定价的一般思想。在练习中，你将稍微扩展这些思想，以对没有解析公式的路径依赖型期权进行定价。

在开始编写代码之前，让我们回顾附录 A 中论证过的蒙特卡洛定价算法。

**算法 1.** 要计算期权在无风险利率下的价格，该期权的收益由时间点 $t_1, t_2, \dots, t_n$ 的价格给出，应按以下步骤进行：

1. 在 $\mathbb{Q}$ 测度下模拟股价路径。所谓股价路径，指的仅仅是股价在时间 $t_i$ 的一种可能实现。典型的股价路径如图 9.1 所示。
2. 计算每条价格路径的收益。
3. 计算折现平均值。这给出了真实无风险价格的无偏估计。

在本章中，我们将首先编写一个函数来模拟遵循几何布朗运动的股价。该过程由方程 (A.8) 描述。当该几何布朗运动的漂移率 $\mu$ 设置为等于无风险利率 $r$ 时，我们将生成无风险测度下的股价，如方程 (A.5) 所述。在编写完此类之后，我们将编写一些测试以确认我们的模拟是正确的。

接下来，我们将使用这些股价路径通过蒙特卡洛方法计算欧式看涨期权的价格。同样，我们将编写测试以确认我们的答案是正确的。

## 9.1 模拟股价的函数

我们希望编写一个函数 **generatePricePath** 来生成模拟的股价路径。它将接收最终日期 **toDate** 和步数 **nSteps** 作为参数。

由于我们要根据 Black–Scholes 模型的离散时间版本生成价格路径，我们选择使函数 **generatePricePath** 成为名为 **BlackScholesModel** 的类的成员函数。这是合乎逻辑的，因为我们需要生成价格路径的关键数据是漂移率 $\mu$ 和波动率 $\sigma$。这些已经是 **BlackScholesModel** 的成员变量。此外，通过将该函数作为 **BlackScholesModel** 的成员添加，可以立即看出 **generatePricePath** 函数将生成遵循几何布朗运动的价格，这是 Black–Scholes 模型所要求的。

该函数的规范实际上告诉我们需要在头文件中编写什么。

```cpp
class BlackScholesModel {
    public:
        ... other members of BlackScholesModel ...

std::vector<double> generatePricePath(
 double toDate,
 int nSteps) const;
};
```

如本例所示，类声明描述了类的功能，而没有详细描述其实现方式。如果你选择好的函数名和变量名，就不需要太多的注释。设计良好的类几乎可以自我文档化。

我们还需要一个函数 generateRiskNeutralPricePath，其行为相同，只是它使用 $\mathbb{Q}$ 测度来计算路径。因此，我们向 BlackScholesModel 添加以下声明

```cpp
class BlackScholesModel {
public:
... other members of BlackScholesModel ...

std::vector<double> generateRiskNeutralPricePath(
 double toDate,
 int nSteps) const;
};
```

为了实现这些函数，我们引入一个 *private* 函数，允许你在价格路径模拟中选择漂移率。

```cpp
class BlackScholesModel {
... other members of BlackScholesModel ...
private:
std::vector<double> generateRiskNeutralPricePath(
 double toDate,
 int nSteps,
 double drift) const;
};
```

该函数是 *private* 的，因为我们创建它只是为了简化实现。类的用户不需要（甚至不想要）知道它。

为了实现该函数，我们需要知道要使用什么算法。相关的数学推导如下给出（并在附录 A 中给出动机）。

**算法 2.** *要模拟遵循离散时间几何布朗运动的股价，其漂移率为 $\mu$，波动率为 $\sigma$，在离散时间 $t_0, t_1, \dots t_n$，应按以下步骤进行：*

(i) *定义*
$$\delta t_i = t_i - t_{i-1}.$$ 
(ii) *选择独立的正态分布 $\epsilon_i$，其均值为 0，标准差为 1。*

