

```
class SingingWaiter : public Waiter, public Singer {...};
```

注意必须用关键字 `public` 限定每个基类。这是因为除非另有指示，编译器会假定为私有派生：

```
class SingingWaiter : public Waiter, Singer {...}; // Singer is a private base
```

正如本章前面所讨论的，私有和受保护的 MI 可以表达 has-a 关系；Student 类的 `student.h` 实现就是一个例子。现在我们将集中讨论公有继承。

MI 可能会给程序员带来新问题。两个主要问题是：从两个不同的基类继承同名但不同的方法，以及通过两个或更多相关的直接基类继承同一个类的多个实例。解决这些问题需要引入一些新规则和语法变体。因此，使用 MI 可能比使用单继承更困难、更容易出问题。因此，C++ 社区中的许多人强烈反对 MI；有些人希望将它从语言中移除。另一些人喜欢 MI，并认为它对特定项目非常有用，甚至必不可少。还有一些人建议谨慎、适度地使用 MI。

让我们探讨一个具体例子，看看问题和解决方案是什么。你需要几个类来创建 MI 情形。对于本例，我们将定义一个抽象的 Worker 基类，并从中派生 Waiter 类和 Singer 类。然后我们可以使用 MI 从 Waiter 和 Singer 类派生 SingingWaiter 类（见图14.3）。这是一个基类（`Worker`）通过两条独立派生路径被继承的情况，而这种情况正是给 MI 带来最多困难的情形。我们先从 Worker、Waiter 和 Singer 类的声明开始，如程序清单14.7所示。

![](img/9afc44517b591d64e2e19f623c9308ef_823_0.png)

图14.3 共享祖先的多重继承。

### 程序清单14.7 `worker0.h`

```cpp
// worker0.h -- working classes
#ifndef WORKER0_H_
#define WORKER0_H_

#include <string>

class Worker   // an abstract base class
{
private:
    std::string fullname;
    long id;
public:
    Worker() : fullname("no one"), id(0L) {}
    Worker(const std::string & s, long n)
        : fullname(s), id(n) {}
    virtual ~Worker() = 0;   // pure virtual destructor
    virtual void Set();
    virtual void Show() const;
};

class Waiter : public Worker
{
private:
    int panache;
public:
    Waiter() : Worker(), panache(0) {}
    Waiter(const std::string & s, long n, int p = 0)
        : Worker(s, n), panache(p) {}
    Waiter(const Worker & wk, int p = 0)
        : Worker(wk), panache(p) {}
    void Set();
    void Show() const;
};

class Singer : public Worker
{
protected:
    enum {other, alto, contralto, soprano,
          bass, baritone, tenor};
    enum {Vtypes = 7};
private:
    static char *pv[Vtypes];   // string equivs of voice types
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

#endif
```

程序清单14.7中的类声明包含一些表示声部类型的内部常量。枚举使 alto、contralto 等成为声部类型的符号常量，静态数组 pv 保存指向等价的 C 风格字符串的指针。如程序清单14.8所示的实现文件初始化该数组并提供方法定义。

### 程序清单14.8 worker0.cpp

```cpp
// worker0.cpp -- working class methods
#include "worker0.h"
#include <iostream>
using std::cout;
using std::cin;
using std::endl;
// Worker methods

// must implement virtual destructor, even if pure
Worker::~Worker() {}

void Worker::Set()
{
    cout << "Enter worker's name: ";
    getline(cin, fullname);
    cout << "Enter worker's ID: ";
    cin >> id;
    while (cin.get() != '\n')
        continue;
}

void Worker::Show() const
{
    cout << "Name: " << fullname << "\n";
    cout << "Employee ID: " << id << "\n";
}

// Waiter methods
void Waiter::Set()
{
    Worker::Set();
    cout << "Enter waiter's panache rating: ";
    cin >> panache;
    while (cin.get() != '\n')
        continue;
}

void Waiter::Show() const
{
    cout << "Category: waiter\n";
    Worker::Show();
    cout << "Panache rating: " << panache << "\n";
}

// Singer methods

char * Singer::pv[] = {"other", "alto", "contralto",
        "soprano", "bass", "baritone", "tenor"};

void Singer::Set()
{
    Worker::Set();
    cout << "Enter number for singer's vocal range:\n";
    int i;
    for (i = 0; i < Vtypes; i++)
    {
        cout << i << ": " << pv[i] << "   ";
        if ( i % 4 == 3)
            cout << endl;
    }
    if (i % 4 != 0)
        cout << endl;
    while (cin >> voice && (voice < 0 || voice >= Vtypes) )
        cout << "Please enter a value >= 0 and < " << Vtypes << endl;

    while (cin.get() != '\n')
        continue;
}

void Singer::Show() const
{
    cout << "Category: singer\n";
    Worker::Show();
    cout << "Vocal range: " << pv[voice] << endl;
}
```

