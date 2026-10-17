
在这里，代码显式调用了 `Worker(const Worker &)` 构造函数。注意，这种用法对于虚基类是合法的且往往是必要的，但对于非虚基类来说是非法的。

## 注意事项

如果一个类具有间接虚基类，则该类的构造函数应该显式调用虚基类的构造函数，除非仅需要虚基类的默认构造函数。

# 哪种方法？

除了类构造函数规则的改变外，多重继承通常还需要其他调整。考虑将 `Show()` 方法扩展到 `SingingWaiter` 类中的问题。由于 `SingingWaiter` 对象没有新的数据成员，你可能认为可以直接使用继承的方法。这引出了一个问题。假设你省略了新版本的 `Show()`，并尝试使用 `SingingWaiter` 对象调用继承的 `Show()` 方法：

```cpp
SingingWaiter newhire("Elise Hawks", 2005, 6, soprano);
newhire.Show(); // 冲突
```

在单继承中，未重定义 `Show()` 会导致使用最新的祖先定义。在这种情况下，每个直接祖先都有 `Show()` 函数，导致此调用产生义。

## 注意事项

多重继承会导致函数调用冲突。例如，`BadDude` 类可能继承自 `Gunslinger` 类和 `PokerPlayer` 类的 `Draw()` 方法。你可以使用作用域解析符来明确你的意思：

```cpp
SingingWaiter newhire("Elise Hawks", 2005, 6, soprano);
newhire.Singer::Show(); // 使用 Singer 版本
```

然而，更好的方法是在 `SingingWaiter` 中重定义 `Show()` 并指定使用哪个 `Show()`。例如，如果你想让 `SingingWaiter` 使用 `Singer` 版本，你可以这样做。这种让派生方法调用基方法的方法对于单继承来说足够了。例如，假设 `HeadWaiter` 类派生自 `Waiter` 类。你可以使用如下定义序列，每个派生类都增加其基类显示的信息：

```cpp
void Worker::Show() const
{
    cout << "Name: " << "\n";
    cout << "Employee ID: " << id << "\n";
}
```

```cpp
void Worker::Show() const
{
    Worker::Show();
    cout << "Panache rating: " << panache << "\n";
}
```

```cpp
void HeadWaiter::Show() const
{
    Waiter::Show();
    cout << "Presence rating: " << presence << "\n";
}
```

这种增量方法在 `SingerWaiter` 案例中失效了。然而，以下方法忽略了 `Waiter` 组件：

```cpp
void SingingWaiter::Show()
{
    Singer::Show();
}
```

你可以通过调用 `Waiter` 基类版本来修复这个问题：

```cpp
void SingingWaiter::Show()
{
    Singer::Show();
    Waiter::Show();
}
```

这会显示两次姓名和 ID，因为 `Singer::Show()` 和 `Waiter::Show()` 都调用了 `Worker::Show()`。

如何修复这个问题？一种方法是使用模块化方法而不是增量方法。即，使用一个只显示 `Worker` 组件的方法，另一个只显示 `Waiter` 组件的方法（而不是 `Waiter` 加上 `Worker` 组件），以及另一个只显示 `Singer` 组件的方法。那么

## 第14 章 在 C++ 中重用代码

`SingingWaiter::Show()` 方法可以将这些组件组合在一起。例如，你可以这样使用：

```cpp
void Worker::Data() const
{
    cout << "Name: " << fullname << "\n";
    cout << "Employee ID: " << id << "\n";
}
```

```cpp
void Waiter::Data() const
{
    cout << "Panache rating: " << panache << "\n";
}
```

```cpp
void Singer::Data() const
{
    cout << "Vocal range: " << pv[voice] << "\n";
}
```

```cpp
void SingingWaiter::Data() const
{
    Singer::Data();
    Waiter::Data();
}
```

```cpp
void SingingWaiter::Show() const
{
    cout << "Category: singing waiter\n";
    Worker::Data();
    Data();
}
```

同样，其他的 `Show()` 方法也将由适当的 `Data()` 组件构建。
通过这种方法，对象仍然会公使用 `Show()` 方法。另一方面，`Data()` 方法应该是类的内部方法；它们应该是用于辅助公共接口的帮助方法。然而，将 `Data()` 方法设为私有将防止（例如）`Waiter` 代码使用 `Worker::Data()`。这就是受保护访问类类的用处。如果 `Data()` 方法是受保护的，它们可以在层次结构中的所有类中内部使用，同时对外部世界隐藏。

另一种方法是将所有的数据组件设为私有，但使用受保护方法而不是受保护数据，可以对数据的允许访问进行更严格的控制。
请求数据以设置对象值的 `Set()` 方法也存在类似的问题。例如，`SingingWaiter::Set()` 应该请求一次 `Worker` 信息，而不是

两次。用于 `Show()` 的相同解决方案同样适用。你可以提供仅为单个类请求信息的保护 `Get()` 方法，然后你可以将 `Get()` 方法作为构建块来组合 `Set()` 方法。

