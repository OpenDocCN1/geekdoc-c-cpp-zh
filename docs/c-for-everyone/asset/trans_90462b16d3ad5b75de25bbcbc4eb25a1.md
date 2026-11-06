

![](img/5e58fb4c840712efd6ed6fa82bb97f57_426_0.png)

当在一个对象上调用成员函数时，**隐式参数**是对该对象的引用。

你可以这样理解 `add_item` 函数的代码：

```cpp
void CashRegister::add_item(double price)
{
    implicit parameter.item_count++;
    implicit parameter.total_price = implicit parameter.total_price + price;
}
```

> 隐式参数是对应用成员函数的那个对象的引用。

在 C++ 中，你实际上并不会在函数定义中写出隐式参数。因此，这个参数被称为“隐式”的。相反，在函数定义中显式提及的参数变量，例如 `price` 参数变量，被称为**显式参数**。每个成员函数恰好有一个隐式参数，以及零个或多个显式参数。

> 成员函数的显式参数在函数定义中列出。

### 9.4.3 从成员函数中调用成员函数

> 在同一对象上调用另一个成员函数时，不要使用点号表示法。

当一个成员函数在*同一个对象*上调用另一个成员函数时，你不使用点号表示法。相反，你只需要使用另一个函数的名称。下面是一个例子。假设我们要实现一个成员函数，用于添加同一商品的多个数量。实现这个函数的一种简单方法是反复调用 `add_item` 函数：

```cpp
void CashRegister::add_items(int quantity, double price)
{
    for (int i = 1; i <= quantity; i++)
    {
        add_item(price);
    }
}
```

在这里，`add_item` 成员函数是在隐式参数上被调用的。

```cpp
for (int i = 1; i <= quantity; i++)
{
    implicit parameter.add_item(price);
}
```

这个隐式参数就是 `add_items` 函数被调用的那个对象。例如，在调用 `register1.add_items(6, 0.95);` 中，`add_item` 函数会在 `register1` 上被调用六次。

### 语法 9.2 成员函数定义

![](img/5e58fb4c840712efd6ed6fa82bb97f57_427_0.png)

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

