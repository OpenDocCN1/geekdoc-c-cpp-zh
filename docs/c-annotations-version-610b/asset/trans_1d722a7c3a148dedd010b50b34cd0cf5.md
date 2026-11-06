

![](img/859c398c8f9601f32700b78894504b0a_366_0.png)

图 14.5：定义虚函数时对象的内部组织。

![](img/859c398c8f9601f32700b78894504b0a_366_1.png)

图 14.6：补充图，由 Guillaume Caumon 提供。

![](img/859c398c8f9601f32700b78894504b0a_368_0.png)

图 14.7：具有多个基类时的 Vtables 和 vpointers

## 14.11 未定义的对 vtable 的引用……

有时，链接器会生成如下错误：

```text
In function `Derived::Derived()`:
    undefined reference to `vtable for Derived`
```

当派生类中缺少虚函数的实现，但该函数又在派生类的接口中被提及时，就会生成此错误。

这种情况很容易遇到：

- 构造一个（完整的）基类，其中定义虚成员函数；
- 构造一个 Derived 类，并在其接口中提及该虚函数；
- Derived 类的虚函数未实现。当然，编译器并不知道派生类的函数未实现，并且在被要求时会生成用于创建派生类对象的代码；
- 最终，链接器无法找到派生类的虚成员函数。因此，它无法构造派生类的 vtable；
- 链接器报错并给出如下消息：

```text
undefined reference to `vtable for Derived`
```

下面是一个会产生该错误的示例：

```cpp
class Base
{
    virtual void member();
};
inline void Base::member()
{}
class Derived: public Base
{
    virtual void member();       // only declared
};
int main()
{
    Derived d;  // Will compile, since all members were declared.
                // Linking will fail, since we don’t have the
                // implementation of Derived::member()
}
```

当然，纠正这个错误很容易：实现派生类中缺失的虚成员函数。

虚函数*绝不*应该以内联方式实现。由于 vtable 包含类的虚函数地址，这些函数必须具有地址，因此它们必须被编译为真正的（非内联的）函数。通过将虚函数定义为内联，你会冒这样的风险：编译器可能直接忽略这些函数（因为它们很可能永远不会被显式调用（而只会以多态方式，从基类指针或引用调用））。结果，它们的地址可能永远不会进入其类的 vtable（甚至 vtable 本身也可能保持未定义），从而导致链接问题，或使程序表现出意外行为。所有这类问题都可以简单地避免：绝不要将虚成员定义为内联（另见第 7.7.2.1 节）。

## 14.12 虚构造函数

在第 14.2 节中，我们了解到 C++ 支持*虚析构函数*。然而，与许多其他面向对象语言（例如 Java）一样，*虚构造函数*的概念并不受支持。当只有基类引用或指针可用，并且需要派生类对象的副本时，没有虚构造函数就会成为一个缺陷。Gamma *et al.*（1995）讨论了*原型设计模式*来处理这种情况。

根据*原型设计模式*，每个派生类都负责实现一个成员函数，该函数返回一个指针，指向调用该成员函数的对象的副本。这个函数通常命名为 clone。为了将用户接口与重新实现接口分离，clone 被纳入接口，而 newCopy 定义在重新实现接口中。支持“克隆”的基类定义一个虚析构函数、clone（返回 newCopy 的返回值）以及*虚拷贝构造函数*（一个纯虚函数），其原型为 `virtual Base * newCopy() const = 0`。由于 newCopy 是纯虚函数，所有派生类现在都必须实现自己的“虚构造函数”。

在大多数拥有基类指针或引用的情况下，这种设置已经足够，但在用于抽象容器时就会失败。我们不能创建 `vector<Base>`，因为 Base 的接口中包含纯虚拷贝成员，而 Base 会被调用来初始化这种 vector 的新元素。这是不可能的，因为 newCopy 是纯虚函数，所以无法构造 Base 对象。

直观的解决方案——为 newCopy 提供默认实现，将其定义为普通虚函数——也会失败，因为容器会调用 Base（Base const & other），而该构造函数将不得不调用 newCopy 来拷贝 other。此时不清楚该如何处理那个副本，因为新的 Base 对象已经存在，并且不包含可用于接收 newCopy 返回值的 Base 指针或引用数据成员。

另一种方案（也是首选方案）是让原来的 Base 类（定义为抽象基类）保持原样，并使用包装类 Clonable 来管理 newCopy 返回的 Base 类指针。第 17 章讨论了将 Base 和 Clonable 合并为一个类的方法，但现在我们将 Base 和 Clonable 定义为独立的类。

Clonable 类是一个非常标准的类。它包含一个指针成员，因此需要拷贝构造函数、析构函数和重载赋值运算符。它至少有一个非标准成员：`Base & base() const`，返回一个引用，指向 Clonable 的 `Base * data` 成员所引用的派生对象。它还提供了一个额外的构造函数来初始化其 `Base * data` 成员。

任何从 Base 派生的非抽象类都必须实现 `Base *newCopy()`，返回一个指针，指向为调用 newCopy 的对象新创建（分配）的副本。

一旦定义了派生类（例如 Derived1），我们就可以很好地利用 Clonable 和 Base 设施。在下一个示例中，我们看到 main 定义了一个 `vector<Clonable>`。然后，通过以下步骤将一个匿名 Derived1 对象插入该 vector：

- 创建一个新的匿名 `Derived1` 对象；
- 它使用 `Clonable(Base *bp)` 初始化一个 `Clonable`；
- 刚刚创建的 `Clonable` 对象使用 `Clonable` 的移动构造函数插入 vector。此时只有临时的 Derived 和 Clonable 对象，因此不需要拷贝构造。

在这个序列中，只使用了包含 `Derived1 *` 的 Clonable 对象。不需要进行（或销毁）额外的副本。

接下来，base 成员与 `typeof` 结合使用，以显示 Base & 对象的实际类型：一个 Derived1 对象。

随后，main 中包含一个有趣的声明 `vector<Clonable> v2(bv)`。这里创建了 bv 的一个副本。这个拷贝构造会观察 Base 引用的实际类型，确保适当的类型出现在 vector 的副本中。在程序结束时，我们创建了两个 Derived1 对象，它们由 vector 的析构函数正确删除。下面是完整程序，演示了“虚构造函数”概念：

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <typeinfo>

// Base and its inline member:
class Base
{
    public:
        virtual ~Base();
        Base *clone() const;
    private:
        virtual Base *newCopy() const = 0;
};
inline Base *Base::clone() const
{
    return newCopy();
}

// Clonable and its inline members:
class Clonable
{
    Base *d_bp;

    public:
        Clonable();
        explicit Clonable(Base *base);
        ~Clonable();
        Clonable(Clonable const &other);
        Clonable(Clonable &&tmp);
        Clonable &operator=(Clonable const &other);
        Clonable &operator=(Clonable &&tmp);

        Base &base() const;
};
inline Clonable::Clonable()
:
    d_bp(0)
{}
inline Clonable::Clonable(Base *bp)
:
    d_bp(bp)
{}
inline Clonable::Clonable(Clonable const &other)
:
    d_bp(other.d_bp->clone())
{}
inline Clonable::Clonable(Clonable &&tmp)
:
    d_bp(tmp.d_bp)
{
    tmp.d_bp = 0;
}
inline Clonable::~Clonable()
```

\* Jesse van den Kieboom 创建了类 Clonable 的另一种实现，以类模板实现。他的实现可在此处找到。

