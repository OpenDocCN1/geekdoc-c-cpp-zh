
如果你定义一个没有参数的构造函数，它就是显式默认构造函数。也可以定义一个带参数的构造函数，并通过默认实参使其仍然成为默认构造函数，我们稍后会讨论这一点。

如果你定义一个至少有一个必需参数的构造函数，那么编译器不会生成默认构造函数。如果你想要默认构造函数，就必须显式定义一个。

## 函数声明中的默认实参

C++ 中的构造函数以及一般函数，可以在其声明中为部分或全部参数指定默认实参（类似于 C# 的可选参数）。在 C++ 函数中，函数声明里所有带默认实参的参数都必须出现在任何不带默认实参的参数的右侧。C++ 不支持 C 风格的命名实参，但你可以使用[命名参数惯用法](#)实现类似效果。

为什么这里要提到默认实参？事实证明，如果某个构造函数的所有参数都有默认实参，那么该构造函数就是默认构造函数。这很合理，因为如果你有一个签名为 `Vehicle(VehicleType type = VehicleType::Car, double odometerReading = 0.0);` 的构造函数，那么你可以用空括号调用该构造函数，并使用那些默认实参。如果你定义默认构造函数，那么只能有一个，无论它没有参数，还是它的所有参数都有默认实参。

这一原则还可进一步推广。在同一作用域中声明的同名函数，不能在这些完全相同的位置上具有相同的参数类型。你猜对了：为了区分函数签名，带默认实参的参数会被忽略。

这一切都说得通，因为默认实参使得无法区分 `double Add(double a, double b = 0.0);` 和 `double Add(double a, int b = 0);`，因为二者都可以像 `double dbl = Add(5.0);` 这样调用。编译器在这种情况下无法知道你想要哪一个，所以它干脆编译失败并显示错误消息。

## 带参构造函数

带参构造函数有一个或多个参数。如果带参构造函数的所有参数都有默认实参，那么它也是类的默认构造函数。C++ 中的带参构造函数没有什么特别之处。

## 转换构造函数

转换构造函数至少有一个参数。如果有多个参数，那么这些额外参数必须具有默认实参。

如果你不希望某个构造函数成为转换构造函数，可以用函数说明符 explicit 标记它。看一个示例：

```cpp
#include <string>

class SomeClass
{
public:
        SomeClass(const wchar_t* value) :
                m_strValue(value),
                m_intValue()
        {
        }

        explicit SomeClass(int value) :
                m_strValue(),
                m_intValue(value)
        {
        }

        ~SomeClass(void) { }

        const wchar_t* GetStringValue(void)
        {
                return m_strValue.c_str();
        }

        int GetIntValue(void) { return m_intValue; }

private:
        std::wstring        m_strValue;
        int                 m_intValue;
};

void DoSomething(void)
{
    // Normal constructor use.
    SomeClass sc1 = SomeClass(L"Hello World");

    // Fine because the const wchar_t* constructor
    // is a conversion constructor.
    SomeClass sc2 = L"Hello World";

    // Normal constructor use.
    SomeClass sc3 = SomeClass(1);

    //// Illegal since the int constructor is not a
    //// conversion constructor.
    //SomeClass sc4 = 1;

    // ...
}
```

如你所见，转换构造函数让我们可以通过直接将 sc2 设置为字符串值来构造它。编译器看到该语句，检查 SomeClass 是否有一个能接收这类值的转换构造函数，然后继续调用适当的 SomeClass 构造函数。如果我们对注释掉的 sc4 行尝试这样做，编译器会失败，因为我们使用 explicit 告诉编译器，那个接受 int 的构造函数不应被视为转换构造函数，而应像其他任何带参构造函数一样。

转换构造函数可能有用，但也可能导致缺陷。例如，当你只是拼错变量名而本意是赋值时，可能会意外创建一个新对象并将其赋给现有变量。如果存在有效的转换构造函数，编译器不会报错；如果不存在，则会报错。因此请记住这一点，并记得将单参数构造函数标记为 explicit，除非你有充分理由提供转换构造函数。

