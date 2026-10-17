
类型转换显式将 `stu` 转换为字符串引用；该类型反过来调用 `operator<<(ostream&, const String&)` 函数。引用不会自动转换为 `string` 引用。根本原因是，对于私有继承，在没有显式类型转换的情况下，基类的引用或指针无法赋值给派生类。

然而，即使示例使用公共继承，也必须使用显式类型转换。一个原因是，如果没有类型代码，像如下的操作会匹配友元函数原型，导致递归调用：

```cpp
os << stu;
```

第二个原因是该类使用了 MI，如果两个基类恰好都提供了 `operator<<()` 函数，编译器将不知道转换为哪一个基类。列表 14.5 显示了 `Student` 类的所有方法，除了类声明中内联的方法。

# 列表 14.5 student.cpp

```cpp
// student.cpp -- 使用私有继承的 Student 类
#include "student.h"
using std::ostream;
using std::endl;
using std::istream;
using std::string;
// 公有方法
double Student::Average() const
{
    if (ArrayDb::size() > 0)
        return ArrayDb::sum()/(ArrayDb::size());
    else
        return 0;
}
const string & Student::Name() const
{
    return (const string &)*this;
}
double & Student::operator[](int i)
{
    return ArrayDb::operator[](i);    // 使用 ArrayDb::operator[](i)
}
```

```cpp
double Student::operator[](int i) const
{
    return ArrayDb::operator[](i);
}
```

```cpp
// 私有方法
ostream & Student::arr_out(ostream & os) const
{
    int i;
    int lim = ArrayDb::size();
    if (lim > 0) {
        for (i = 0; i < lim; i++) {
            os << ArrayDb::operator[](i) << " ";
            if (i % 5 == 4)
                os << endl;
        }
        if (i % 5 != 0)
            os << endl;
    } else {
        os << " empty array ";
        return os;
    }
}
```

```cpp
// 友元
// 使用 string 版本的 operator>>
istream & operator>>(istream & is, Student & stu)
{
    is >> (string &)stu;
    return is;
}
```

```cpp
// 使用 string  friend getline(ostream &, const string &)
istream & getline(istream & is, Student & stu)
{
    getline(is, (string &)stu);
    return is;
}
```

```cpp
// 使用 string 版本的 operator<<(ostream & os, const Student & stu)
{
    os << "Scores for " << (const string &)stu << ":\n";
    stu.arr_out(os); // 使用私有方法输出分数
    return os;
}
```

再次，由于示例复用了 `string` 和 `valarray` 的代码，除了私有辅助方法外，还需要一些较新的代码。

## 使用修改后的 Student 类

再次，是时候测试新类了。注意，`Student` 类的两个版本具有完全相同的公共接口，因此你可以用相同的程序测试这两个版本。唯一的区别是，你必须包含 `student.i` 而不是 `student.h`，并且链接程序时需要使用 `studenti.cpp` 而不是 `student.cpp`。列表 14.6 显示了该程序。确保将其与 `student.cpp` 一起编译。

# 列表 14.6 use_stui.cpp

```cpp
// use_stui.cpp -- 使用带有私有继承的类
// 使用 studenti.cpp 编译
#include <iostream>
#include "studenti.h"
using std::cin;
using std::cout;
using std::endl;
void set(Student & sa, int n);
const int pupils = 3;
const int quizzes = 5;
int main()
{
    Student ada[pupils] =
    {Student(quizzes), Student(quizzes), Student(quizzes)};
    int i;
    for (i = 0; i < pupils; i++)
        set(ada[i], quizzes);
    cout << "\nStudent List:\n";
    for (i = 0; i < pupils; i++)
        cout << ada[i].Name << endl;
    cout << "\nResults:\n";
    for (i = 0; i < pupils; i++)
        {
            cout << endl << ada[i];
            cout << "  average: " << ada[i].Average() << endl;
        }
    cout << "  Done.\n";
    return 0;
}
```

```cpp
void set(Student & sa, int n)
{
    cout << "Please enter the student's name: ";
    getline(cin, sa);
    cout << "Please enter " << n << " quiz scores:\n";
    for (int i = 0; i < n; i++)
        cin >> sa(i);
        while (cin.get() != '\n')
            continue;
    }
}
```

以下是列表 14.6 程序的运行示例：

Please enter the student's name: Gil Bays
Please enter 5 quiz scores:
Please enter the student's name: Ada Love
Please enter 5 quiz scores:
Please enter the student's name: B Gates
Please enter 5 quiz scores:

Student List:
Gil Bays
Ada Love
B Gates

Results:

  average: 85
  average: 90
  average: 75

  Done.

