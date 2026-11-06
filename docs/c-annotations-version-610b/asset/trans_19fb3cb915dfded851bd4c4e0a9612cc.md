

## 14.5 虚函数与多重继承

在第6章中，我们遇到了 `fstream` 类，它是一个同时具备 `ifstream` 和 `ofstream` 特性的类。在第13章中，我们了解到一个类可以从多个基类派生。这样的派生类继承了其所有基类的属性。多态性也可以与多重继承结合使用。

考虑一下，如果从派生类到其（基）类有多条“路径”会怎样。下一个（虚构的）示例说明了这一点，其中类 `Derived` 从 `Base` 双重派生：

```cpp
class Base
{
    int d_field;
    public:
        void setfield(int val);
        int field() const;
};
inline void Base::setfield(int val)
{
    d_field = val;
}
inline int Base::field() const
{
    return d_field;
}

class Derived: public Base, public Base
{
};
```

由于双重派生，`Base` 的功能在 `Derived` 中出现了两次。这导致了歧义：当对 `Derived` 类对象调用 `setfield()` 函数时，由于有两个这样的函数，到底会调用哪一个呢？作用域解析运算符也无法解决这个问题，因此 C++ 编译器无法编译上述示例，并且（正确地）识别出一个错误。

上面的代码显然在派生过程中重复了其基类，这当然可以通过不从 `Base` 双重派生（或者使用组合（！））来轻松避免。但基类的重复也可能通过嵌套继承发生，例如一个对象派生自 `Auto` 和 `Air`（参见第13.1节）。这样的类将用于表示例如飞行汽车³。一个 `AirAuto` 最终将包含两个 `Vehicle`，因此包含两个 `mass` 字段、两个 `setMass()` 函数和两个 `mass()` 函数。这是我们想要的吗？

### 14.5.1 多重继承中的歧义

让我们更仔细地研究一下，为什么从 `Auto` 和 `Air` 派生出的 `AirAuto` 会引入歧义。

- 一个 `AirAuto` 是一个 `Auto`，因此是一个 `Land`，因此是一个 `Vehicle`。
- 然而，一个 `AirAuto` 也是一个 `Air`，因此也是一个 `Vehicle`。

`Vehicle` 数据的重复在图14.1中进一步说明。`AirAuto` 的内部组织如图14.2所示。C++ 编译器检测到 `AirAuto` 对象中的歧义，因此不会编译如下语句：

```cpp
AirAuto jBond;
cout << jBond.mass() << '\n';
```

³比如詹姆斯·邦德与金枪人中的那辆……

![](img/859c398c8f9601f32700b78894504b0a_343_0.png)

图14.1：多重派生中基类的重复。

![](img/859c398c8f9601f32700b78894504b0a_343_1.png)

图14.2：`AirAuto` 对象的内部组织。

编译器无法确定调用哪个成员函数 `mass`，但程序员有两种方法可以为编译器解决歧义：

- 首先，可以修改产生歧义的函数调用。使用作用域解析运算符来解决歧义：

```cpp
// 让我们希望质量保存在 Auto
// 部分对象中..
cout << jBond.Auto::mass() << '\n';
```

作用域解析运算符和类名放在成员函数名的正前方。

- 其次，可以为类 `AirAuto` 创建一个专门的 `mass` 函数：

```cpp
int AirAuto::mass() const
{
    return Auto::mass();
}
```

第二种方法更可取，因为它不需要编译器标记错误；也不需要使用 `AirAuto` 类的程序员采取特殊预防措施。

然而，存在一种更优雅的解决方案，将在下一节中讨论。

### 14.5.2 虚基类

如图14.2所示，一个 `AirAuto` 表示*两个* `Vehicle`。这不仅导致访问质量数据时使用哪个函数的歧义，还在 `AirAuto` 中定义了两个质量字段。这有点冗余，因为我们可以假设一个 `AirAuto` 只有一个质量。

![](img/859c398c8f9601f32700b78894504b0a_344_0.png)

图14.3：当基类为虚基类时 `AirAuto` 对象的内部组织。

然而，可以将 `AirAuto` 定义为一个仅包含一个 `Vehicle` 的类，同时又使用多重派生。这可以通过将派生类继承树中多次出现的基类定义为*虚基类*来实现。

对于类 `AirAuto`，这意味着从 `Land` 和 `Air` 类派生 `AirAuto` 时需要做一个小改动：

```cpp
class Land: virtual public Vehicle
{
    // 等等
};
class Auto: public Land
{
    // 等等
};
class Air: virtual public Vehicle
{
    // 等等
};
class AirAuto: public Auto, public Air
{
};
```

