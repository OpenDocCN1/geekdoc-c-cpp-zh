
91 到 3,951。类似地，在 1,000 次以 1 英尺步幅行走 50 英尺的试验中，平均走了 2,557 步（接近理论值 2,500），范围从 345 到 10,882。所以，如果你发现自己正在随机行走，要有信心并迈开大步。你仍然无法控制最终前进的方向，但至少可以走得更远。

## 程序说明

首先，我们注意到在程序清单 11.15 中使用 `VECTOR` 命名空间是多么轻松。下面的 `using` 声明将 `Vector` 类的名称引入作用域：

```cpp
using VECTOR::Vector;
```

由于所有 Vector 类方法都具有类作用域，因此导入类名也会使 Vector 方法可用，而无需任何进一步的 `using` 声明。

接下来，我们来谈谈随机数。标准 ANSI C 库（随 C++ 一同提供）包含一个 `rand()` 函数，它返回一个从 0 到某个与实现相关的值之间的随机整数。随机行走程序使用模运算符获取一个 0 到 359 之间的角度值。`rand()` 函数通过对初始种子值应用一种算法来获得一个随机值。该值又作为下一次函数调用的种子，依此类推。这些数字实际上是*伪随机*的，因为连续 10 次调用通常会产生同一组 10 个随机数。（具体值取决于实现。）不过，`srand()` 函数允许你覆盖默认的种子值，并开始一个不同的随机数序列。这个程序使用 `time()` 的返回值来设置种子。`time()` 函数返回当前的日历时间，通常实现为自某个特定日期以来的秒数。（更一般地，`time()` 接受一个 `time_t` 类型变量的地址，将时间放入该变量中，同时也返回它。将地址参数设为 0，就无需创建一个原本不需要的 `time_t` 变量。）因此，下面的语句每次运行程序时都会设置一个不同的种子，使随机输出看起来更加随机：

```cpp
srand(time(0));
```

`cstdlib` 头文件（以前是 `stdlib.h`）包含 `srand()` 和 `rand()` 的原型，而 `ctime`（以前是 `time.h`）包含 `time()` 的原型。（C++11 通过 random 头文件支持的函数，提供了更广泛的随机数支持。）

程序使用 result 向量来跟踪行走者的进度。在内层循环的每一轮中，程序将 step 向量设置为一个新方向，并将其加到当前的 result 向量上。当 result 的长度超过目标距离时，循环终止。

通过设置向量模式，程序以直角坐标和极坐标的形式显示最终位置。

顺便提一下，下面的语句会使 `result` 处于 RECT 模式，无论 `result` 和 `step` 的初始模式是什么：

```cpp
result = result + step;
```

原因如下。首先，加法运算符函数创建并返回一个新向量，其中包含两个参数之和。该函数通过使用默认构造函数创建该向量，默认构造函数创建的向量都处于 `RECT` 模式。因此，被赋给 `result` 的向量处于 `RECT` 模式。默认情况下，赋值会逐个成员地赋给每个成员变量，所以 `RECT` 被赋给了 `result.mode`。如果你希望有其他行为，比如让 `result` 保持其原始模式，可以通过为类定义赋值运算符来覆盖默认赋值。第 12 章展示了这方面的示例。

顺便说一下，将连续的位置保存到文件中是一件简单的事。首先，包含 `<fstream>`，声明一个 ofstream 对象，并将该对象与文件关联：

```cpp
#include <fstream>
...
ofstream fout;
fout.open("thewalk.txt");
```

然后，在计算结果的循环中，插入类似下面的代码：

```cpp
fout << result << endl;
```

这会调用友元函数 `operator<<(fout, result)`，使 `os` 引用参数指向 `fout`，从而将输出发送到文件。你也可以使用 `fout` 将其他信息写入文件，比如当前由 `cout` 显示的摘要信息。

## 类的自动转换和类型强制转换

关于类的下一个主题是类型转换。我们将探讨 C++ 如何处理与用户自定义类型之间的转换。为了铺垫，我们先回顾一下 C++ 如何处理其内置类型的转换。当你编写一条将一个标准类型的值赋给另一个标准类型的变量的语句时，如果这两个类型兼容，C++ 会自动将该值转换为接收变量的类型。例如，下面的语句都会产生数值类型转换：

```cpp
long count = 8;      // int value 8 converted to type long
double time = 11;    // int value 11 converted to type double
int side = 3.33;     // double value 3.33 converted to type int
```

