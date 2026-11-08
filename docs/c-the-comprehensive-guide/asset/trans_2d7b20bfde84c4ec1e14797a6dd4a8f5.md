
## 15.1 关系

对象之间的关系在面向对象编程（OOP）中起着核心作用，因为它们显著影响软件的结构和功能，并支持对复杂系统进行建模和组织。在此语境下，has-a 关系和 is-a 关系尤为重要，因为它们定义了对象如何连接以及如何按层次相互关联。

### 15.1.1 Has-a 组合

当你在第 12 章学习使用 `struct` 和 `class` 时，我最初将数据字段捆绑进*聚合体*。

```cpp
class Car {
    Windscreen windscreen_;
    std::vector<Wheel> wheels_;
    // ...
};
```

这辆 Car *拥有（has-a）* windscreen_ 以及 wheels_——每个都对应其类型。在这种情况下，这是一种 has-a 关系，Car 甚至由这些对象组成或构成。这是一种*组合*。这意味着该对象通常*拥有*其组件——在 C++ 中，这意味着它负责这些组件的构造和析构。组件的生命周期受对象生命周期的限制。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_390_0.png)

图 15.1 Has-a 关系：UML 表示法中的组合（左）和聚合（右）。

### 15.1.2 Has-a 聚合

当你把汽车说成拥有一个车棚（car port）或拥有一个持有者（holder）时，情况就不同了。这是一种*聚合*：

```cpp
class Car {
    CarPort& carPort_;
    Person& holder_;
    // ...
};
```

被包含的事物只与该对象处于一种*关系*中，但并不*属于*它。因此，该对象通常不负责它们的创建或销毁。这些元素的生命周期独立于该对象的生命周期。

汽车、挡风玻璃和车棚这个说明性示例似乎清楚地分别描述了组合和聚合。在设计具体软件时，事情往往没那么简单。如果你要为汽车制造商的装配线编程，那么你在数据库中把挡风玻璃实例与汽车关联的方式，会不同于你为汽车租赁公司的车队创建目录时的方式。

在图 15.2 中，你可以看到这些关系的一种可能表示方式。组合被归入一个框中。箭头连接其他关系，聚合用实线和实心箭头表示。箭头还可以明确指定关系的类型。在一个框内，列出了属性（正常字体）和行为/方法（*斜体字体*）。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_391_0.png)

图 15.2 表示两种 has-a 关系的另一种更非正式的表示方式。

表示对象之间关系的方式有几十种。这里我只非常简要地概述了其中两种。

### 15.1.3 Is-a 继承

通过继承，你现在映射的是一种 *is-a（是）* 关系。例如：一辆大众巴士（VW bus）*是一辆（is-a）* 汽车。这意味着以下规则适用：

- 一辆大众巴士具有汽车所具有的全部属性。
- 每个符合大众巴士描述（或规范）的对象，也符合汽车的描述。
- 大众巴士的描述（或规范）*更具体*，而汽车的描述（或规范）*更弱*。
- 如果你期望的是一辆汽车，那么交付给你一辆大众巴士也是正确的。

对于大众巴士和汽车，显然可以通过继承来映射它们的关系。但有时把它们放在一起时，事情并不那么清晰。此时这些规则可能有助于检查是否存在 *is-a（是）* 关系。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_392_0.png)

图 15.3 这个维恩图表明所有大众巴士都是汽车，但并非所有汽车都是大众巴士。

### 15.1.4 Instance-of 与 Is-a 关系

注意，对于 car herbie 的 is-a 关系；并不意味着“herbie is-a car”。这被称为“是一个实例（is an instance of）”，或者在 C++ 中称为“herbie is of type car”。几乎不可避免的是，这些术语并不总是被正确使用。例如，“7 is an integer”或“7 is an int”在此语境下并不精确。但总是说“7 is an element of integers”或“7 is of type int”听起来很怪。

当你谈论类层次结构时，应当注意这一区别。

> **不是：Is-an-Instance-of**
> 
> *记住：* 在继承中，*is-a（是）* 并不意味着某个类的实例，而是指具有超类全部属性的子类。