简而言之，引入带有共同祖先的多重继承（MI）需要引入虚基类、修改构造函数初始化规则，并且如果这些类在编写时没有考虑多重继承，则可能需要对它们进行修改。列表 14.10 显示了带有这些更改的类声明，列表 14.11 显示了实现。

### Listing 14.10 workeri.h

```cpp
// workeri.h
// 使用多重继承的工作类
#ifndef WORKERMI_H_
#define WORKERMI_H_
#include <string>
class Worker // 一个抽象基类
{
private:
    std::string fullname;
    long id;
protected:
    virtual void Data() const;
    virtual void Get();
public:
    Worker() : fullname("no one"), id(0) {}
    Worker(const std::string & s, long n)
        : fullname(s), id(n) {}
    virtual ~Worker() = 0; // 纯虚函数
    virtual void Set() = 0;
    virtual void Show() const = 0;
};
class Waiter : virtual public Worker
{
private:
    int panache;
protected:
    void Data() const;
    void Get();
public:
    Waiter() : Worker(), panache(0) {}
    Waiter(const std::string& s, long n, int p = 0)
        : Worker(s, n), panache(p) {}
    Waiter(const Worker & wk, int p = 0)
        : Worker(wk), panache(p) {};
    void Set();
    void Show() const;
};
class Singer : virtual public Worker
{
protected:
    enum {other, alto, contralto, soprano,
        bass, baritone, tenor};
    enum {Vtypes = 7};
    void Data() const;
    void Get() const;
private:
    static char *pv[Vtypes]; // 音域类型的字符串等
    int voice;
public:
    Singer() : Worker(), voice(other) {}
    Singer(const std::string & s, long n, int v = other)
        : Worker(s, n), voice(v) {}
    Singer(const Worker & wk, int v = other)
        : Worker(wk), voice(v) {}
    void Set();
    void Show() const;
};
// 多重继承
class SingerWaiter : public Singer, public Waiter
{
protected:
    void Data() const;
    void Get() const;
public:
    SingerWaiter() {}
    SingerWaiter(const std::string & s, long n, int p = 0,
        int v = other)
        : Worker(s,n), Waiter(s, n, p), Singer(s, n, v) {}
    SingerWaiter(const Worker & wk, int p = 0, int v = other)
        : Worker(wk), Waiter(wk,p), Singer(wk,v) {}
    SingerWaiter(const Singer & wt, int v = other)
        : Worker(wt), Waiter(wt), Singer(wt,v) {}
    SingerWaiter(const Singer & wt, int p = 0)
        : Worker(wt), Waiter(wt,p), Singer(wt) {}
    void Set();
    void Show() const;
};
#endif
```

### Listing 14.11 workeri.cpp

```cpp
// workeri.cpp
// workeri.cpp -- 使用多重继承的工作类
#include "workeri.h"
#include <iostream>
using std::cout;
using std::cin;
// Worker 方法
void Worker::Data() const
{
    cout << "Name: " << fullname << "\n";
    cout << "Employee ID: " << id << "\n";
}
void Worker::Get()
{
    cin >> fullname;
}
void Worker::Set()
{
    cout << "Enter name: ";
    cin >> fullname;
    cout << "Enter ID: ";
    cin >> id;
}
void Worker::Show() const
{
    cout << "Category: worker\n";
    Data();
}
// Waiter 方法
void Waiter::Data() const
{
    cout << "Panache rating: " << panache << "\n";
}
void Waiter::Get()
{
    cin >> panache;
}
void Waiter::Set()
{
    cout << "Enter panache: ";
    cin >> panache;
}
void Waiter::Show() const
{
    cout << "Category: waiter\n";
    Data();
}
// Singer 方法
void Singer::Data() const
{
    cout << "Vocal range: " << pv[voice] << "\n";
}
void Singer::Get() const
{
    cin >> voice;
}
void Singer::Set()
{
    cout << "Enter voice range: ";
    cin >> voice;
}
void Singer::Show() const
{
    cout << "Category: singer\n";
    Data();
}
// SingerWaiter 方法
void SingingWaiter::Data() const
{
    Singer::Data();
    Waiter::Data();
}
void SingingWaiter::Get() const
{
    // 在此示例中未使用
}
void SingingWaiter::Set()
{
    cout << "Enter name: ";
    cin >> fullname;
    cout << "Enter ID: ";
    cin >> id;
    cout << "Enter panache: ";
    cin >> panache;
    cout << "Enter voice range: ";
    cin >> voice;
}
void SingingWaiter::Show() const
{
    cout << "Category: singing waiter\n";
    Worker::Data();
    Data();
}
```

# 多重继承

```cpp
int i;
for (i = 0; i < ct; i++)
{
    cout << endl;
    lolas[i]->Show();
}
for (i = 0; i < ct; i++)
    delete lolas[i];
cout << "Bye.\n";
return 0;
```