虚派生确保 `Vehicle` 只被添加到派生类一次。这意味着 `Vehicle` 被添加到 `AirAuto` 的路径不再取决于其直接基类；我们只能说 `AirAuto` 是一个 `Vehicle`。虚派生后 `AirAuto` 的内部组织如图14.3所示。

当一个类 `Third` 继承自基类 `Second`，而 `Second` 又继承自基类 `First` 时，当构造 `Third` 对象时，如果使用该 `Second` 构造函数，那么 `Second` 构造函数调用的 `First` 类构造函数也会被使用。示例：

```cpp
class First
{
    public:
        First(int x);
};
class Second: public First
{
    public:
        Second(int x)
        :
            First(x)
        {}
};
class Third: public Second
{
    public:
        Third(int x)
        :
            Second(x)          // 调用 First(x)
        {}
};
```

当 `Second` 使用虚派生时，上述情况不再成立。当 `Second` 使用虚派生时，当从 `Third` 调用 `Second` 的构造函数时，其基类构造函数会被忽略。取而代之的是，`Second` 默认调用 `First` 的默认构造函数。下一个示例说明了这一点：

```cpp
class First
{
    public:
        First()
        {
            cout << "First()\n";
        }
        First(int x);
};
class Second: public virtual First       // 注意：virtual
{
    public:
        Second(int x)
        :
            First(x)
        {}
};
class Third: public Second
{
    public:
        Third(int x)
        :
            Second(x)
        {}
};
int main()
{
    Third third(3);      // 显示 "First()"
}
```

构造 `Third` 时，默认使用 `First` 的默认构造函数。然而，`Third` 的构造函数可以通过显式指定要使用的构造函数来覆盖此默认行为。由于 `First` 对象必须在 `Second` 可构造之前可用，因此必须首先指定它。要在构造 `Third(int)` 时调用 `First(int)`，后者的构造函数可以定义如下：

```cpp
class Third: public Second
{
    public:
        Third(int x)
        :
            First(x),          // 现在调用 First(int)。
            Second(x)
        {}
};
```

当使用简单的线性继承时，这种行为可能看起来令人费解，但当使用多重继承且基类使用虚继承时，它就变得有意义了。考虑 `AirAuto`：当 `Air` 和 `Auto` 都虚继承自 `Vehicle` 时，`Air` 和 `Auto` 是否都会初始化共同的 `Vehicle` 对象？如果是，哪个会先被调用？如果 `Air` 和 `Auto` 使用不同的 `Vehicle` 构造函数怎么办？所有这些疑问都可以通过将公共基类初始化的责任交给最终使用公共基类对象的类来避免。在上面的例子中是 `Third`。因此，`Third` 有机会在初始化 `First` 时指定要使用的构造函数。

多重继承也可以用于继承那些并非都使用虚继承的类。假设我们有两个类 `Derived1` 和 `Derived2`，它们都（可能虚）继承自 `Base`。

现在我们讨论在调用类 `Final` 的构造函数时会调用哪些构造函数：

```cpp
class Final: public Derived1, public Derived2
```

为了区分涉及的构造函数，`Base1` 表示作为 `Derived1` 的基类初始化器调用的 `Base` 类构造函数（类似地：`Base2` 是从 `Derived2` 调用的）。普通的 `Base` 表示 `Base` 的默认构造函数。

`Derived1` 和 `Derived2` 表示构造 `Final` 对象时使用的基类初始化器。

现在我们准备区分构造类 `Final`（`class Final: public Derived1, public Derived2`）的对象时的各种情况：

| 类 | 按顺序调用的构造函数 | 说明 |
|---|---|---|
| `Derived1: public Base`<br>`Derived2: public Base` | `Base1, Derived1, Base2, Derived2` | 这是普通的非虚多重派生。 |
| `Derived1: public Base`<br>`Derived2: virtual public Base` | `Base, Base1, Derived1, Derived2` | 只有 `Derived2` 使用虚派生。`Derived2` 的基类构造函数被忽略。取而代之的是，调用 `Base`，并且它先于任何其他构造函数被调用。由于只有一个类使用虚派生，最终的 `Final` 类中仍然存在两个 `Base` 类对象。 |
| `Derived1: virtual public Base`<br>`Derived2: public Base` | `Base, Derived1, Base2, Derived2` | 只有 `Derived1` 使用虚派生。`Derived1` 的基类构造函数被忽略。取而代之的是，调用 `Base`，并且它先于任何其他构造函数被调用。与第一种（非虚）情况不同，现在调用的是 `Base`，而不是 `Base1`。 |

