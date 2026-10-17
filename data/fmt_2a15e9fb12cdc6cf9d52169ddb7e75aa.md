
让我们编写一个名为 `Point` 的类，它旨在完全像我们的 `CartesianPoint` 示例那样工作，但现在拥有了构造函数。

```cpp
class Point {
public:
    Point(); // declare default constructor
    double x;
    double y;
};

Point::Point() {
    x=0.0;
    y=0.0;
}

int main() {
    Point p;
    cout << "What is the value of x?\n";
    cout << p.x;
    return 0;
}
```

在类声明中，我们现在在第 3 行有了声明 `Point();`。这声明了构造函数。

构造函数声明看起来像函数声明，除了：

- (i) 没有返回类型；
- (ii) 在函数名称的位置，你有类的名称。

同样地，构造函数定义看起来像函数定义，具有相同的差异。在上面的示例中，构造函数定义从第 8 行开始。

在我们的示例中，构造函数看起来像一个不接受参数的函数。正如我们将看到的，构造函数可以接受参数。默认构造函数只是一个不接受参数的构造函数。

你可以将构造函数视为一个在任何人被允许查看对象之前自动调用的函数。从技术上讲，它实际上不是一个函数，因为它*只能*在对象初始化时被调用，并且因为它没有返回值。

在构造函数的定义内部，你应该将所有 `int`、`double` 等字段设置为合理的默认值。更一般地说，你应该确保在任何人看到对象之前，对象处于一致的状态，并执行达到此状态所需的任何处理。

## 8.7.2 一种替代且更优的语法

这里是另一种我们可以编写 *Point* 构造函数的方法：

```cpp
class Point {
public:
   Point(); // declare default constructor
   double x;
   double y;
};

Point::Point() :
    x(0.0),
    y(0.0) {
}

int main() {
    Point p;
    cout << "What is the value of x?\n";
    cout << p.x;
    return 0;
}
```

在 `Point` 构造函数的定义中，你可以看到一个语句列表：

```cpp
x(0.0),
y(0.0)
```

这被称为初始化列表。这调用了 `x` 和 `y` 的构造函数以初始化数据。这与我们之前使用 `=` 语句初始化变量的代码略有不同。

带初始化列表的构造函数的通用语法是：

```cpp
CLASS_NAME::CLASS_NAME( PARAMETER_LIST) :
INITIALISATION_LIST {
... NORMAL CODE ...
}
```

注意初始化列表前的冒号。

经验丰富的 C++ 程序员更喜欢初始化列表，因为它稍微快一点。这是因为调用默认构造函数然后执行赋值操作比第一次就使用正确的值要慢。

此外，一旦你熟悉了这种语法，它更可读，因为很明显没有任何花哨的操作。所做的只是数据正在被初始化。这意味着你可以猜到，如果大括号之间有一些代码，它将相对有趣。

## 8.8 带参数的构造函数

编写接受参数的构造函数很简单。以下是如何向 `CallOption` 类添加一个接受行权价（strike）和到期日（maturity）作为参数的构造函数。

```cpp
class CallOption {
public:
    double strike;
    double maturity;
    CallOption(); // default constructor
    CallOption(double strike, double maturity);//alternative
};

// default constructor implementation
CallOption::CallOption():
    strike(0.0),
    maturity(0.0){
}

// alternative constructor implementation
CallOption::CallOption(
    double s,
    double m ):
    strike(s),
    maturity(m){
}
```

为了创建一个行权价为 100 且到期日为 2.0 的期权，我们可以这样写

```cpp
CallOption myOption( 100, 2.0 );
```

这似乎是一个非常方便的系统，但这可能不是一个很好的设计。原因是通过引入类，我们消除了在调用函数时记住参数顺序的问题。通过拥有一个带多个参数的构造函数，我们重新引入了这个问题！

这并不意味着带参数的构造函数总是坏的，只是你不应该过度使用它们。当然，能够构造给定大小和默认值的 `vector` *是*构造函数的一个良好用途。

有一个关于带参数构造函数的奇怪技巧你应该试着记住。考虑类 `string`。它有一个接受原始文本数据的构造函数：

```cpp
string s("Some raw text");
```

C++ 使用这个构造函数自动将原始文本数据转换为 `string`，而无需你思考。例如，代码：

```cpp
plot( "myPlot.txt", xVec, yVec );
```

