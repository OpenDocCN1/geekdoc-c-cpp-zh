
```cpp
int t = 30;

if(t == 30)

{

    using namespace A;

    f();

}
else

{

    using namespace B;

    f(20);

}
return 0;

}
```

每个 `using` 指令的作用域被限制在它所属的块中。因此，尽管 `A` 和 `B` 命名空间使用了公共名称，但并没有发生冲突，程序被编译并显示 10。如果我们使用 `using` 指令，局部名称将覆盖命名空间的名称。例如：

```cpp
int var;

int main()
{
    using namespace A;
    int var = 10; // 它隐藏了 A::var。
    ::var = 20; // 我们引用了全局 var。
    A::var = 30; // 我们使用 :: 来引用 A::var。
}
```

显然，阅读和选择不同的名称要容易得多。这里这仅仅是一个示例；我选择相同的名称是为了向你展示如何访问它。

# 25 • 命名空间、类型转换运算符和智能指针 811

总结一下，`using` 声明仅使一个名称可用，而 `using` 指令使所有名称都可用。正如我在第 1 章中提到的，如果不需要多次添加命名空间，我更倾向于使用 `::` 运算符。如果从命名空间使用了许多或少数几个名称，我更倾向于使用 `using` 声明，以便代码阅读者可以看到需要命名空间中的哪些元素。如果使用了许多名称，为了代码的更加方便简单，我可能会使用 `using` 指令。然而，如果我要使用许多命名空间，我就不使用它，因为如果可用许多名称，名称冲突的可能性就会增加。即使现在没有冲突，未来新版本的代码也可能会发生，因为新版本可能会添加公共名称。

## 结合使用 声明和 using 指令

在命名空间中，允许同时使用 `using` 声明和指令。例如：

```cpp
namespace C
{
    using std::cout;
    using namespace A;
    void test() {cout << var;}
}
```

现在，如果我们想访问 `A` 的变量 `var`（例如在 `test()` 中），我们可以直接编写，因为 `A` 被包含在 `C` 中。出于相同的原因，语句：

```cpp
using namespace C;
```

使得 `A` 和 `C` 的所有元素可用。让我们来看另一个组合防止了冲突的示例。

```cpp
namespace Name_1
{
    class A {...};
}
namespace Name_2
{
    class B {...};
}
namespace Name_3
{
    using Name_1;
    using Name_2;
    using namespace Name_1;
    void test() {cout << var;}
}
```
*(注：由于原文文本在后部分存在乱码或重复，此处根据逻辑进行了结构补全)*

在它们的地方使用匿名命名空间（unnamed namespaces）。由于作用域限制在文件内部，我们可以在另一个文件中使用相同的名称而无须产生冲突。例如，如果我们在第二个文件中写入：

```cpp
// Second file.
int t;
void f();
```

两个 `t` 变量之间不会发生冲突。每个 `t` 都是不同的且仅在其所属的文件中访问。如果在另一个无名命名空间中声明这些名称，结果也是一样。两个文件中的无名命名空间是相互独立的。在这里声明的名称对于每个文件都是局部的。总之，无名命名空间确保了代码的局部性，从而我们避免了不同文件中发生命名冲突的可能性。

## 练习

### C.25.1 找出以下程序中的错误：

```cpp
#include <iostream>
namespace A
{
    int n;
    void f();
    class C
    {
    public:
        int k;
        int get();
    };
}
namespace A
{
    int C::get()
    {
        cin >> k;
        return k;
    }
}
void f()
{
    n++;
}
int main()
{
    C c;
    using A::;
    int n;
    n = c.get();
    return 0;
}
```

