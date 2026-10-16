

```
class CW_ival_slider
: public Ival_slider, protected CWslider { /* ... */ };
```

或图形表示为：

![](img/a47cb5c880e9c78ea4f904f538cf91c8_618_0.png)

当我们的抽象与用于实现的系统提供的抽象并不太不同时——这种情况并不少见——这种改进变得显著。在这种情况下，编程被简化为在相似概念之间进行映射。此时，仅在很少情况下才会从通用基类（如 **BBwidget**）派生。

完整的层次结构将由我们原始的应用导向概念层次结构组成，以接口形式表示为派生类：

```
class Ival_box { /* ... */ };
class Ival_slider
: public Ival_box { /* ... */ };
class Ival_dial
: public Ival_box { /* ... */ };
class Flashing_ival_slider
: public Ival_slider { /* ... */ };
class Popup_ival_slider
: public Ival_slider { /* ... */ };
```

随后是该层次结构针对各种图形用户界面系统的实现，以派生类的形式表示：

```
class BB_ival_slider
: public Ival_slider, protected BBslider { /* ... */ };
class BB_flashing_ival_slider
: public Flashing_ival_slider, protected BBwidget_with_bells_and_whistles { /* ... */ };
class BB_popup_ival_slider
: public Popup_ival_slider, protected BBslider { /* ... */ };
class CW_ival_slider
: public Ival_slider, protected CWslider { /* ... */ };
// ...
```

使用明显的缩写，该层次结构可以图形化地表示如下：

![](img/a47cb5c880e9c78ea4f904f538cf91c8_618_1.png)

原始的 **Ival_box** 类层次结构保持不变，其周围环绕着实现类。

## 21.2.3.1 评述

抽象类设计灵活且几乎与依赖于定义用户界面系统的公共基的等效设计一样简单易用。在后者设计中，窗口类是树的根。在前者中，原始的应用类层次结构保持不变，作为提供其实现的类的根。从应用的角度来看，这两种设计在强意义上是等价的，即几乎所有代码在两种情况下都能不变地工作且方式相同。在任何一种情况下，你都可以查看 Ival_box 系列类，而大多数时候无需关心与窗口相关的实现细节。例如，如果我们从一个类层次结构切换到另一个，如果我们切换类层次结构，就无需重写 §21.2.1 中的 interact()。

在任何一种情况下，当用户界面系统的公共接口发生变化时，每个 Ival_box 类的实现都必须重写。然而，在抽象类设计中，几乎所有用户代码都受到实现层次结构变化的保护，并且在这种变化后无需重新编译。这在实现层次结构的供应商发布一个“几乎兼容”的新版本时尤其重要。此外，抽象类层次结构的用户比经典层次结构的用户更不容易被锁定在专有实现中。Ival_box 抽象类应用层次结构的用户无法意外使用来自实现的设施，因为只有在 Ival_box 层次结构中明确指定的设施才可访问；没有任何内容从实现特定的基类隐式继承。

这一思路的逻辑结论是一个向用户表示为抽象类层次结构并由经典层次结构实现的系统。换句话说：

- 使用抽象类来支持接口继承 (§3.2.3, §20.1)。
- 使用具有虚函数实现的基类来支持实现继承 (§3.2.3, §20.1)。

# 第 21.2.4 节 局部化对象创建 623

## 21.2.4 局部化对象创建

大部分应用都可以使用 Ival_box 接口编写。此外，如果派生接口演进以提供比纯 Ival_box 更多的设施，那么大部分应用都可以使用 Ival_box、Ival_slider 等接口编写。然而，对象的创建必须使用实现特定的名称，例如 CW_ival_dial 和 BB_flashing_ival_slider。我们希望将此类特定名称出现的次数降到最低，而对象创建除非系统化进行，否则很难局部化。

通常的解决方案是引入间接层。这可以通过多种方式实现。一种简单的方法是引入一个抽象类来表示创建操作集合：

