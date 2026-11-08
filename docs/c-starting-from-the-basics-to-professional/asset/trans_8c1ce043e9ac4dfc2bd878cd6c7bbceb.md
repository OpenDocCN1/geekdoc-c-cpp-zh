
包含至少一个纯虚函数的类称为抽象类。Shape 类包含两个纯虚函数——area() 和 scale()——因此它毫无疑问是一个抽象类。我们再进一步看看这究竟意味着什么。

## 抽象类

尽管 Shape 类有一个成员变量、一个构造函数，甚至还有一个带实现的成员函数，但它仍然是对对象的不完整描述，因为 area() 和 scale() 函数没有被定义。因此，不允许创建 Shape 类的实例；这个类存在的纯粹目的就是供其他类从它派生。由于不能创建抽象类的对象，因此不能按值将它传递给函数；类型为 Shape 的参数将无法通过编译。同样，也不能从函数中按值返回 Shape。但是，指向抽象类的指针或引用可以用作参数类型或返回类型，因此像 Shape* 和 Shape& 这样的类型在这些场合没有问题。对于获得派生类对象的多态行为而言，必须如此，这一点至关重要。

这就引出了一个问题：“如果不能创建抽象类的实例，那么抽象类为什么还要包含构造函数？”答案是，抽象类的构造函数用于初始化其成员变量。抽象类的构造函数将由派生类构造函数调用，可能是隐式调用，也可能从构造函数初始化列表中调用。如果你试图从其他任何地方调用抽象类的构造函数，编译器会给出错误消息。

由于抽象类的构造函数通常不能使用，最好将其声明为类的 protected 成员，就像我们对 Shape 类所做的那样。这样既允许在派生类构造函数的初始化列表中调用它，又能阻止从其他任何地方访问它。注意，抽象类的构造函数不得调用纯虚函数；这样做的效果是未定义的。

任何从 Shape 类派生的类都必须定义 area() 函数和 scale() 函数。如果不这样做，它本身也是抽象类。更具体地说，如果抽象基类的任何纯虚函数未在派生类中定义，那么该纯虚函数将照原样被继承，派生类也将是抽象类。

为了说明这一点，可以定义一个名为 Circle 的新类，它以 Shape 类为基类。假设你从 shape 模块导出 Shape 类，那么可以创建一个新的 shape.circle 模块，按如下方式导出 Circle：

```cpp
export module shape.circle;
import shape;        // For the Shape base class
import <numbers>;    // For the constant π

// Class defining a circle
export class Circle : public Shape
{
public:
  Circle(const Point& center, double radius) : Shape{center}, m_radius{radius} {}

  double area() const override {
    return m_radius * m_radius * std::numbers::pi;
  }

  void scale(double factor) override { m_radius *= factor; }

private:
  double m_radius;   // Radius of a circle
};
```

area() 和 scale() 函数已定义，因此这个类不是抽象类。如果其中任一函数未定义，那么 Circle 类就会是抽象类。该类包含一个构造函数，它通过调用基类构造函数来初始化基类子对象。

当然，抽象类可以包含它确实定义的虚函数以及非虚函数。前者的一个例子是 Shape 中的 move() 函数。它也可以包含任意数量的纯虚函数。

> **注意** 对于本章中的所有 boxes 模块，我们将每个类定义在各自的模块分区中。对于 shapes，我们决定再次改变做法，将每个类重新定义在各自独立的模块中。也就是说，标识符 `shape.circle` 是模块的标识符，而不是分区的标识符。模块分区始终具有 `module:partition` 形式的标识符（注意冒号！）。区别在于，`shape.circle` 模块可以从任何源文件导入，而分区只能从属于同一模块的源文件导入。因此，作为这些模块的使用者，你总是会一次性获得所有 `Box` 类型——如果你愿意，可以把它看作一揽子交易——而不同的 `Shape` 类型则必须分别导入。为了兼得两者之长，你可以定义一个额外的伞形模块，让你可以轻松地一次性导入多个相关模块。例如：

```cpp
export module shapes;
export import shape.circle;
export import shape.rectangle;
// ... same for any other module exporting a shape class
```

如何将类型（和函数）打包到模块中完全由你决定。如果一组类型总是一起使用，你可能希望将它们归入同一个模块。但如果这些类型可以独立使用，或者通常独立使用，那么创建单独的模块可能更有意义。

### 抽象 Box 类

让我们看一个使用抽象类的工作示例。为此，我们将定义 Box 类的一个新版本，其中 volume() 函数被声明为纯虚函数。作为多态基类，它当然也需要一个虚析构函数：

