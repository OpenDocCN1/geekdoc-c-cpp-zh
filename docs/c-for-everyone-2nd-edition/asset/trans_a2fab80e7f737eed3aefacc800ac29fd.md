

![](img/23fb3582e93ebc95909e1de029c3d388_443_0.png)

### 自我检查

- 29. 寻找类的经验法则是什么？
- 30. 你要编写一个下棋的程序。`ChessBoard` 可能是一个合适的类吗？`MovePiece` 呢？
- 31. 在电子邮件系统中，消息存储在邮箱中。绘制一个 UML 图，显示适当的聚合关系。
- 32. 你正在实现一个管理图书馆的系统，跟踪哪些书被谁借出。`Book` 类应该聚合 `Patron`，还是反过来？
- 33. 在图书馆管理系统中，`Patron` 类和 `Author` 类之间的关系会是什么？

**动手练习** 现在你可以尝试本章末尾的这些练习：R9.23、R9.24、R9.26。

### 编程提示 9.3：将并行向量改为对象向量

![](img/23fb3582e93ebc95909e1de029c3d388_443_1.png)

有时，你会发现自己使用长度相同的多个向量，每个向量存储的只是概念上应该属于一个对象的一部分内容。在这种情况下，最好重新组织程序，使用一个元素为对象的单一向量。

例如，假设一张发票包含一系列商品描述和价格。一种解决方案是维护两个向量：

```cpp
vector<string> descriptions;
vector<double> prices;
```

每个向量的长度都相同，由 `descriptions[i]` 和 `prices[i]` 组成的*第 i 个切片*包含需要一起处理的数据。这些向量称为**并行向量**（见图 5）。

在较大的程序中，并行向量会变得令人头疼。程序员必须确保这些向量始终具有相同的长度，并且每个切片中填充的值确实属于一起。此外，任何对切片进行操作的函数都必须将所有向量作为参数接收，这在编程时很繁琐。

解决办法很简单。查看切片并找出它所代表的*概念*。然后将该概念做成一个类。在这个例子中，每个切片包含一个*商品*的描述和价格；将其转换为一个类。

> 通过将并行向量改为对象向量来避免并行向量。

```cpp
class Item
{
public:

private:
   string description;
   double price;
};
```

![](img/23fb3582e93ebc95909e1de029c3d388_443_2.png)

**图 5** 并行向量

![](img/23fb3582e93ebc95909e1de029c3d388_444_0.png)

**图 6** 消除并行向量

现在可以消除这些并行向量，并用一个单一向量替换它们：

```cpp
vector<Item> items;
```

结果向量中的每个槽位对应于这组并行向量中的一个切片（见图 6）。

## 9.8 分离编译

复杂程序的代码分布在多个文件中。

当你编写并编译小程序时，可以将所有代码放在一个源文件中。当程序变大或在团队中工作时，情况就会发生变化。你会希望将代码拆分成独立的源文件。这种拆分变得必要有两个原因。首先，编译文件需要时间，而等待编译器不断翻译没有变化的代码似乎很愚蠢。如果你的代码分布在多个源文件中，那么只有你更改过的文件才需要重新编译。第二个原因在团队中与其他程序员一起工作时会变得明显。多个程序员同时编辑一个源文件会非常困难。因此，程序代码被拆分，以便每个程序员单独负责一组独立的文件。

如果你的程序由多个文件组成，其中一些文件会定义其他文件所需的数据类型或函数。文件之间必须有一条通信路径。在 C++ 中，这种通信通过包含头文件来实现。

头文件包含

- 类的定义。
- 常量的定义。
- 非成员函数的声明。

头文件包含类的定义和非成员函数的声明。

注意包围头文件的这组指令：

```cpp
#ifndef CASHREGISTER_H
#define CASHREGISTER_H

#endif
```

假设一个文件包含两个头文件：cashregister.h，以及另一个自身也包含 cashregister.h 的头文件。这些指令的作用是，当第二次遇到该文件时跳过它。如果没有这个检查，编译器在看到 CashRegister 类的定义两次时会报错。（遗憾的是，它并不检查这些定义是否完全相同。）

