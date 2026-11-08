

```cpp
y[i] {
}
```

这种表述要求为每个将被混入的类做更多工作，因此像 label 和 color 这样的类将需要成为类模板。然而，被混入的类现在可以针对它们被混入的派生类的特定实例来调整其行为。例如，我们可以将前面讨论的对象计数器模板混入根类：每个类创建的对象数量可以由该混入连同其他应用特定的混入一起计数。

### 21.3.2 参数化虚性

混入还允许我们间接地参数化派生类的其他属性，例如成员函数的虚性。一个简单的例子展示了这种相当令人惊讶的技术：

inherit/virtual.cpp

```cpp
#include <iostream>

class NotVirtual {
};

class Virtual {
public:
    virtual void foo() {
    }
};

template<typename... Mixins>
class Base :
    public Mixins... {
public:
    // the virtuality of foo() depends on its declaration
    // (if any) in the base classes Mixins.
    void foo() {
        std::cout << "Base::foo()\n";
    }
};

template<typename... Mixins>
class Derived : public Base<Mixins...> {
public:
    void foo() {
        std::cout << "Derived::foo()\n";
    }
};

int main()
{
    Base<NotVirtual> *p1 = new Derived<NotVirtual>();
    p1->foo(); // calls Base::foo()

    Base<Virtual> *p2 = new Derived<Virtual>();
    p2->foo(); // calls Derived::foo()
}
```

这种技术可以提供一个工具，用于设计既可用来实例化具体类、又可通过继承进行扩展的类模板。然而，仅仅对某些成员函数特化虚性，通常不足以获得一个能作为更专门功能良好基类的类。这类开发方法需要更根本的设计决策。因此，通常更实际的做法是设计两个不同的工具（一个类或类模板层次结构），而不是试图把所有东西都塞进一个带许多不同模板类型参数的模板层次结构中。不过，这些参数中的许多往往具有合理的默认值。定义这样一个类模板的一种自然方式可能如下所示：

```cpp
template<typename Policy1 = DefaultPolicy1,
         typename Policy2 = DefaultPolicy2,
         typename Policy3 = DefaultPolicy3,
         typename Policy4 = DefaultPolicy4>
class ThreadLocker
{
};
```

据推测，这样的模板通常可以使用默认模板实参值，语法为`ThreadLocker<>`。然而，如果必须指定一个非默认实参，则也必须指定所有前面的实参（即使它们可能具有默认值）。

显然，像现在这样只能使用 `ThreadLocker<DefaultPolicy1, DefaultPolicy2, Custom>`，而不能使用类似 `ThreadLocker<Policy3 = Custom>` 的构造，这是不理想的。下面我们开发一种技术，几乎正好实现这一点。

```cpp
template<typename PolicySet1 = DefaultPolicySet1,
         typename PolicySet2 = DefaultPolicySet2,
         typename PolicySet3 = DefaultPolicySet3,
         typename PolicySet4 = DefaultPolicySet4>
class PolicySelector
{
    PolicySet1 policySet1;
    PolicySet2 policySet2;
    PolicySet3 policySet3;
    PolicySet4 policySet4;
};
```

我们的技术包括将默认类型值放在一个基类中，并通过派生来覆盖其中一些值。我们不是直接指定类型实参，而是通过成员函数来提供它们。例如，我们可以写 `Great<Policy1>`，因为每个模板实参可以描述策略之一，而默认值可以不同。换句话说，在更高层次上，每个模板参数都是等价的：

```cpp
template<typename Policy1, typename Policy2,
         typename Policy3, typename Policy4>
class PolicySelector : public PolicySelectorBase<Policy1,
                                                 Policy2,
                                                 Policy3,
                                                 Policy4>
{
public:
    PolicySelector() {}
};
```

剩下的挑战是编写策略选择器模板。它必须将不同的模板实参合并为一个单一类型，该类型用所指定的任何非默认类型来覆盖默认策略类型及其成员。这种合并可以通过继承来实现：

