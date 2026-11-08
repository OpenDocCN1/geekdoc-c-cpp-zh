
```
// Function to calculate the volume of a Box object
virtual double volume() const { return m_length * m_width * m_height; }

// ...
};
```

> **注意** 如果成员函数定义在类定义之外，你*绝不能*在函数定义中添加 **virtual** 关键字；这样做是错误的。你只能在类定义内部的声明或定义中添加 **virtual**。

为了更有趣，让我们在一个名为 Carton 的新类中以稍微不同的方式实现 volume() 函数。以下是类定义：

```
// Carton.cppm
export module boxes:carton;

import :box;          // For the Box base class
import <algorithm>;   // For std::max()
import <string>;
import <string_view>;

export class Carton : public Box
{
public:
  // Constructor explicitly calling the base constructor
  Carton(double l, double w, double h, std::string_view mat = "cardboard")
    : Box(l, w, h), m_material(mat)
  {}

  // Function to calculate the volume of a Carton object
  double volume() const
  {
    const double volume {(m_length - 0.5) * (m_width - 0.5) * (m_height - 0.5)};
    return std::max(volume, 0.0);      // Or: return volume > 0.0 ? volume : 0.0;
  }

private:
  std::string m_material;
};
```

Carton 对象的 volume() 函数假设材料厚度为 0.25，因此从每个维度减去 0.5 以考虑纸箱的侧边。如果由于某种原因创建的 Carton 对象任一维度小于 0.5，那么这将导致体积为负值，因此在这种情况下，纸箱的体积将被设置为 0。

注意，我们没有向 Carton 或 ToughPack 类的 volume() 函数添加 virtual 关键字。将 virtual 关键字应用于基类中的 volume() 函数，就足以确定派生类中该函数的所有定义也将是虚函数。你也可以选择为派生类函数使用 virtual 关键字，如图 15-2 所示。是否这样做是个人偏好问题。我们将在本章后面回到这个选择。

程序现在干净地完成了我们想要的功能。对 box 对象调用 showVolume() 会调用基类版本的 volume()。因为 box 的类型是 Box，下一次对 showVolume() 的调用是针对 ToughPack 对象 hardware 的。它调用从 Box 类继承的 showVolume() 函数，但 showVolume() 中对 volume() 的调用被解析为 ToughPack 类中定义的版本，因为 volume() 是虚函数。因此，你得到的是适合 ToughPack 对象计算的体积。对 carton 对象第三次调用 showVolume() 会调用 Carton 类版本的 volume()，所以你也得到了正确的结果。

接下来，使用指针 base 直接调用 volume() 函数，并通过非虚函数 showVolume() 间接调用它。该指针首先包含 Box 对象的地址，然后依次包含两个派生类对象的地址。每个对象的输出结果表明，在每种情况下都会自动选择适当版本的 volume() 函数，因此你清楚地演示了多态性的实际作用。

## 虚函数运行的要求

要使函数表现出“虚”行为，其在派生类中的定义必须与基类中的签名相同。例如，如果基类函数是 const，那么派生类函数因此也必须是 const。通常，派生类中虚函数的返回类型也必须与基类中的相同，但当基类中的返回类型是指向类类型的指针或引用时存在例外。在这种情况下，虚函数的派生类版本可以返回指向比基类更专门类型的指针或引用。我们不会进一步深入讨论这一点，但如果你在其他地方遇到它，与这些返回类型相关的技术术语是协变。

如果派生类中函数的函数名和参数列表与基类中声明的虚函数相同，那么虚函数的返回类型必须相同。如果不同，派生类函数将无法编译。另一个限制是虚函数不能是模板函数。

在标准的面向对象编程术语中，派生类中重新定义基类虚函数的函数被称为重写该函数。与基类中虚函数同名的函数，只有在它们的签名其余部分也完全匹配时，才会重写该函数；如果不匹配，派生类中的函数就是一个新函数，它会隐藏基类中的函数。后者就是我们在上一章讨论重复成员函数名称时看到的情况。

这当然意味着，如果你尝试在派生类中为虚函数使用不同的参数或不同的 const 说明符，那么虚函数机制将不起作用。派生类中的函数随后定义了一个新的、不同的函数——因此这个新函数将使用在编译时建立并固定的静态绑定进行操作。

你可以通过从 Carton 类中 volume() 的定义里删除 const 关键字并再次运行 Ex15_02 来测试这一点。Carton 中的 volume() 函数签名不再与 Box 中的虚函数匹配，因此派生类的 volume() 函数不是虚函数。因此，解析是静态的，所以通过基类指针为 Carton 对象调用的函数，甚至通过 showVolume() 函数间接调用的函数，都是基类版本。

将 virtual 关键字用于基类函数，并对派生类中所有虚函数重写应用 override 说明符。但如果你觉得有帮助，也可以随意为函数重写包含 virtual 关键字。

## 使用 final

有时你可能希望防止成员函数在派生类中被重写。例如，这可能是因为你想限制派生类修改类接口行为的方式。你可以通过指定函数为 final 来做到这一点。你可以像这样指定，以防止 Carton 类中的 volume() 函数被从 Carton 派生的类中的定义重写：

```
    class Carton : public Box
    {
        public:
            double volume() const override final
            {
                // Function body as before...
            }

            // Details of the class as in Ex15_02...
    };
```

在将 Carton 作为基类的类中尝试重写 volume() 将导致编译器错误。这确保只有 Carton 版本可以用于派生类对象。放置 override 和 final 关键字的顺序无关紧要——因此 override final 和 final override 都是正确的——但两者都必须位于 const 或函数签名的任何其他部分之后。

> **注意** 原则上，你可以声明一个既是 virtual 又是 final 的成员函数，即使它不重写任何基类成员。不过，这将是自相矛盾的。你添加 virtual 是为了允许函数重写，而添加 final 是为了阻止重写。注意，将 override 和 final 组合在一起并不矛盾。这只是表示你不允许对你正在重写的函数进行任何进一步的重写。

你也可以将整个类指定为 final，像这样：

```
    class Carton final : public Box
    {
        public:
            double volume() const override
            {
                // Function body as before...
            }

            // Details of the class as in Ex15_02...
    };
```

现在编译器将不允许将 Carton 用作基类。不可能再从 Carton 类进一步派生。注意，这一次对没有自己基类的类使用 final 是完全合理的。不过，没有意义的是在 final 类中引入新的虚函数，即不重写基类函数的虚函数。