这些赋值之所以可行，是因为 C++ 认识到各种数值类型都表示同一个基本事物——数字——并且 C++ 内置了进行转换的规则。不过，回想一下第 3 章“处理数据”中的内容，在这些转换中你可能会损失一些精度。例如，将 `3.33` 赋给 `int` 变量 `side` 后，`side` 得到的值是 3，丢失了 `0.33` 这部分。

C++ 不会自动转换不兼容的类型。例如，下面的语句会失败，因为左边是指针类型，而右边是数字：

```cpp
int * p = 10;  // type clash
```

注意，Stonewt 类有三个构造函数。它们允许你将 Stonewt 对象初始化为一个以浮点数表示的磅数，或者初始化为英石和磅的组合。你也可以创建一个不进行初始化的 Stonewt 对象：

```cpp
Stonewt blossem(132.5);       // weight = 132.5 pounds
Stonewt buttercup(10, 2);     // weight = 10 stone, 2 pounds
Stonewt bubbles;              // weight = default value
```

这个类实际上并不需要声明析构函数，因为自动默认析构函数对于这种情况已经足够。另一方面，提供显式声明可以让你为将来做好准备，那时你将必须定义析构函数。

此外，Stonewt 类提供了两个显示函数。一个以磅为单位显示重量，另一个以英石和磅为单位显示重量。程序清单 11.17 展示了这些类方法的实现。注意，每个构造函数都会给所有三个私有成员赋值。因此，创建 Stonewt 对象会自动设置两种重量表示。

### 程序清单 11.17 stonewt.cpp

```cpp
// stonewt.cpp -- Stonewt methods
#include <iostream>
using std::cout;
#include "stonewt.h"

// construct Stonewt object from double value
Stonewt::Stonewt(double lbs)
{
    stone = int (lbs) / Lbs_per_stn;    // integer division
    pds_left = int (lbs) % Lbs_per_stn + lbs - int(lbs);
    pounds = lbs;
}

// construct Stonewt object from stone, double values
Stonewt::Stonewt(int stn, double lbs)
{
    stone = stn;
    pds_left = lbs;
    pounds = stn * Lbs_per_stn +lbs;
}

Stonewt::Stonewt()          // default constructor, wt = 0
{
    stone = pounds = pds_left = 0;
}

Stonewt::~Stonewt()         // destructor
{
}

// show weight in stones
void Stonewt::show_stn() const
{
    cout << stone << " stone, " << pds_left << " pounds\n";
}

// show weight in pounds
void Stonewt::show_lbs() const
{
    cout << pounds << " pounds\n";
}
```

因为 Stonewt 对象表示一个单独的重量，所以提供将整数或浮点值转换为 Stonewt 对象的方法是合理的。你已经做到了！在 C++ 中，任何只接受一个参数的构造函数都可以作为将该参数类型转换为类类型的蓝图。因此，下面的构造函数可以作为将 double 类型值转换为 Stonewt 类型值的指令：

```cpp
Stonewt(double lbs);  // template for double-to-Stonewt conversion
```

也就是说，你可以编写如下代码：

```cpp
Stonewt myCat;       // create a Stonewt object
myCat = 19.6;        // use Stonewt(double) to convert 19.6 to Stonewt
```

程序使用 Stonewt(double) 构造函数来构造一个临时 Stonewt 对象，并使用 19.6 作为初始化值。然后，逐成员赋值将临时对象的内容复制到 myCat 中。这个过程被称为*隐式转换*，因为它是自动发生的，不需要显式类型强制转换。

只有可以只用一个参数调用的构造函数才能作为转换函数。下面的构造函数有两个参数，因此它不能用于转换类型：

```cpp
Stonewt(int stn, double lbs);  // not a conversion function
```

但是，如果它为第二个参数提供默认值，就可以作为 int 转换的指南：

```cpp
Stonewt(int stn, double lbs = 0);  // int-to-Stonewt conversion
```

让构造函数作为自动类型转换函数似乎是一个很好的特性。然而，随着程序员在使用 C++ 的过程中积累了更多经验，他们发现自动转换这一特性并不总是理想的，因为它可能导致意外的转换。因此，C++ 增加了一个新关键字 `explicit` 来关闭这种自动转换。也就是说，你可以这样声明构造函数：

```cpp
explicit Stonewt(double lbs);  // no implicit conversions allowed
```

这会禁用类似前面示例中的隐式转换，但仍允许显式转换——即使用显式类型强制转换的转换：