程序清单14.9 使用多态指针数组对这些类做了一个简短测试。

### 程序清单14.9 worktest.cpp

```cpp
// worktest.cpp -- test worker class hierarchy
#include <iostream>
#include "worker0.h"
const int LIM = 4;
int main()
{
    Waiter bob("Bob Apple", 314L, 5);
    Singer bev("Beverly Hills", 522L, 3);
    Waiter w_temp;
    Singer s_temp;

    Worker * pw[LIM] = {&bob, &bev, &w_temp, &s_temp};

    int i;
    for (i = 2; i < LIM; i++)
        pw[i]->Set();
    for (i = 0; i < LIM; i++)
    {
        pw[i]->Show();
        std::cout << std::endl;
    }

    return 0;
}
```

以下是程序清单14.7、14.8和14.9中程序的输出：

```text
Enter waiter's name: Waldo Dropmaster
Enter worker's ID: 442
Enter waiter's panache rating: 3
Enter singer's name: Sylvie Sirenne
Enter worker's ID: 555
Enter number for singer's vocal range:
0: other  1: alto  2: contralto  3: soprano
4: bass   5: baritone  6: tenor
3
Category: waiter
Name: Bob Apple
Employee ID: 314
Panache rating: 5

Category: singer
Name: Beverly Hills
```

```
class Singer : public Worker { ...};
class Waiter : public Worker { ...};
class SingingWaiter : public Singer, public Waiter { ...};
```

![](img/9afc44517b591d64e2e19f623c9308ef_829_0.png)

图14.4 继承两个基类对象。

## 虚基类

虚基类使得一个由多个基类派生而来的对象只继承这些基类所共享的那个公共基类的一个对象。对于本例，你会通过在类声明中使用关键字 virtual，使 Worker 成为 Singer 和 Waiter 的虚基类（virtual 和 public 可以以任意顺序出现）：

```
class Singer : virtual public Worker { ...};
class Waiter : public virtual Worker { ...};
```

然后像之前一样定义 SingingWaiter：

```
class SingingWaiter: public Singer, public Waiter { ...};
```

现在，一个 SingingWaiter 对象将包含一份 Worker 对象的副本。本质上，继承来的 Singer 和 Waiter 对象共享一个公共的 Worker 对象，而不是各自带入自己的副本（见图14.5）。由于 SingingWaiter 现在只包含一个 Worker 子对象，你可以再次使用多态。

```
class Singer : virtual public Worker { ...};
class Waiter : virtual public Worker { ...};
class SingingWaiter : public Singer, public Waiter { ...};
```

![](img/9afc44517b591d64e2e19f623c9308ef_830_0.png)

图14.5 使用虚基类的继承。

来看看你可能会有的几个问题：

- 为什么用 *虚拟* 这个术语？
- 为什么不放弃将基类声明为 virtual，而让虚继承行为成为多重继承的常规做法呢？
- 有什么隐患吗？

首先，为什么用 virtual 这个术语？毕竟，虚函数和虚基类的概念之间似乎没有明显联系。C++ 社区强烈反对引入新关键字。例如，如果新关键字与某个大型程序中的重要函数或变量名相同，那会很别扭。所以 C++ 只是为新特性重复使用了关键字 virtual——这有点像是关键字重载。

接下来，为什么不放弃将基类声明为 virtual，而让虚继承行为成为多重继承的常规做法呢？首先，有些情况下你可能希望基类有多个副本。其次，将基类设为 virtual 要求程序做一些额外的记录工作，而如果你不需要这个特性，就不应该为此付出代价。第三，还有下一段将提到的缺点。

最后，有隐患吗？有。让虚基类正常工作需要对 C++ 规则进行调整，而且有些地方的编码方式必须不同。此外，使用虚基类可能涉及修改现有代码。例如，将 SingingWaiter 类添加到

