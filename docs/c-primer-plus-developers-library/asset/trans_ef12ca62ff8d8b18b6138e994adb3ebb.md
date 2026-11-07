
事实上，编译器不会允许你同时使用这两个 using 声明，因为这样会产生歧义。

## using 指令与 using 声明

使用 using 指令将命名空间中的所有名称整体导入，这与使用多个 using 声明并不相同。这更像是作用域解析运算符的大规模应用。当你使用 using 声明时，就好像该名称是在 using 声明的位置声明的。如果某个特定名称已经在函数中声明，则不能使用 using 声明导入相同的名称。然而，当你使用 using 指令时，名称解析会像你在同时包含 using 指令和命名空间本身的最小声明区域内声明了这些名称一样进行。对于下面的示例，该区域就是全局命名空间。如果你使用 using 指令导入一个已经在函数中声明的名称，局部名称将隐藏命名空间名称，就像它会隐藏同名的全局变量一样。但是，你仍然可以使用作用域解析运算符，如下例所示：

```cpp
namespace Jill {
    double bucket(double n) { ... }
    double fetch;
    struct Hill { ... };
}
char fetch;                 // global namespace
int main()
{
    using namespace Jill;       // import all namespace names
    Hill Thrill;                // create a type Jill::Hill structure
    double water = bucket(2);   // use Jill::bucket();
    double fetch;               // not an error; hides Jill::fetch
    cin >> fetch;               // read a value into the local fetch
    cin >> ::fetch;             // read a value into global fetch
    cin >> Jill::fetch;         // read a value into Jill::fetch
    ...
}

int foom()
{
    Hill top;                   // ERROR
    Jill::Hill crest;            // valid
}
```

在这里，main() 中，名称 Jill::fetch 被放置在局部命名空间中。它没有局部作用域，因此不会覆盖全局 fetch。但局部声明的 fetch 会同时隐藏 Jill::fetch 和全局 fetch。不过，如果你使用作用域解析运算符，后两个 fetch 变量仍然可用。你可能想将这个示例与前面使用 using 声明的示例进行比较。

相反，你应该这样使用：

```cpp
int x;
std::cin >> x;
std::cout << x << std::endl;
```

或者你可以这样使用：

```cpp
using std::cin;
using std::cout;
using std::endl;
int x;
cin >> x;
cout << x << endl;
```

你可以使用嵌套命名空间（如下一节所述）来创建一个命名空间，其中包含你常用的 using 声明。

## 更多命名空间特性

你可以嵌套命名空间声明，如下所示：

```cpp
namespace elements
{
    namespace fire
    {
        int flame;
        ...
    }
    float water;
}
```

在这种情况下，你可以通过 `elements::fire::flame` 来引用 `flame` 变量。类似地，你可以使用以下 using 指令使内部名称可用：

```cpp
using namespace elements::fire;
```

你也可以在命名空间内部使用 using 指令和 using 声明，如下所示：

```cpp
namespace myth
{
    using Jill::fetch;
    using namespace elements;
    using std::cout;
    using std::cin;
}
```

假设你想访问 `Jill::fetch`。由于 `Jill::fetch` 现在是 `myth` 命名空间的一部分，在该命名空间中它可以被称为 `fetch`，你可以这样访问它：

```cpp
std::cin >> myth::fetch;
```

当然，由于它同时也是 Jill 命名空间的一部分，你仍然可以这样调用它：

```cpp
Jill::fetch;
std::cout << Jill::fetch;  // display value read into myth::fetch
```

或者你可以这样做，前提是没有局部变量冲突：

```cpp
using namespace myth;
cin >> fetch;           // really std::cin and Jill::fetch
```

现在考虑将 using 指令应用于 myth 命名空间。using 指令是可传递的。我们说一个操作 op 是可传递的，如果 A op B 且 B op C 意味着 A op C。例如，> 运算符就是可传递的。（也就是说，A 大于 B 且 B 大于 C 意味着 A 大于 C。）在这种情况下，结果是以下语句将 myth 和 elements 命名空间都置于作用域内：

```cpp
using namespace myth;
```

这条单独的指令与以下两条指令具有相同的效果：

```cpp
using namespace myth;
using namespace elements;
```

你可以为命名空间创建别名。例如，假设你有一个命名空间定义如下：

```cpp
namespace my_very_favorite_things { ... };
```

你可以通过以下语句将 mvft 设为 my_very_favorite_things 的别名：

```cpp
namespace mvft = my_very_favorite_things;
```

你可以使用这种技术来简化对嵌套命名空间的使用：

```cpp
namespace MEF = myth::elements::fire;
using MEF::flame;
```

## 未命名命名空间

你可以通过省略命名空间名称来创建未命名命名空间：

```cpp
namespace           // unnamed namespace
{
    int ice;
    int bandycroot;
}
```

这段代码的行为就像是后面跟随了一个 using 指令；也就是说，在此命名空间中声明的名称在包含该未命名命名空间的声明区域结束之前都处于潜在作用域内。在这方面，未命名命名空间中的名称类似于全局变量。然而，如果命名空间没有名称，你就不能显式地使用 using 指令或 using 声明来使这些名称在其他地方可用。特别是，你不能在包含命名空间声明的文件之外使用未命名命名空间中的名称。这为使用具有内部链接的静态变量提供了一种替代方案。例如，假设你有以下代码：

```cpp
static int counts;   // static storage, internal linkage
int other();
int main()
{
...
}
```

```cpp
int other()
{
...
}
```

命名空间方法则是这样做：

```cpp
namespace
{
    int counts;   // static storage, internal linkage
}
int other();
int main()
{
...
}
```

```cpp
int other()
{
...
}
```

## 一个命名空间示例

让我们看一个多文件示例，它演示了命名空间的一些特性。此示例中的第一个文件（参见清单 9.11）是一个头文件，其中包含通常在头文件中出现的项目——常量、结构定义和函数原型。在本例中，这些项目被放置在两个命名空间中。第一个命名空间 pers 包含一个 Person 结构定义，以及一个用姓名填充结构的函数原型和一个显示结构内容的函数原型。第二个命名空间 debts 定义了一个结构，用于存储一个人的姓名以及欠该人的金额。该结构使用了 Person 结构，因此 debts 命名空间有一个 using 指令，使 pers 命名空间中的名称在 debts 命名空间中可用。debts 命名空间还包含一些原型。

### 清单 9.11：namesp.h

```cpp
// namesp.h
#include <string>
// create the pers and debts namespaces
namespace pers
{
    struct Person
    {
        std::string fname;
        std::string lname;
    };
    void getPerson(Person &);
    void showPerson(const Person &);

}

namespace debts
{
    using namespace pers;
    struct Debt
    {
        Person name;
        double amount;
    };
    void getDebt(Debt &);
    void showDebt(const Debt &);
    double sumDebts(const Debt ar[], int n);
}
```

### 清单 9.12：namesp.cpp

```cpp
// namesp.cpp -- namespaces
#include <iostream>
#include "namesp.h"

namespace pers
{
```