```cpp
export module boxes:box;
export class Box
{
public:
    Box(double l, double w, double h) : m_length {l}, m_width {w}, m_height {h} {}
    virtual ~Box() = default;       // Virtual destructor
    virtual double volume() const = 0;  // Function to calculate the volume

protected:  // Should be private in production-quality code (add getters to access)
    double m_length, m_width, m_height;
};
```

由于 Box 现在是抽象类，你不能再创建这种类型的对象。即使构造函数是 public，从派生类构造函数以外的任何地方调用它都会导致编译器错误。

> **提示** 由于 Box 构造函数只打算供派生类中的构造函数使用，我们本也可以将它声明在 Box 类的 protected 区段中。然而，这样做虽然明确了意图，却也实际上阻止了构造函数继承。请记住，当继承构造函数时，你总是连同基类的访问说明符一起继承。无论你把继承声明放在派生类的哪个区段中，都是如此。因此，作为一条规则，我们更愿意将抽象基类的构造函数声明在 public 区段中。

本例中的 Carton 和 ToughPack 类与 Ex15_06 中的相同。它们都定义了 volume() 函数，因此不是抽象类，我们可以使用这些类的对象来表明虚函数 volume() 仍然像以前一样工作：

```cpp
// Ex15_10.cpp
// Using an abstract class
import <iostream>;
import boxes;

int main()
{
  // Box box{20.0, 30.0, 40.0};              // Uncomment for compiler error

  ToughPack hardcase {20.0, 30.0, 40.0};    // A derived box - same size
  Carton carton {20.0, 30.0, 40.0, "plastic"}; // A different derived box

  Box* base {&hardcase};                    // Base pointer - derived address
  std::cout << "hardcase volume is " << base->volume() << std::endl;

  base = &carton;                           // New derived address
  std::cout << "carton volume is " << base->volume() << std::endl;
}
```

这会产生以下输出：

```text
hardcase volume is 20400
carton volume is 22722.4
```

在 Box 类中将 volume() 声明为纯虚函数，可以确保 Carton 和 ToughPack 类的 volume() 函数成员也是虚函数。因此，你可以通过指向基类的指针调用它们，而这些调用将动态解析。ToughPack 和 Carton 对象的输出表明一切都在按预期工作。

> **注意** 现在你不能再像我们在 Ex15_09 中所做的那样实现 ToughPack 类的 `volume()` 成员：
>
> ```cpp
> double volume() const override { return 0.85 * Box::volume(); }
> ```
>
> `Box::volume()` 现在是纯虚函数，而且永远不能使用静态绑定调用纯虚函数（它没有函数体！）。由于不再提供基类实现，你在这里又必须写出 `m_length * m_width * m_height`。

### 作为接口的抽象类

有时，抽象类的出现仅仅是因为某个函数在该类的上下文中没有合理的定义，而只有在派生类中才有有意义的解释。然而，还有另一种使用抽象类的方式。一个只包含纯虚函数——没有成员变量或其他函数——的抽象类，可以用来定义面向对象术语中通常所说的接口。它通常表示一组相关函数的声明，这些函数支持某种特定能力——例如，一组用于通过调制解调器进行通信的函数。虽然 Java 和 C# 等其他编程语言为此提供了特定的类式语言构造，但在 C++ 中，人们使用仅由纯虚函数组成的抽象类来定义接口。正如我们已经讨论过的，从这种抽象基类派生的类必须为每个虚函数定义实现，但每个虚函数的具体实现方式由实现派生类的人指定。抽象类固定了接口，而派生类中的实现是灵活的。

由于上一节中的抽象 Shape 和 Box 类有成员变量，它们并不是真正的接口类。接口的一个例子是下面这个 Vessel 类，它定义在 Vessel.cpp 中。它所做的只是规定任何 Vessel 都有一个体积，该体积可以通过其（纯虚）volume() 成员函数获得：

```cpp
// Vessel.cpp - Abstract class defining a vessel
export module vessel;

export class Vessel
{
public:
    virtual ~Vessel() = default;       // As always: a virtual destructor!
    virtual double volume() const = 0;
};
```

可以有任意数量的类实现 Vessel 接口。所有类都会以自己的方式实现该接口的 `volume()` 函数。我们的第一个 Vessel 类自然将是我们钟爱的 Box 类：

```cpp
export module boxes:box;
import vessel;

export class Box : public Vessel
{
public:
    Box(double l, double w, double h) : m_length {l}, m_width {w}, m_height {h} {}

    double volume() const override { return m_length * m_width * m_height; }
};
```