```cpp
// PolicySelector<A,B,C,D> creates A,B,C,D as base
// classes
// Discriminator to allow having more than one base class
template<typename Base>
class Discriminator : public Base
{
};

template<typename Select1, typename Select2,
         typename Select3, typename Select4>
class PolicySelector : public Discriminator<Select1>,
                       public Discriminator<Select2>,
                       public Discriminator<Select3>,
                       public Discriminator<Select4>
{
};
```

注意中间`Discriminator`模板的使用。需要它来允许各种`Selector`类型相同。不能有多个相同类型的直接基类。另一方面，间接基类可以具有与其他基类相同的类型。

作为一个提议的策略，我们将默认值收集到一个基类中。

```cpp
// Name default policies as P1, P2, P3, P4
class DefaultPolicies
{
public:
    using P1 = DefaultPolicy1;
    using P2 = DefaultPolicy2;
    using P3 = DefaultPolicy3;
    using P4 = DefaultPolicy4;
};
```

然而，如果我们最终多次继承这个基类，就必须小心避免歧义。因此，我们确保以虚继承方式继承该基类：

```cpp
template<typename Policy>
class Policy1 : virtual public DefaultPolicies {
public:
    using P1 = Policy; // overriding type alias
};

template<typename Policy>
class Policy2 : virtual public DefaultPolicies {
public:
    using P2 = Policy; // overriding type alias
};

template<typename Policy>
class Policy3 : virtual public DefaultPolicies {
public:
    using P3 = Policy; // overriding type alias
};

template<typename Policy>
class Policy4 : virtual public DefaultPolicies {
public:
    using P4 = Policy; // overriding type alias
};
```

一切就绪后，我们期望的目标就实现了。现在让我们通过示例来看看我们得到了什么。让我们实例化一个 BreadSlices 类：

```cpp
BreadSlices<Policy3, IceCreamPolicy> bc;
```

对于这个类，输出定义为

```cpp
PolicySelector<Policy3, IceCreamPolicy>,
    DefaultPolicy<...>,
    DefaultPolicy<...>,
    DefaultPolicy<...>
```

借助 Discriminator<> 类模板，这会形成一个层次结构，其中所有子类型都派生自这些基类（见图 21-4）。重要的一点是，这些基类都具有相同的虚基类 DefaultPolicies，它定义了 P1、P2、P3 和 P4 的默认类型。然而，P3 在其中一个派生类中——即 Policy3 中——被重新定义，并且根据支配规则，这个定义隐藏了基类中的定义。因此，这不是歧义。

*图 21-4. BreadSlices<Policies> 的类型层次解析*

在模板 BreadSlices 内部，可以使用限定名（如`Policies::P3`）来引用这四个策略。例如

```cpp
template<...>
class BreadSlices {

public:
    void print() {
        Policies::P1::doPrint();
    }
};
```

在 inherit/named1.cpp 中可以找到完整的示例。

我们针对四个模板参数开发了这项技术，但它显然可以扩展到任意合理数量的此类参数。请注意，我们实际上从不实例化包含虚基的辅助类的对象。事实上，它们是虚基这一点并不是性能或内存消耗问题。

## 21.5 后记

Bill Gibbons 是将 EBCO 引入 C++ 编程语言的主要推动者。Nathan Myers 使之流行，并提出了一个类似于我们的 BaseMemberPair 的模板，以更好地利用它。Boost 库包含一个相当复杂的模板，称为 compressed_pair，它解决了本章中 C++ 模板的一些问题。

本章中 EBCO 的简单方法基于这样一种思想：如果一个基类没有数据成员也没有虚函数，那么它的实现可以被优化掉。然而，C++ 标准并不要求这种优化，而且有些实现并不执行它。

C++ 和许多形式的参数化继承并不符合 EBCO。EBCO 在 Boost 库中特别有用，在那里它被用来实现函数对象和其他泛型编程技术。

混入的概念至少自 1986 年（MoonFlavors）起就存在于面向对象编程中，作为一种将小块行为引入类层次结构的方式。

