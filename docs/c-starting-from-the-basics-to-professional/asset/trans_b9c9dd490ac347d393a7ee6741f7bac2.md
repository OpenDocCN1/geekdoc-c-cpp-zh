
```cpp
if (auto derived1 = dynamic_cast<Derived1*>(base); derived1 != nullptr)
    derived1->DoThis();
else if (auto derived2 = dynamic_cast<Derived2*>(base); derived2 != nullptr)
    derived2->do_this();
...
else if (auto derivedN = dynamic_cast<DerivedN*>(base); derivedN != nullptr)
    derivedN->doThat();
```

通常，这类代码应替换为基于多态的解决方案。在我们虚构的示例中，您可能应该在 Base 类中创建一个名为 DoThisOrThat() 的函数，并在任何需要不同实现的派生类中重写它。然后整个代码块就简化为：

```cpp
Base* base = ...;    // Start from a pointer-to-Base
base->DoThisOrThat();
```

这不仅短得多，而且如果将来某个时候又添加了一个从 Base 派生的 DerivedX 类，它甚至还能继续工作。这正是多态的强大之处。您的代码不需要知道现在或将来所有可能的派生类。它只需要知道基类的接口。任何使用动态转换来模仿这种机制的尝试都注定是劣质的。

虽然我们之前的示例显然是虚构的，但不幸的是，我们在真实代码中确实经常看到这种模式出现。因此，我们建议您对此非常谨慎！

我们有时会遇到 dynamic_cast 误用的一个相关症状，尽管不那么频繁，那就是对 this 指针进行动态转换。例如，这种不明智的代码可能看起来像这样：

```cpp
void Base::DoSomething()
{
    if (dynamic_cast<Derived*>(this))    // NEVER DO THIS!
    {
        /* do something else instead... */
        return;
    }
    ...
}
```

这里的正确解决方案是将 DoSomething() 函数设为虚函数，并在 Derived 中重写它。对 this 指针进行向下转换绝不是一个好主意，所以请不要这样做！基类的代码不应涉及派生类。这种模式的任何变体都应替换为多态的应用。

> **提示** 一般来说，利用多态可能涉及将一个函数拆分为多个函数，然后您可以重写其中的一些函数。如果您感兴趣，这又与前面提到的*模板方法设计模式*有关。您可以在网上或关于设计模式的书籍中找到更多信息。

## 转换引用

您可以将 `dynamic_cast<>` 运算符应用于函数中的引用参数，以沿类层次结构向下转换，从而产生另一个引用。在以下示例中，函数 `doThat()` 的参数是对基类 `Box` 对象的引用。在函数体中，您可以将该参数转换为对派生类型的引用：

```cpp
double doThat(Box& box)
{
  ...
  Carton& carton {dynamic_cast<Carton&>(box)};
  ...
}
```

这条语句从对 `Box` 的类型引用转换为对 `Carton` 的类型引用。当然，作为参数传递的对象可能不是 `Carton` 对象，如果是这种情况，转换就不会成功。不存在空引用这种东西，因此这种失败方式与指针转换失败不同。函数执行停止，并抛出类型为 `std::bad_cast` 的异常（该异常类定义在标准库的 `<typeinfo>` 模块中）。您还没有真正接触过异常，但您会在下一章中了解这意味着什么。

因此，盲目地对引用应用动态转换显然是有风险的，但有一个简单的替代方案。只需将引用转换为指针，并对指针应用转换即可。然后您可以再次检查结果指针是否为 `nullptr`：

```cpp
double doThat(Box& box)
{
  ...
  if (Carton* carton {dynamic_cast<Carton*>(&box)}; carton != nullptr)
  {
    ...
  }
  ...
}
```

## 调用虚函数的基类版本

您已经看到，通过指向派生类对象的指针或引用调用虚函数的派生类版本很容易——调用是动态进行的。但是，当您实际上想为派生类对象调用基类函数时，该怎么办？

如果在派生类中重写虚基类函数，您通常会发现在后者是前者的轻微变体。一个很好的例子是您在本章中一直使用的 `ToughPack` 类的 `volume()` 函数：