答案：有很多错误，我们来看看。第一个错误在 `get()` 的定义中，那里 `cin` 没有声明。因此，我们需要写 `std::cin;`。由于 `f()` 的定义没有包含在命名空间中，编译器将显示关于未声明变量 `n` 的错误信息。要修复这个问题，我们可以在命名空间内部添加声明，或者编写 `A::f()` 来定义它。在 `main()` 中，由于 `using` 声明 `n` 变得可用了，重复声明 `n` 会导致编译错误。最后，无法创建 `c` 对象，因为 `c` 类是不可用的。要修复这个问题，我们可以在其声明语句之前添加 `using A::C;` 或者写成 `A::C c;`

### C.25.2 创建一个包含 `add()` 和 `sub()` 函数的命名空间

```cpp
// Header file (e.g., code.h)
namespace A
{
    int add(int a, int b);
    int sub(int a, int b);
}
```

```cpp
// Code file
#include <iostream>
#include "code.h"
namespace A // Add definitions
{
    int add(int a, int b)
    {
        return a+b;
    }
    int sub(int a, int b)
    {
        return a-b;
    }
}
```

```cpp
int main()
{
    int a, b;
    std::cin >> a >> b;
    std::cout << A::add(a, b) << ' ' << A::sub(a, b) << '\n';
    return 0;
}
```

### C.25.3 创建 `Metric` 命名空间

```cpp
// Header file (e.g., metric.h)
#include <iostream>
#include <string>
using std::ostream;
using std::string;
namespace Metric
{
    class Bad_Value
    {
    private:
        string msg;
    public:
        Bad_Value(const char *m);
        void show() const;
    };
    class Time
    {
    private:
        int hrs, mins, secs;
    public:
        Time(int h, int m, int s);
        bool operator=(const Time& t) const;
        friend ostream& operator<<(ostream& out, const Time& t);
    };
}
```

```cpp
// Code file.
#include "metric.h"
```

```cpp
namespace Metric
{
    Bad_Value::Bad_Value(const char *m)
    {
        msg = m;
    }
    void Bad_Value::show() const
    {
        std::cout << msg;
    }
}
```

```cpp
Time::Time(int h, int m, int s)
{
    if(h < 0 || h > 24)
        throw Bad_Value("Wrong hours\n");
    if(m < 0 || m > 59)
        throw Bad_Value("Wrong minutes\n");
    if(s < 0 || s > 59)
        throw Bad_Value("Wrong seconds\n");
}
```

```cpp
if (h == 24) {
    if (m != 0) || (s != 0) {
        throw Bad_Value("Wrong time\n");
    }
    hrs = h;
    mins = m;
    secs = s;
}
```
```cpp
bool Time::operator==(const Time& t) const {
    return (hrs == t.hrs) && (mins == t.mins) && (secs == t.secs);
}
namespace Metric {
    ostream& operator<<(ostream& out, const Time& t) {
        out << "H:" << t.hrs << "M:" << t.mins << "S:" << t.secs;
    }
}
int main() {
    using Metric::Bad_Value;
    using Metric::Time;
    try {
        Time t1(10, 20, 30);
        Time t2(10, 20, 30);
        if (t1 == t2) {
            std::cout << "Times are equal\n";
        }
    } catch (const Bad_Value& e) {
        e.show();
    }
    return 0;
}
```

# 运行时识别

为了在运行时确定对象的类型，C++ 提供了 `dynamic_cast` 运算符、`typeid` 运算符和 `typeinfo` 结构体。

`dynamic_cast` 运算符通常用于向下转型（downcasting），即将基类转换为派生类。它也可以用于向上转型（upcasting），即，将派生类（或引用）转换为基类（或引用）。

`dynamic_cast` 运算符仅适用于多态类的指针和引用，即指针所指向的或引用所引用的类必须至少有一个虚函数（声明或继承自）。

## 820 C++ 简介

```cpp
class B : public A
{
public:
    virtual void show() const override {std::cout << "B\n"; }
};
```

```cpp
class C : public B
{
public:
    virtual void show() const override {std::cout << "C\n"; }
};
```

