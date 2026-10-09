
double getStrike() const {
    return strike;
}
void setStrike(double strike) {
    this->strike = strike;
}
// ... more methods ...
private:
double maturity;
double strike;
};

注意我们的基类有一个虚析构函数。

virtual ~ContinuousTimeOptionBase() {}

我们之前曾在接口类中见过这种用法。正如接口类一样，任何用作基类的类都必须拥有虚析构函数。

现在我们可以编写一个“继承”自基类的 PutOption 类。它将自动“继承”所有函数。

class PutOption : public ContinuousTimeOptionBase {
public:

    /* Calculate the payoff of the option given
       a history of prices */
    double payoff(
        const std::vector<double>& stockPrices
    ) const;

    double price( const BlackScholesModel& bsm )
        const;

    bool isPathDependent() const {
        return false;
    };
};

代码的第一行表明 PutOption 类扩展了 ContinuousTimeOptionBase 类。

class PutOption : public ContinuousTimeOptionBase {

这意味着在 ContinuousTimeOptionBase 中定义的所有方法都会自动提供给 PutOption，因此我们无需再次编写它们。

特别是，PutOption 继承了 `getMaturity`、`getStrike` 等函数，以及数据 `maturity` 和 `strike`。没有必要重新声明或重新定义这些内容。

此外，PutOption 从 ContinuousTimeOptionBase 继承了 ContinuousTimeOption 接口。因此，PutOption 将自动成为 ContinuousTimeOption 的一个实例。

class ContinuousTimeOptionBase :
    public ContinuousTimeOption {

请注意，我们在 C++ 中使用相同的记号来表示扩展类或实现接口。

## 12.3.1 我们获得了什么？

到目前为止，我们似乎只是让事情变得更复杂了。但现在我们可以轻松编写以下类：

- CallOption,
- DigitalCallOption,
- DigitalPutOption,
- UpAndOutOption.

如果它们都扩展 ContinuousTimeOptionBase，我们就不需要为其中任何一个编写 `getMaturity`、`getStrike` 等方法了。

这消除了一大量重复代码。请注意，接口概念本身（即一组必须由所有类实现的固定方法）自然会导致某种程度的代码重复。你应该使用继承来避免这种代码重复。

### 12.3.2 术语

各种术语用来描述 PutOption 和 ContinuousTimeOptionBase 之间的关系。

- ContinuousTimeOptionBase 被称为 PutOption 的*超类*或*父类*。
- PutOption 被称为 ContinuousTimeOptionBase 的*子类*或*子*类*。
- PutOption *扩展*自 ContinuousTimeOptionBase。
- PutOption *继承*自 ContinuousTimeOptionBase。

## 12.4 重写方法 — virtual 关键字

让我们向 ContinuousTimeOptionBase 添加一个新方法，用于根据定价模型对期权进行定价。

class ContinuousTimeOptionBase
    : public ContinuousTimeOption {
public:
    /* Price the option, by Monte Carlo or otherwise */
    double price(
        const BlackScholesModel& model) const;
    // ... other members ...
};

若使用蒙特卡洛方法实现该方法，我们只需使用以下代码：

double ContinuousTimeOptionBase::price(
    const BlackScholesModel& model ) const {
    MonteCarloPricer pricer;
    return pricer.price( *this, model );
}

这种实现对于所有期权类型都相当适用，但并非一定是最优的。例如，PutOption 最好通过解析法而非蒙特卡洛法进行定价。

因此，我们希望能够*重写*默认实现。关键字 virtual 意味着函数可以在子类中被重写。因此，我们必须将其添加到 *price* 的声明中。

class ContinuousTimeOptionBase
    : public ContinuousTimeOption {
public:
    /* Price the option, by Monte Carlo or otherwise */
    virtual double price(
        const BlackScholesModel& model) const;
    // ... other members ...
};

如果你希望在子类中重写某个方法，你应该执行以下操作：

- (i) 检查该超类中是否将其声明为 *virtual*。
- (ii) 在你的子类中使用完全相同的参数和返回类型（以及 *const* 的使用）进行声明。可选地，你可以使用 *override* 关键字，以便编译器检查你是否正确执行了此操作。
- (iii) 你必须提供新的实现，以覆盖默认行为。

以下是 PutOption 类的一个示例。

class PutOption : public ContinuousTimeOptionBase {
public:
    double price(const BlackScholesModel& bsm)
        const override;
    // ... other members ...
};

这意味着 PutOption 拥有一个不同于默认 price 函数的 price 函数。该方法的实现就是我们要看过的常规 Black–Scholes 定价公式。

override 关键字不会影响程序运行时的行为。它只是一种表明你意图是重写某个函数的方式。如果你不使用这个关键字并且在函数的参数类型列表中犯了小错误，编译器可能不会注意到你的错误。这可能导致难以发现的 bug。因此，当你希望重写函数时，使用 override 是明智之举。

当你在期权上调用 price 时，会根据期权的类型自动选择合适的 price 方法。这将允许我们在下一章中编写一个类来对整个期权投资组合（Portfolio）进行定价。

### 12.4.1 关于 virtual 关键字的说明

virtual 关键字意味着“可以被重写”。

当你编写接口类时，方法没有定义，因此我们必须始终将它们声明为 virtual，因为它们必须被重写。

所有类都有析构函数。这是一个在对象销毁时调用的特殊函数。在可能被继承的任何类中，析构函数都必须声明为 virtual，以便调用电被重写的析构函数。

这解释了我们为什么在接口类的定义中需要使用几次 virtual 关键字。

**危险！**

**虚析构函数：** 任何设计为可被继承的类都应该拥有虚析构函数。不幸的是，如果你忘记编写它，大多数编译器并不会报错。

## 12.5 抽象函数 =0

你可以通过写 `=0` 来说明某个函数没有实现。这仅仅意味着没有默认实现，子类必须提供自己的实现。这样的函数被称为抽象函数。显然，没有定义的函数必须声明为 `virtual`，以便它们可以被重写。

接口类是只有*抽象*函数的类。正如我们之前所示，你可以编写混合了已实现和未实现函数的类。抽象类是包含至少一个抽象函数的类。例如，`ContinuousTimeOptionBase` 是一个抽象类，因为它继承了抽象的 `payoff` 函数但没有实现它。

## 12.6 多层级

我们并不局限于父类和子类。我们可以构建复杂的类层次结构。

例如，一个类可以有祖父母类（grandparent）。事实上，我们已经见过这种情况，`PutOption` 的父类是 `ContinuousTimeOptionBase`，祖父母类是 `ContinuousTimeOption`。

你可以无限地继续下去。例如，我们可以（并且应该）引入一个新类 `PathIndependentOption`，其中包含看涨和看跌期权共有的代码，但不包括敲出期权和亚式期权使用的代码。

以下是 `PathIndependentOption` 的一个适当声明：

class PathIndependentOption :
           public ContinuousTimeOptionBase {
 public:
 /*  A virtual destructor */
 virtual ~PathIndependentOption() {}
 /*  Returns the payoff at maturity */
 virtual double payoff(double endStockPrice) const
 = 0;
 /*  Compute the payoff from a price path */
 double payoff(
  const std::vector<double>& stockPrices ) const {
   return payoff(stockPrices.back());
}
 /*  Is the option path dependent? */
}