/**
    A simulated cash register that tracks the item count and
    the total amount due.
*/
class CashRegister
{
public:
    /**
        Clears the item count and the total.
    */
    void clear();
```

```cpp
77    register1.add_item(0.95);
78    display(register1);
79    register1.add_item(2.50);
80    display(register1);
81    return 0;
82 }
```

### 程序运行

|  |  |
|---|---|
| 1 | $1.95 |
| 2 | $2.90 |
| 3 | $5.40 |

![](img/5e58fb4c840712efd6ed6fa82bb97f57_429_0.png)

- 15. `get_total` 成员函数的这种实现有什么问题？
  ```cpp
  int get_total()
  {
      return total_price;
  }
  ```
- 16. 在不调用 `add_item` 的情况下，实现第 9.4.3 节中描述的 `add_items` 成员函数。
- 17. 为 `CashRegister` 类实现一个成员函数 `get_dollars`，该函数以美元数值（不含美分）的形式返回销售总金额。
- 18. 考虑 `string` 类的 `substr` 成员函数。它有多少个参数，这些参数的类型是什么？
- 19. 考虑 `string` 类的 `length` 成员函数。它有多少个参数，这些参数的类型是什么？

**练习** 现在你可以尝试本章末尾的这些练习：P9.3、P9.4、P9.6。

### 编程提示 9.1 所有数据成员都应为私有；大多数成员函数应为公有

![](img/5e58fb4c840712efd6ed6fa82bb97f57_429_1.png)

在类的公有部分定义数据成员是可能的，但你不应该在代码中这样做。始终使用封装，将数据成员设为私有，并通过成员函数对其进行操作。

通常，成员函数应该是公有的。但是，有时你有一个成员函数仅用作其他成员函数的辅助函数。在这种情况下，你可以将辅助函数设为私有。只需在类的私有部分声明它即可。

### 编程提示 9.2 const 正确性

![](img/5e58fb4c840712efd6ed6fa82bb97f57_429_2.png)

你应该在 C++ 中使用 const 保留字声明所有访问器函数。（回顾一下，访问器函数是不修改其隐式参数的成员函数。）

例如，假设你设计了以下类：

```cpp
class CashRegister
{
    void display(); // 糟糕的风格——没有 const
    ...
};
```

当你编译代码时，不会报错。但现在假设另一个程序员在某个函数中使用了你的 `CashRegister` 类：

```cpp
void display_all(const CashRegister registers[])
{
    for (int i = 0; i < NREGISTERS; i++) { registers[i].display(); }
}
```

那位程序员很认真，将 `registers` 参数变量声明为 const。但随后 `registers[i].display()` 的调用将无法编译。因为 `CashRegister::display` 未标记为 const，编译器怀疑调用 `registers[i].display()` 可能会修改 `registers[i]`。但该函数承诺不会修改 `registers` 数组。

如果你与团队中其他对 const 很认真的成员一起编写程序，那么你也必须做好自己的部分。因此，你应该养成在所有访问器成员函数中使用 const 的习惯。

## 9.5 构造函数

> 每当创建对象时，构造函数会被自动调用。

**构造函数**（constructor）是初始化对象数据成员的成员函数。每当创建对象时，构造函数会被自动调用。通过提供构造函数，你可以确保在任何成员函数作用于对象之前，所有数据成员都已正确设置。

为了理解构造函数的重要性，请考虑以下语句：

```cpp
CashRegister register1;
register1.add_item(1.95);
int count = register1.get_count();  // 可能不是 1
```

这里，程序员在添加商品之前忘记调用 `clear`。因此，`register1` 对象的数据成员被随机值初始化。构造函数保证了对象在定义时总是被完全初始化。

> 构造函数的名称与类名相同。

构造函数的名称与其类名完全相同。你在类定义中声明构造函数，例如：

```cpp
class CashRegister
{
public:
    CashRegister();  // 一个构造函数
    ...
};
```

构造函数从不返回值，但你不需要在声明它们时使用 void 保留字。

下面是该构造函数的定义：

```cpp
CashRegister::CashRegister()
{
    item_count = 0;
    total_price = 0;
}
```

在构造函数定义中，第一个 `CashRegister`（在 `::` 之前）表示我们将要定义 `CashRegister` 类的一个成员函数。第二个 `CashRegister` 是该成员函数的名称。

```cpp
public:
    Item();
    // 其他成员函数省略
private:
    string description;
    double price;
};
```

在 Item 构造函数中，你需要将 `price` 设置为 0，但不需要初始化 `description` 数据成员。它会自动初始化为空字符串。

如果你没有为类提供任何构造函数，编译器会自动生成一个默认构造函数。默认构造函数使用其默认构造函数初始化所有类类型的数据成员，而其他数据成员则保持未初始化状态。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_432_0.png)

### 自检

- 20. 为 `BankAccount` 类的默认构造函数提供实现。
- 21. 为 `BankAccount(double)` 构造函数提供实现。
- 22. 为 Item 类的默认构造函数提供实现。
- 23. 为 `CashRegister` 类的默认构造函数提供实现，该构造函数调用 `clear` 成员函数。
- 24. 在以下每个定义中，调用了哪个构造函数？
  a. `Item item1;`
  b. `Item item2("Corn flakes");`
  c. `Item item3(3.95);`
  d. `Item item4("Corn flakes", 3.95);`
  e. `Item item5();`

**练习** — 现在你可以尝试本章末尾的这些练习：R9.13、R9.14、P9.5、P9.8。

### 常见错误 9.2 —— 试图调用构造函数

![](img/5e58fb4c840712efd6ed6fa82bb97f57_432_1.png)

构造函数只在对象首次创建时被调用。你不能再次调用它。例如，你不能调用构造函数来清除一个对象：

```cpp
CashRegister register1;
...
register1.CashRegister(); // 错误
```

确实，默认构造函数会将一个新的 `CashRegister` 对象设置为清除状态，但你不能对现有对象调用构造函数。

### 专题 9.1 —— 初始化器列表

![](img/5e58fb4c840712efd6ed6fa82bb97f57_432_2.png)

当你构造一个数据成员本身是对象的对象时，这些对象由它们所属类的默认构造函数构造。但是，如果某个数据成员属于没有默认构造函数的类，你就需要显式调用该数据成员的构造函数。下面是一个例子。

这个 Item 类没有默认构造函数：

```cpp
class Item
{
```