```cpp
// Function to calculate volume of a ToughPack allowing 15% for packing
double volume() const override { return 0.85 * m_length * m_width * m_height; }
```

显然，这个 return 语句中的 m_length * m_width * m_height 部分正是用于计算基类 Box 中 volume() 的公式。在这种情况下，您必须重新键入的代码量有限，但情况并非总是如此。因此，如果您能直接调用该函数的基类版本，那会好得多。

在我们的示例中，一个看似可行的首次尝试可能是这样：

```cpp
double volume() const override { return 0.85 * volume(); } // Infinite recursion!
```

然而，如果您这样写，volume() 重写函数只是在调用自身，然后又会再次调用自身，然后又会再次调用自身……您明白意思；这将导致我们在第 8 章中所谓的无限递归，从而导致程序崩溃（也就是说，如果您的编译器还没有直接拒绝这段代码的话）。解决方案是显式指示编译器调用该函数的基类版本（您可以在 Ex15_07A 中找到包含此修改的 ToughPack.cpp）：

```cpp
double volume() const override { return 0.85 * Box::volume(); }
```

像这样在函数重写中调用基类版本很常见。不过，在某些罕见情况下，您可能还想在其他地方做类似的事情。Box 类提供了一个机会来了解为什么可能需要这样的调用。计算 Carton 或 ToughPack 对象中的体积损失可能很有用；一种方法是计算 volume() 函数的基类版本和派生类版本返回的体积之差。您可以通过用类名限定来强制静态调用基类的虚函数。假设您有一个这样定义的指针 box：

```cpp
Carton carton {40.0, 30.0, 20.0};
Box* box {&carton};
```

您可以使用以下语句计算 Carton 对象的总体积损失：

```cpp
double difference {box->Box::volume() - box->volume()};
```

表达式 box->Box::volume() 调用 volume() 函数的基类版本。类名连同作用域解析运算符一起标识了特定的 volume() 函数，因此这将是编译时解析的静态调用。

您不能使用类名限定符来强制在通过指向基类的指针进行的调用中选择特定的派生类函数。表达式 box->Carton::volume() 将无法编译，因为 Carton::volume() 不是 Box 类的成员。通过指针调用函数要么是对指针所属类类型的成员函数的静态调用，要么是对虚函数的动态调用。

通过派生类的对象调用虚函数的基类版本可以类似地完成。您可以使用以下语句计算 Carton 对象的体积损失：

```cpp
double difference {carton.Box::volume() - carton.volume()};
```

## 从构造函数或析构函数中调用虚函数

Ex15_08 说明了当您从构造函数和析构函数内部调用虚函数时会发生什么。一如既往，我们从一个 Box 类开始，在其相关成员中包含必要的调试语句：

```cpp
// Box.cpp
export module boxes;
import <iostream>;

export class Box
{
public:
  Box(double length, double width, double height)
    : m_length {length}, m_width {width}, m_height {height}
  {
    std::cout << "Box constructor called for a Box of volume " << volume() << std::endl;
  }
  virtual ~Box()
  {
    std::cout << "Box destructor called for a Box of volume " << volume() << std::endl;
  }

  // Function to calculate volume of a Box
  virtual double volume() const { return m_length * m_width * m_height; }

  void showVolume() const
  {
    std::cout << "The volume from inside Box::showVolume() is "
              << volume() << std::endl;
  }

private:
  double m_length, m_width, m_height;
};
```

我们还需要一个派生类，一个重写 `Box::volume()` 的派生类；

```cpp
export module boxes::tough_pack;
import <iostream>;
import :box;

export class ToughPack : public Box
{
public:
  ToughPack(double length, double width, double height)
    : Box{length, width, height}
  {
    std::cout << "ToughPack constructor called for a Box of volume "
              << volume() << std::endl;
  }
  virtual ~ToughPack()
  {
    std::cout << "ToughPack destructor called for a Box of volume "
              << volume() << std::endl;
  }

  // Function to calculate volume of a ToughPack allowing 15% for packing
  double volume() const override { return 0.85 * Box::volume(); }
};
```