即使 `plot` 的第一个参数被声明为 `const string&` 而不是 `char*`，它也能正常工作。

一般来说，如果你的类有一个接受单一参数构造函数的类，C++ 将执行类似的自动转换。虽然这对于 `string` 数据类型非常好，但通常会导致非常不自然的代码。

例如，假设你在 `BlackScholesModel` 中添加了构造函数，其中你只提供股票价格：

```cpp
class BlackScholesModel {
public:
 double stockPrice;
 double data;
 double volatility;
 double riskFreeRate;
 BlackScholesModel();
 BlackScholesModel( double stockPrice ); // 关键行
};
```

这样做意味着 C++ 将自动把 `double` 类型转换为 `BlackScholesModel` 的实例。这是一种非常奇怪的做法，通常是不希望出现的。为了防止这种非预期的行为，你应该将接受单个参数的构造函数标记为 `explicit`。

```cpp
class BlackScholesModel {
public:
 double stockPrice;
 double data;
 double volatility;
 double riskFreeRate;
 BlackScholesModel();
 explicit BlackScholesModel( double stockPrice ); // 关键行
};
```

上面的代码阻止了自动类型转换。只有在极少数自动转换有用的情况下（例如对于字符串），才可以省略 `explicit`。

如果你忘记了使用 `explicit`，也不是世界末日。在实践中，因忘记使用 `explicit` 而导致的困惑是相当罕见的。

## 练习

- 8.8.1 为你迄今创建的每个类编写一个默认构造函数。使用构造函数的两种语法形式，以便熟悉这些选项。
- 8.8.2 编写一个类 `Polynomial`，表示多项式 $a_{0}+a_{1}x+a_{2}x^{2}+...+x^{n}.$ 其中系数 $a_{i}$ 是与多项式本身关联的双精度浮点数，但 $x$ 是未知数。

类 `Polynomial` 应具备以下特性：

- 它应使用 `vector` 存储系数 $a_i$。
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

如果你尚未完成这些练习，应该尝试去做。你可以在 `FMLib9` 中找到文件 `matlib.cpp`，其中包含所有这些函数的可用版本。

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

我们还需要一个函数 `generateRiskNeutralPricePath`，其行为相同，只是它使用 $\mathbb{Q}$ 测度来计算路径。因此，我们向 `BlackScholesModel` 添加以下声明

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

(iii) 定义

$$s_{t_i} = s_{t_{i-1}} + \left(\mu - \frac{1}{2}\sigma^2\right)\delta t_i + \sigma\sqrt{\delta t_i}\epsilon_i.$$ 

(iv) 定义 $S_{t_i} = \exp(s_{t_i})$.

在 $S_{t_i}$ 处生成的股票价格将与 Black-Scholes 模型给出的具有相同的联合概率分布。

基于该算法的数学表述，实现我们的辅助函数是 straightforward（直接明了的）的。你可以在 `BlackScholesModel.cpp` 中找到代码。

```cpp
vector<double> BlackScholesModel::generatePricePath(
	double toDate,
	int nSteps,
	double drift ) const {
vector<double> path(nSteps,0.0);
vector<double> epsilon = randn( nSteps );
double dt = (toDate-date)/nSteps;
double a = (drift-volatility*volatility*0.5)*dt;
double b = volatility*sqrt(dt);
double currentLogS = log( stockPrice );
for (int i=0; i<nSteps; i++) {
	double dLogS = a + b*epsilon[i];
	double logS = currentLogS + dLogS;
	path[i] = exp( logS );
	currentLogS = logS;
}
	return path;
}
```

我们只实现了等间隔时间点的算法。将其推广到任意时间点是很简单的。

在实现了该私有函数之后，公共函数非常简单。这些实现同样放置在 `BlackScholesModel.cpp` 中。

```cpp
vector<double> BlackScholesModel::generatePricePath(
	double toDate,
	int nSteps ) const {
	return generatePricePath(toDate, nSteps, drift );
}

vector<double> BlackScholesModel::
	generateRiskNeutralPricePath(
	double toDate,
	int nSteps ) const {
	return generatePricePath(
    toDate, nSteps, riskFreeRate );
}
```

需要注意的是，通过使用一种带有**私有**辅助函数的设计，我们避免了两次编写相同的复杂代码。

测试这段代码很重要。第一个测试是视觉上的，我们想检查这是否真的看起来像一条价格路径。我们可以使用 `LineChart` 类来做到这一点。
