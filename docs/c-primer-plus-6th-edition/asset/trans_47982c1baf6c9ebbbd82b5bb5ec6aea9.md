

# 第 9 章内存模型与命名空间

文件（`extern` 使用时不进行初始化）。定义在任何函数之外但用 `static` 关键字修饰的变量具有文件作用域，但对其他文件不可（内部链接）。定义在块内部并用 `static` 关键字修饰的变量是该块局部的（局部作用域，无链接），在程序运行期间保留其值。

默认情况下，C++ 函数具有外部链接，因此它们可以在文件之间共享。用 `static` 关键字修饰的函数具有内部链接，并被限制在定义文件中。

使用 `new` 和 `delete` 进行动态内存分配和释放，使用空存储器（或堆）来存储数据。当调用 `new` 时分配内存，当调用 `delete` 时释放内存。程序使用指针来跟踪这些内存位置。

命名空间允许你定义可以在其中声明标识符的区域。其意图是减少命名冲突，特别是在使用来自多个供应商代码的大型程序。你可以通过使用作用域解析符、使用声明或使用指令来使用命名空间中的标识符。

# 本章总结

- 1. 针对以下情况，你会使用哪种存储方案？
  a. `homer` 是函数的正式参数（参数）。
  b. 变量 `secret` 需要被两个文件共享。
  c. 变量 `topsecret` 需要被一个文件中的函数共享，对其他文件隐藏。
  d. `beencalled` 用于跟踪包含它的函数被调用次数。

- 2. 描述 `using` 声明（using declaration）和 `using` 指令（using directive）之间的区别。

- 3. 重写以下代码，使其不使用 `using` 声明或 `using` 指令：

```cpp
#include <iostream>
using namespace std;
int main()
{
    double x;
    cout << "Enter value: ";
    while (!cin >> x)
    {
        cout << "Bad input. Please enter a number: ";
        cin.clear();
        while (cin.get() != '\n')
            continue;
    }
}
```

```cpp
}
cout << "Value = " << x << endl;
return 0;
}
```

- 4. 重写以下代码，使其使用 `using` 声明而不是 `using` 指令：

```cpp
#include <iostream>
using namespace std;
int main()
{
    double x;
    cout << "Enter value: ";
    while (! cin >> x) {
        cout << "Bad input. Please enter a number: ";
        cin.clear();
        while (cin.get() != '\n')
            continue;
    }
    cout << "Value = " << x << endl;
    return 0;
}
```

- 5. 假设你希望 `average(3,6)` 函数在一个文件中被调用时返回两个参数的 `int` 类型平均值，而在程序的第二个文件中被调用时，返回两个 `int` 参数的 `double` 类型平均值。你应该如何设置？

- 6. 以下两个文件的程序将显示什么？

```cpp
// file.cpp
#include <iostream>
using namespace std;
void other();
void another();
int x = 10;
int y;

int main()
{
    cout << x << endl;
    {
        int x = 4;
        cout << x << endl;
        cout << y << endl;
    }
}
other();
another();
return 0;
}
```

```cpp
void other() {
    int y = 1;
    cout << "Other: " << x << ", " << y << endl;
}
```

```cpp
// file 2.cpp
#include <iostream>
using namespace std;
extern int x;
namespace {
    int y = -4;
}
```

```cpp
void another() {
    cout << "another(): " << x << ", " << y << endl;
}
```

- 7. 以下程序将显示什么？

```cpp
#include <iostream>
using namespace std;
void other()
namespace n1 {
    int x = 1;
}

namespace n2 {
    int x = 2;
}

int main() {
    using namespace n1;
    cout << x << endl;
}

int x = 4;
cout << x << ", " << n1::x << " " << n2::x << endl;
}
using n2::x;
cout << x << endl;
other();
return 0;
}
```

```cpp
void other()
{
using namespace n2;
cout << x << endl;
{
int x = 4;
cout << x << ", " << n1::x << " " << n2::x << endl;
}
using n2::x;
cout << x << endl;
}
```

# 编程练习

- 1. 这是一个头文件：
// golf.h -- 用于 pe9-1.cpp

```cpp
const int Len = 40;
struct golf
{
char fullname[Len];
int handicap;
};
```

> // 非交互式版本：
// 函数将 golf 结构体设置为提供的名称、让杆分
// 使用传递给函数的参数
void setgolf(golf &g, const char * name, int hc);

> // 交互式版本：
// 函数向用户请求名称和让杆分
// 并 g 的成员设置为这些值

- 2. 重做列表 9.9，将字符数组替换为字符串。程序不再需要检查输入。

- 3. 以以下结构开始：

```cpp
struct chaff
{
    char dross[20];
    int slag;
};
```
编写一个使用放置 new（placement new）在缓冲区中此类结构数组的程序。然后为结构成员赋值（记得对字符数组使用 `strcpy()`）并使用循环显示。选项 1 使用静态数组（类似于 9.10）作为缓冲区。选项 2 使用 `new` 分配缓冲区。

- 4. 根据以下命名空间编写三文件程序：

```cpp
namespace SALES
{
    const int QUARTERS = 4;
    struct Sales
    {
        double sales[QUARTERS];
        double average;
        double max;
        double min;
    }; // 将数组中少于 4 的 n 个项目拷贝到 sales 成员中并计算并存储平均值、最大值最小值；s 的剩余元素（如果有）设置为 0
void setSales(Sales &s, const double ar[], int n);
// 交互式收集 4 季度的销售情况，将其存储在 s 成员中并计算并存储
// 平均值、最大值和最小值
void setSales(Sales &s);
// 显示结构 s 中的所有信息
void showSales(const Sales &s);
}
```

第一个文件应该是包含命名空间的头文件。第二个文件应该是扩展命名空间的源代码，为原型函数提供定义。第三文件文件声明两个 Sales 对象。它应该使用交互版本的 `setSales()` 为一个结构提供值，使用非交互版本的 `setSales()` 为第二个结构提供值。它应该通过 `showSales()` 显示两个结构的内容。

# 对象与类

在本章中你将学习：

- 过程化与面向对象的编程
- 类的概念
- 如何定义和实现类
- 公有和私有类访问
- 类数据成员
- 类方法（类函数成员）
- 创建和使用类对象
- 类构造函数和析构函数
- const 成员函数
- this 指针
- 对象数组
- 类作用域
- 抽象数据类型

面向对象编程（OOP）是一种特定的设计程序的概念方法，C++ 增强了 C 的特性，有助于应用该方法。以下是最重要的 OOP 特性：

- 抽象
- 封装和数据隐藏
- 多态
- 继承
- 代码复用

