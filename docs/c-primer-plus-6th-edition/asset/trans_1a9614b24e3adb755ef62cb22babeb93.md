

## 第14 章 在 C++ 中重用代码

SingingWaiter::Show() 方法可以将这些组件组合在一起。例如，你可以这样使用：

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

同样，其他的 Show() 方法也将由适当的 Data() 组件构建。
通过这种方法，对象仍然会公使用 Show() 方法。另一方面，Data() 方法应该是类的内部方法；它们应该是用于辅助公共接口的帮助方法。然而，将 Data() 方法设为私有将防止（例如）Waiter 代码使用 Worker::Data()。这就是受保护访问类类的用处。如果 Data() 方法是受保护的，它们可以在层次结构中的所有类中内部使用，同时对外部世界隐藏。

另一种方法是将所有的数据组件设为私有，但使用受保护方法而不是受保护数据，可以对数据的允许访问进行更严格的控制。
请求数据以设置对象值的 Set() 方法也存在类似的问题。例如，SingingWaiter::Set() 应该请求一次 Worker 信息，而不是

# 多重继承

两次。用于 Show() 的相同解决方案同样适用。你可以提供仅为单个类请求信息的保护 Get() 方法，然后你可以将 Get() 方法作为构建块来组合 Set() 方法。

简而言之，引入带有共同祖先的多重继承（MI）需要引入虚基类、修改构造函数初始化规则，并且如果这些类在编写时没有考虑多重继承，则可能需要对它们进行修改。列表 14.10 显示了带有这些更改的类声明，列表 14.11 显示了实现。

Listing 14.10 workeri.h

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

Listing 14.11 workeri.cpp

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