## 15.2 C++ 中的继承

在 C++ 中，你按如下方式表示继承：

```cpp
class Car {                 // Base or superclass
public:
    Windscreen windscreen_;
    std::vector<Wheel> wheels_;
    // ...
};
class VwBus : public Car {   // VwBulli is a subclass
public:
    Flowers flowers_;
    // ...
};
```

因此，你写出*基*类的名称，用冒号 `:` 分隔，并在当前类名之后写 `public`：

```cpp
class Subclass : public Baseclass { ...
```

现在你可以愉快地创建新的 `VwBus` 实例。而且每个实例都自动拥有 `windscreen_` 和 `wheels_`，即使你并未在 `VwBus` 类中显式提及它们：

```cpp
VwBus vw{};
cout << vw.windscreen_;
cout << vw.flowers_;
```

如果你创建一个纯 `Car` 汽车，那么 `car.windscreen_` 将是有效访问，但在 `Car` 类中，`car.flowers_` 并不存在。

因此，如果你有一个子类实例，你既可以访问它自己的数据字段和方法，也可以访问从超类继承而来的数据字段和方法。例如，如果你实现图 15.4 中的 *露营（camping）* 方法，那么你可以在其中同时使用 `Windscreen` 和 `Flowers`。

反过来则不成立（从逻辑上讲）：如果你当前正在实现 `Car` 中的 `drive`，你可以访问 windscreen 和四个车轮，但 Flowers 对你来说并不存在。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_393_0.png)

**图 15.4** 超类的所有数据字段和方法也都存在于子类中。

## 15.3 Has-a 与 Is-a

如前所述，你可以从逻辑和概念上设计继承层次结构。具体怎么做取决于特定应用。有时让 `VwBus` 继承自 `Car` 是合理的，而在另一个应用中，`VW bus` 是一个独立类，并将 `Car` 作为属性。

如果你不确定是否要构建继承层次结构，在有疑问时，优先选择 has-a 关系而不是 is-a 关系。在 C++ 中，继承只是实现设计的一种技术。原则上，你可以通过让 `Car` 成为 `VwBus` 的数据元素，并转发 `drive` 和 `refuel` 方法，来实现同样的效果。

诚然，在这一点上这是个相当强的论断。当你创建一些类和层次结构时，你可能会想起这个提示，并知道不必把所有东西都塞进继承层次结构中。有时一个封装良好的数据字段就足够了。<sup>1</sup>

## 15.4 寻找共性

话虽如此，我会回到要点：在你可能放弃看似合理的继承层次结构的情况下，另一方面，你也可以使用继承来整合不相关的数据并避免代码重复。正如我在开头所说，我把这称为继承层次结构的技术原因。

例如，查看第 12 章中的代码清单 12.24 和代码清单 12.27。如果你像 Year 那样完整地写出数据类型 Month 和 Day，那么你会得到大量在三个类中看起来完全相同的代码。代码重复是不好的——你可以构建一个小型继承层次结构来避免它。

首先，在代码清单 15.1 中，你定义三个辅助类的共同祖先 Value。

```cpp
// https://godbolt.org/z/hHoG46z5a
#include <iostream>    // ostream
#include <format>      // format, vformat, make_format_args
using std::ostream;
class Value {
protected: // not public, only for own and derived use
    int value_;
    const std::string fmt_;   // e.g. "{02}" or "{04}"
    Value(int v, unsigned w)  // constructor with two arguments
        : value_{v}, fmt_{std::format("{{:{}}}", w)} {}
public:
    ostream& print(ostream& os) const;
};
ostream& operator<<(ostream& os, const Value& right) {
    return right.print(os);
}
ostream& Value::print(ostream& os) const {
    return os << std::vformat(fmt_, std::make_format_args(value_));
}
```

**代码清单 15.1** 我们的 “Year”、“Month” 和 “Day” 辅助类的共同祖先。

<sup>1</sup> 你可能会失去动态类型多态，但使用模板的静态类型多态是可能的。