`Student` 类。在这种情况下，在 `student.h` 中，你可以向 public 部分添加 `using` 声明：

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    using std::valarray<double>::min;
    using std::valarray<double>::max;
    ...
};
```

`using` 声明使得 `valarray<double>::min()` 和 `valarray<double>::max()` 方法像它们是 `Student` 的公共方法一样可用：
out << "high score: " << ada[i] << endl;

请注意，`using` 声明使用的是成员名——没有括号、没有函数签名、没有返回类型。例如，为了让 `valarray operator[]` 方法对 `Student` 类可用，你可以在 `Student` 类定义的 public 部分放置以下 `using` 声明：

```cpp
using std::valarray<double>::operator();
```

这将使得两个版本（const 和非 const）都可用。然后，你可以移除现有的 `Student::operator()` 的原型声明和定义。`using` 声明方法仅适用于继承，不适用于包含。

在私有派生类中重新声明基类方法有一种旧方法：你将方法名放在派生类的 public 部分。以下是实现方法：

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    std::valarray<double>::operator[](); // 重新声明为公共，仅使用名称
    ...
};
```

这看起来像是一个没有 `using` 关键字的 `using` 声明。这种方法已经过弃（deprecated），意味着其意图是将其逐渐淘汰。因此，如果你的编译器支持 `using` 声明，你可以使用它来让来自私有基类的方法对派生类可用。

# 多重继承 (Multiple Inheritance)

MI 描述了一个具有多个直接基类的类。与单重继承一样，公共多重继承 应该表达一种“是一种”（is-a）的关系。例如，如果你有一个 `Waiter` 类和一个 `Singer` 类，你可以从它们派生出一个 `SingingWaiter` 类：

```cpp
class SingingWaiter : public Waiter, public Singer {...};
```

注意，你必须用 `public` 关键字限定每个基类。这是因为编译器除非指示说明，否则假设为私有派生：

```cpp
class SingingWaiter : public Waiter, Singer {...}; // Singer 是私有基类
```

正如本章之前讨论的，私有和保护的 MI 可以表达一种“有一个”（has-a）的关系；`Student` 类的实现就是一个例子。我们现在重点关注公共继承。

MI 会给程序员带来新问题。两个主要问题是从两个基类继承具有相同名的不同方法，以及通过两个或多个相关的基类继承同一个类的多个实例。解决这些问题涉及引入一些新规则和语法变体。因此，使用 MI 比使用单重继承更困难，且更容易出错。由于这个原因，C++ 社区的许多人强烈反对 MI；一些人希望将其从语言中移除。另一些人建议使用 MI 并认为它对特定项目非常有用，甚至是必要的。还有人建议谨慎且适度地使用 MI。

让我们探索一个特定的示例，看看问题和解决方案。你需要几个类来创建一个 MI 场景。对于这个示例，我们定义了一个抽象基类 `Worker`，并从它派生出 `Waiter` 类和 `Singer` 类。然后我们可以使用 MI 从 `Waiter` 和 `Singer` 类派生出一个 `SingingWaiter` 类（见图 14.3）。这是一个基类（Worker）通过两个单独派生被继承的情况，这是导致 MI 产生最大困难的情况。我们从 `Worker`、`Waiter` 和 `Singer` 类的声明开始，如列表 14.7 所示。

![](img/cd111a87c1db9aff4db4b18834327463_823_0.png)

图 14.3 共享祖先的 MI。

# 810 第14 章在 C++ 中重用代码

# 列表 14.7 worker0.h

```cpp
// worker0.h -- 工作类
#ifndef WORKER0_H_
#define WORKER0_H_
#include <string>
class Worker // 一个抽象基类
{
private:
    std::string fullname;
    long id;
public:
    Worker() : fullname("no one
```

```cpp
Singer(const std::string &s, long n, int v = other)
    : Worker(s, n), voice(v) {}
Singer(const Worker &wk, int v = other)
    : Worker(wk), voice(v) {}
void Set();
void Show() const;
#endif
```

列表 14.7 中的类声明包含了一些表示声部的内部常量。枚举为声部类型提供了 alto、centralto 等符号常量，静态数组 `pv` 持有指向 C 风格字符串等值的指针。列表 14.8 所示的实现文件初始化了这个数组并提供了方法定义。

# 列表 14.8 worker0.cpp

```cpp
// worker0.cpp -- 工作类方法
#include "worker0.h"
#include <iostream>
using std::cout;
using std::cin;
using std::endl;
// Worker 方法
// 必须实现虚析构函数，即使是纯虚
Worker::Worker() {}
void Worker::Set()
{
    cout << "Enter worker's name: ";
    getline(cin, fullname);
    cout << "Enter worker's ID: ";
```

[PAGE 826]
# 812 第14 章在 C++ 中重用代码

```cpp
    cout << "Enter worker's ID: ";
    cout << "Enter worker's name: ";
    getline(cin, fullname);
    cout << "Enter worker's ID: ";
```