```cpp
        int        m_value;
};

class B : virtual public A
{
public:
        explicit B(int) :
                A(CallingMsg(L"A")),
                m_b(InitializingIntMsg(2, L"m_b")),
                m_a(InitializingIntMsg(5, L"m_a"))
        {
                wcout << L"Constructing B. m_a is " <<
                        m_a << L" and m_b is " << m_b << L"." << endl;
        }
        virtual ~B(void)
        {
                wcout << L"Destroying B." << endl;
        }

private:
        int        m_a;
        int        m_b;
};

class C
{
public:
        explicit C(int) :
                m_c(InitializingIntMsg(0, L"m_c"))
        {
                wcout << L"Constructing C. m_c is " <<
                        m_c << L"." << endl;
        }
        virtual ~C(void)
        {
                wcout << L"Destroying C." << endl;
        }

private:
        int        m_c;
};

class D
{
public:
        explicit D(int) :
                m_d(InitializingIntMsg(3, L"m_d"))
        {
                wcout << L"Constructing D. m_d is " <<
                        m_d << L"." << endl;
        }
        virtual ~D(void)
        {
                wcout << L"Destroying D." << endl;
        }

private:
```

```cpp
wcout << endl << "Break between Y and Z." << endl
     << endl;

{
        Z someZ(CallingMsg(L"Z"));
        wcout << L"Z::GetSomeInt returns " <<
        someZ.GetSomeInt() << L"." << endl;
}
return 0;
}
```

我们做的第一件事是定义两个写消息的辅助函数，这样就能轻松跟踪事情发生的顺序。你会注意到，每个类都有一个接受 int 的构造函数，不过只有 Y 和 Z 实际使用了它。A、B、C 和 D 甚至没有在其 int 参数构造函数中为这个 int 指定名称；它们只是指定有一个 int 参数。这完全是合法的 C++ 代码，而我们一直在 main 中使用自定义参数名。A 类有两个构造函数：一个默认构造函数和一个接受 int 的带参构造函数。其余类只有带参构造函数，每个都接受一个 int。

- B 类虚继承自 A。
- C 类不继承任何类。
- D 类不继承任何类。
- Y 类按该顺序虚继承自 B、直接继承自 D、虚继承自 C。
- Z 类同样按该顺序直接继承自 D、虚继承自 B、直接继承自 C。

让我们看看该程序给我们的输出，然后讨论正在发生什么以及为什么。

```text
Calling Y constructor.
Initializing DEFAULT m_value.
DEFAULT Constructing A. m_value is '5'.
Calling B constructor.
Initializing m_a.
Initializing m_b.
Constructing B. m_a is '5' and m_b is '2'.
Calling C constructor.
Initializing m_c.
Constructing C. m_c is '0'.
Calling D constructor.
Initializing m_d.
Constructing D. m_d is '3'.
Initializing m_someInt.
Constructing Y. m_someInt is '0'.
Y::GetSomeInt returns '0'.
Destroying Y.
Destroying D.
Destroying C.
Destroying B.
Destroying A.

Break between Y and Z.

Calling Z constructor.
Calling A constructor.
Initializing m_value.
Constructing A. m_value is '20'.
Calling B constructor.
Initializing m_a.
Initializing m_b.
Constructing B. m_a is '5' and m_b is '2'.
Calling D constructor.
Initializing m_d.
Constructing D. m_d is '3'.
Calling C constructor.
Initializing m_c.
Constructing C. m_c is '0'.
Initializing m_someInt.
Constructing Z. m_someInt is '0'.
Z::GetSomeInt returns '0'.
Destroying Z.
Destroying C.
Destroying D.
Destroying B.
Destroying A.
```

在我们的 main 函数中，首先在 Y 自己的作用域内创建一个 Y 类型的对象。然后调用它的 GetSomeInt 成员函数。这有助于确保即使你改动代码，编译器也不会在发布版本中优化掉 Y 的创建。它还充当构造与析构之间的标记。

然后我们退出 Y 的作用域，触发其析构。之后，我们写入另一个标记字符串，将 Y 实例的实例化与随后 Z 实例的实例化分隔开。我们在 Z 自己的作用域中创建 Z 实例，以便像跟踪 Y 一样跟踪它的构造和析构。

那么我们看到了什么？信息很多。先关注 Y。

当我们调用 Y 构造函数时，它做的第一件事是调用 A 的默认构造函数。由于若干原因，这看起来可能非常不对，但实际上是对的。Y 构造函数规定要遵循以下顺序：

1. 初始化基类 C。
2. 初始化 Y 的成员变量 m_someInt。
3. 初始化基类 D。
4. 初始化基类 B。

但最终得到的却是以下顺序：

1. 通过 A 的默认构造函数初始化基类 A。
2. 初始化基类 B。
3. 初始化基类 C。
4. 初始化基类 D。
5. 初始化 Y 的成员变量 m_someInt。

既然我们知道 B 虚继承自 A，并且 B 是 A 的唯一继承来源，我们可以得出结论：B 优先于其他类，而 A 优先于 B。
