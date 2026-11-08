
至此，你已经实现了三个值类的所有重要功能。我添加了 `fmt_` 数据字段，因为 `Year` 会以宽度 4 输出，而 `Month` 和 `Day` 会以宽度 2 输出。你把所需的输出宽度作为参数添加到构造函数中。`print` 中调用 `vformat` 所需的 `fmt_` 格式是在构造函数中准备好的。

或者，你也可以为 `Value` 或 `Date` 编写一个格式化器，但那样会付出更多努力。

现在，这三个辅助类的声明非常短，正如你在清单 15.2 中看到的那样。

```cpp
// https://godbolt.org/z/eYYjIs4Te
class Year : public Value {            // derive from class Value
public:
    explicit Year(int v) : Value(v, 4) {} // initialize base class
};
class Month : public Value {
public:
    explicit Month(int v) : Value(v, 2) {}
};
struct Day : public Value {            // class-public corresponds to struct
    explicit Day(int v) : Value(v, 2) {}
};
```

**清单 15.2** 辅助类的重复代码现在消失了。

只剩下各个数据类型的构造函数；其他所有内容都由继承的类 `Value` 处理。

请特别注意以下几点：

- 在类 `Year : public Value` 中，我通过 `: public Value` 表示这个新类派生自 `Value` 类。
- 在构造函数的初始化列表中，我用两个参数调用 `Value` 的构造函数；例如，在 `Year(int v) : Value(v, 4)` 中，基类也必须被初始化，并且*必须*调用它的某个构造函数。具体调用哪一个，你在子类的冒号 `:` 后指定。如果省略这个显式调用，编译器会尝试使用不带参数的基类构造函数。在这里那会是 `Value{}`，但它并不存在。
- `class Value` 以一个 `protected` 部分开始。这意味着只有该类本身和派生类可以访问其内容，外部（`public`）不可以。构造函数位于这个部分。这允许子类在初始化时作为构造函数的一部分调用该构造函数，但我不能在 `main` 中定义 `Value val{10,3};`；那将是对构造函数“从外部”的访问。
- 基类 `Value(int v, unsigned w)` 构造函数不需要是 `explicit`，因为有两个参数时，它不再是自动类型转换的候选。它不会成为错误，但没必要。
- 提醒一下：用 `class` 声明一个新类型并立即开始一个 `public:` 部分，其效果与用 `struct` 定义相同。我曾用 `struct Day` 示范性地这样做过一次。你选择哪种是品味问题，但有一条指导原则是明智的。

清单的其余部分基本保持不变。`Date` 像往常一样使用 `Year`、`Month` 和 `Day`。对于 `Date` 来说，这一变化仍然不可见——这是封装的一个优势。

```cpp
// https://godbolt.org/z/9rY7qhK89
class Date {
    Year year_;
    Month month_{1};
    Day day_{1};
public:
    explicit Date(int y) : year_{y} {} // year-01-01
    Date(Year y, Month m, Day d) : year_{y}, month_{m}, day_{d} {}
    ostream& print(ostream& os) const;
};

ostream& Date::print(ostream& os) const {
    return os << year_ << "-" << month_ << "-" << day_;
}

ostream& operator<<(ostream& os, const Date& right) {
    return right.print(os);
}

int main() {
    Date d1 { Year{2024}, Month{11}, Day{19} };
    std::cout << d1 << "\n"; // Output: 2024-11-19
}
```

**清单 15.3** 这就是 “Date” 使用新类的方式。

## 15.5 派生类型扩展

在第 12 章清单 12.24 中，Easter 是一个自由函数。如果 Easter 是 Year 的一个方法，难道不是更合理吗？那样我们就可以直接向实例 `Year year{2018}` 询问 `year.easter()`，即那一年的复活节是哪一天。

```cpp
struct Component {
    Color getColor() const { return white; }
};
struct Window : public Component { };
struct MainWindow : public Window { };
struct Dialog : public Window { };
struct TextInput : public Component { };
struct Button : public Component {
    Color getColor() const { return gray; }
};
```

**清单 15.5** 所有组件都有白色；只有按钮会是灰色。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_398_0.png)

**图 15.5** 一个带有被重写方法的类层次结构。