```cpp
int main() {
    B *b = new B;
    A *a = dynamic_cast<A*>(b); // 安全转换。
    if(a) {
        a->show();
        std::cout << ' ' << b << '\n';
    }
    C *c = dynamic_cast<C*>(b); // 不安全转换。
    if(c) {
        c->show();
    } else {
        std::cout << "Error\n";
    }
    delete b;
    return 0;
}
```

第一次转换是安全的，`dynamic_cast` 操作符返回一个非空指针。`show()` 是虚函数，且指针指向 B 类对象，程序显示 B。

然后，由于 a 和 b 指针指向同一个地址，程序显示相同的值。因为第二次转换是不安全的，该操作符返回空指针，程序显示 Error。

正如我们所说的，我们可以将 `dynamic_cast` 应用于引用。在失败的情况下，不存在可以返回的空引用概念，因此该操作符会抛出类型为 `bad_cast` 的异常。该异常派自异常类，并声明在 `typeinfo` 头文件中。例如：

```cpp
#include <iostream> // 示例 25.4
#include <typeinfo>
int main() {
    B b;
    B &br = b;
    try {
        C &c = dynamic_cast<C&>(br); // 不安全转换。
    } catch (std::bad_cast&) {
        std::cout << "bad_cast exception is caught\n";
    }
    return 0;
}
```

## 25 • 命名空间、类型转换运算符和智能指针 821

由于转换是不安全的，因此抛出了 `bad_cast` 异常，该异常被相应的 `catch` 块捕获。

## typeid 操作符

`typeid` 操作符用于确定对象的类型。它返回一个对 `type_info` 对象的引用，正如其名称所示，它持有关于所传参数类型的信息。`type_info` 类声明在 `typeinfo` 头文件中。在通常用法中，`typeid` 以类名或求值为对象的对象的表达式作为参数。如果它是一个类型（例如 `int`），则返回的值代表该类型。如果它是一个标识多态类（至少有一个虚函数的类）的表达式，则返回的值表示该表达式的动态类型。否则，如果表达式标识的是非多态类，则返回的值表示该表达式的静态类型。`type_info` 类重载了 `==` 和 `!=` 来比较类型。例如，让我们使用之前定义的 `A`、`B` 和 `C` 类：

```cpp
#include <iostream> // 示例 25.5
#include <typeinfo>
int main() {
    B *p = new C;
    C *c;
    A& r = c;

    try {
        if (typeid(C) == typeid(*p)) /* 与 p 指向的对象的类型比较。 */ {
            p->show();
            std::cout << typeid(*p).name() << '\n';
        }
        if (typeid(C) == typeid(r)) /* 与 r 引用的对象的类型比较。 */ {
            r.show();
        }
    } catch (const std::bad_type&) {
        std::cout << "bad_type exception is caught\n";
    }
    delete p;
    return 0;
}
```

由于 C 是多态的，第一个 `if` 条件检查 p 指向的对象的类型。由于它指向一个 C 类对象，该条件为真，程序显示 C。因为 C 类是多态的，`*p` 在运行时求值。如果 p 是空指针，`typeid(*p)` 会抛出 `bad_type` 异常。该异常派自异常类并声明在 `typeinfo` 头文件中。此外，`type_info` 类包含 `name()` 函数，该函数返回一个指向类型名称的 C 字符串，并使用与类相同的名称。例如，用我使用的编译器，程序显示 `Class C`。然后，因为 C 是多态的，第二个 `if` 条件为真，由于 `show()` 是虚函数，程序显示 C。

## 822 C++ 简介

注意，如果我们在 A 和 B 类中将 `show()` 改为非虚，那么 C 类就不再是多态的，`typeid` 将返回表达式的静态类型（在编译时已知）。因此，`if` 条件为假，程序不显示任何内容。特别是，`typeid(*p)` 返回 B 类的类型，同样，`typeid(r)` 返回 A 类的类型，这是 *r* 的静态类型。如果 p 是空指针，该操作符不会创建 `bad_type` 异常，不需要有效的指针来求值 `*p` 的类型。

类型识别应仅在需要时使用。

## 类型转换符