```
class Ival_maker {
public:
virtual Ival_dial* dial(int, int) =0; // makedial
virtual Popup_ival_slider* popup_slider(int, int) =0; // makepopup slider
// ...
};
```

对于 Ival_box 系列类族中用户应了解的每个接口，类 Ival_maker 都提供一个创建对象的函数。此类有时被称为工厂，其函数有时（有些误导性地）被称为虚构造函数 (§20.3.6)。

我们现在用派生自 Ival_maker 的类来表示每个用户界面系统：

```
class BB_maker : public Ival_maker { // makeBBversions
public:
Ival_dial* dial(int, int) override;
Popup_ival_slider* popup_slider(int, int) override;
// ...
};
```

```
class LS_maker : public Ival_maker { // makeLSversions
public:
Ival_dial* dial(int, int) override;
Popup_ival_slider* popup_slider(int, int) override;
// ...
};
```

每个函数都创建所需接口和实现类型的对象。例如：

```
Ival_dial* BB_maker::dial(int a, int b)
{
return new BB_ival_dial(a,b);
}
```

```
Ival_dial* LS_maker::dial(int a, int b)
{
return new LS_ival_dial(a,b);
}
```

给定一个 Ival_maker，用户现在可以在不知道使用哪个用户界面系统的情况下创建对象。例如：

```
void user(Ival_maker& im) {
unique_ptr<Ival_box> pb {im.dial(0,99)}; // create appropriate dial // ...
}
```

```
BB_maker BB_impl; LS_maker LS_impl;
void driver() {
// forBBusers // forLSusers
user(BB_impl); // use BB
user(LS_impl); // use LS
}
```

向此类“虚构造函数”传递参数有点棘手。特别是，我们不能用不同参数覆盖表示接口的基类函数在不同派生类中。这意味着设计工厂类接口需要相当多的前瞻性。

## 21.3 多重继承

如 §20.1 中所述，继承旨在提供两种好处之一：

• *共享接口*：导致使用类的代码重复减少并使此类代码更统一。这通常称为 *运行时多态* 或 *接口继承*。
• *共享实现*：导致代码更少且实现代码更统一。这通常称为 *实现继承*。

一个类可以结合这两种风格的方面。
在此，我们探讨多重基类的更一般用途，并检查与组合和访问来自多个基类的特性相关的更多技术问题。

### 21.3.1 多个接口

抽象类（例如，[Ival_box; §21.2.2) 是表示接口的明显方式。
对于没有可变状态的抽象类，类层次结构中单次和多次使用基类之间实际上几乎没有区别。潜在歧义的解析在 §21.3.3、§21.3.4 和 §21.3.5 中讨论。事实上，任何没有可变状态的类都可以在多重继承格中作为接口使用，而不会产生显著的复杂性和开销。关键观察是，没有可变状态的类如果需要可以被复制，如果希望也可以被共享。

在面向对象设计中，使用多个抽象类作为接口几乎是普遍的（在任何具有接口概念的语言中）。

### 21.3.2 多个实现类

考虑一个模拟地球轨道上天体的仿真，其中轨道物体表示为类 *Satellite* 的对象。*Satellite* 对象将包含轨道、大小、形状、反照率、密度参数等，并提供轨道计算、修改属性等操作。卫星的例子将是岩石、旧航天器残骸、通信卫星和国际空间站。这些类型的卫星将是派生自 *Satellite* 的类的对象。此类派生类将添加数据成员和函数，并重写 *Satellite* 的某些虚函数以适当地调整其含义。

现在假设我想以图形方式显示这些仿真的结果，并且我有一个可用的图形系统，该系统使用（并不少见）的策略，即从保存图形信息的公共基类派生要显示的对象。此图形类将提供屏幕放置、缩放等操作。为了通用性、简洁性和隐藏实际图形系统的细节，我将把提供图形（或实际上非图形）输出的类称为 *Display*。

我们现在可以定义一个模拟通信卫星的类，类 *Comm_sat*：
```
class Comm_sat : public Satellite, public Display {
public:
// ...
};
```