如果你现在写 `Component c{}; c.getColor();`，你会得到白色，就像 `Dialog d{}; d.getColor();` 等一样。只有 `Button b{}; b.getColor();` 返回灰色。如果你无法从清单 15.5 推断出类层次结构，你可以在图 15.5 中找到可视化表示。

## 15.7 方法如何工作

在类层次结构中使用方法时，你需要注意几件事。看一下清单 15.6：注意 `print` 调用了哪些其他方法，并思考你会预期什么。我已将程序精简到本质部分，这就是它看起来有些理论化的原因。

2 在实践中，这样的组件层次结构不会以这种方式出现；我稍后会描述的 virtual 关键字仍然缺失。

```cpp
// https://godbolt.org/z/YTK8PfcMc
#include <iostream>
struct Base {
    int eight_ = 8;
    int value() const { return eight_; }
    void print(std::ostream& os) const { os << value() << "\n"; }
};
struct Print : public Base {
    int nine_ = 9;
    void print(std::ostream& os) const { os << value() << "\n"; }
};
struct Value : public Base {
    int ten_ = 10;
    int value() const { return ten_; }
};
struct Both : public Base {
    int eleven_ = 11;
    int value() const { return eleven_; }
    void print(std::ostream& os) const { os << value() << "\n"; }
};
int main() {
    Base ba{}; ba.print(std::cout);    // Base call
    Print pr{}; pr.print(std::cout);   // print overridden
    Value va{}; va.print(std::cout);   // print from Base
    Both bo{}; bo.print(std::cout);    // everything overridden
}
```

**清单 15.6** “print” 输出什么？“value” 方法出现得更频繁。

你认为 `main` 中不同的 print 行分别输出什么？

- **`Base ba{}; ba.print(cout);`—基类调用**
  在 `Base` 中，`print()` 和 `value()` 两个方法都是直接定义的。这里还没有涉及其他类。因此 `value()` 返回 `eight_`，输出 8。
- **`Print pr{}; pr.print(cout);`—print 被重写**
  在 `Print` 中，`print()` 方法被重写。对于 `pr`，会调用 `Print::print()` 方法。那里需要 `value()`。这个方法是从 `Base` 继承来的。而 `Base::value()` 返回 `eight_`——所以输出 8。
- **`Value va{}; va.print(cout);`—print 来自 Base**
  `va.print()` 必须回退到继承来的方法 `Base::print()`。现在那里需要 `value()` 方法。虽然存在 `Value::value()` 方法，但它在 `Base::print()` 中还不可知！在基类的方法中，只会使用基类的方法——这里是 `Base::value()`，它返回 `eight_` 并导致输出 8。
- **`Both bo{}; bo.print(cout);`—所有内容都被重写**
  这里又简单了：存在一个会被调用的 `Both::print()`。对 `value()` 的调用在其自己的方法中访问 `Both::value()`，并引用 `eleven_`。它输出 11。

你正确猜出第三种情况了吗？如果没有，不要难过。`Base::print()` 采用哪个 `value()` 方法是一个定义问题：两者都有可能。在 C++ 中，它的定义方式是：一个方法只能看到在通过继承、新定义或重写翻译该类时已经可用的方法。`Base::print()` 对可能的派生类还一无所知。

## 15.8 虚方法

在其他语言中，这有时不同：如果你在 Java 中编写前面的清单（针对该语言做明显修改），那么在 `Value va{}; va.print(cout);` 处你会看到 10，因为 Java 会在*运行时*检查实例可用的方法。

而且因为这也是一种合理的行为（否则它几乎不会被选为 Java 的默认行为），所以在 C++ 中也可以实现。关键在于*虚方法*。

如果你用 virtual 关键字标记一个方法，编译器会在*运行时*决定该方法的哪个版本有效。这样你就得到了 Java 的行为。

```cpp
// https://godbolt.org/z/wV5s3Kh6M
#include <iostream>

using std::ostream; using std::cout;
struct Base2 {
    int eight_ = 8;
    virtual int value() const        // virtual method
        { return eight_; }
    void print(ostream& os) const
        { os << value() << "\n"; }
};
struct Value2 : public Base2 {
    int ten_ = 10;
    virtual int value() const override // override
        { return ten_; }
};
int main() {
    Value2 v2{}; v2.print(cout);       // use
}
```

**清单 15.7** 用 “virtual” 标记的方法在运行时解析。