CashRegister 类的源文件只包含成员函数（包括构造函数）的定义。

注意，源文件 cashregister.cpp 包含它自己的头文件 cashregister.h。编译器需要知道 CashRegister 类是如何定义的，以便编译成员函数。

**ch09/cashregister.cpp**

```cpp
#include "cashregister.h"

CashRegister::CashRegister()
{
   clear();
}

void CashRegister::clear()
{
   item_count = 0;
   total_price = 0;
}

void CashRegister::add_item(double price)
{
   item_count++;
   total_price = total_price + price;
}

double CashRegister::get_total() const
{
   return total_price;
}

int CashRegister::get_count() const
{
   return item_count;
}
```

注意，函数注释位于头文件中，因为注释是接口的一部分，而不是实现的一部分。

cashregister.cpp 文件不包含 *main* 函数。有许多潜在的程序可能会使用 CashRegister 类。这些程序中的每一个都需要提供自己的 *main* 函数，以及其他函数和类。

下面是一个使用 CashRegister 类的简单测试程序。它的源文件包含 cashregister.h 头文件。

**ch09/registertest2.cpp**

```cpp
#include <iostream>
#include <iomanip>
#include "cashregister.h"

using namespace std;

/**
    Displays the item count and total price of a cash register.
    @param reg the cash register to display
*/
void display(CashRegister reg)
{
    cout << reg.get_count() << " $" << fixed << setprecision(2)
         << reg.get_total() << endl;
}

int main()
{
    CashRegister register1;
    register1.clear();
    register1.add_item(1.95);
    display(register1);
    register1.add_item(0.95);
    display(register1);
    register1.add_item(2.50);
    display(register1);
    return 0;
}
```

要构建完整程序，需要同时编译 registertest2.cpp 和 cashregister.cpp 源文件（见图 7）。具体细节取决于你的编译器。例如，使用 GNU 编译器时，可以执行以下命令

```bash
g++ -o registertest registertest2.cpp cashregister.cpp
```

![](img/23fb3582e93ebc95909e1de029c3d388_447_0.png)

你刚刚看到了设计头文件和源文件的最简单、最常见的情况。还有一些额外的技术细节你应该知道。

- 头文件应包含定义该类所需的所有头文件。例如，如果某个类使用了 string 类，也要包含 `<string>` 头文件。每当包含标准库中的头文件时，还要包含 `using namespace std;` 指令。

**item.h**

```cpp
#include <string>
using namespace std;

class Item
{
    ...
private:
    string description;
};
```

- 将共享常量放入头文件中。例如，

**volumes.h**

```cpp
const double CAN_VOLUME = 0.355;
```

- 要共享非成员函数，请将函数声明放入头文件，并将函数定义放入对应的源文件。

**cube.h**

```cpp
double cube_volume(double side_length);
```

**cube.cpp**

```cpp
#include "cube.h"

double cube_volume(double side_length)
{
    double volume = side_length * side_length * side_length;
    return volume;
}
```

![](img/23fb3582e93ebc95909e1de029c3d388_448_0.png)

### 自我检查

- 34. 假设收银机被增强为可以从银行账户直接扣款，并且向 CashRegister 类添加了一个成员函数声明 `BankAccount()`。你需要在 `cashregister.h` 中包含哪个头文件？
- 35. 在自我检查 34 描述的增强中，你需要在 `cashregister.cpp` 中包含哪个额外文件？
- 36. 在自我检查 34 描述的增强中，你需要在 `bankaccount.h` 文件中包含哪个额外文件？
- 37. 假设我们想将 display 函数从 `registertest2.cpp` 移到 `cashregister.h` 和 `cashregister.cpp` 文件中。解释这些文件需要如何更改。
- 38. 使用 `#include <iostream>` 指令包含的头文件位于哪里？

### 动手练习

现在你可以尝试本章末尾的这些练习：R9.28、R9.29、P9.20。

