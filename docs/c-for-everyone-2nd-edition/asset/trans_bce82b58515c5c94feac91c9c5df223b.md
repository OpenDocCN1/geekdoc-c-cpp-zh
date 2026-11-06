
```cpp
/**
    Adds an item to this cash register.
    @param price the price of this item
*/
void add_item(double price);

/**
    @return the total amount of the current sale
*/
double get_total() const;

/**
    @return the item count of the current sale
*/
int get_count() const;

private:
    int item_count;
    double total_price;
};

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

## 程序运行

```text
1 $1.95
2 $2.90
3 $5.40
```

![](img/23fb3582e93ebc95909e1de029c3d388_429_0.png)

- 15. 这个 `get_total` 成员函数的实现有什么问题？

  ```cpp
  int get_total()
  {
      return total_price;
  }
  ```

- 16. 实现 9.4.3 节中描述的 `add_items` 成员函数，但不要调用 `add_item`。

- 17. 为 CashRegister 类实现一个成员函数 `get_dollars`，它以美元值（不含美分）给出总销售额。

- 18. 考虑 string 类的 `substr` 成员函数。它有多少个参数，它们是什么类型？

- 19. 考虑 string 类的 `length` 成员函数。它有多少个参数，它们是什么类型？

## 实践练习

现在你可以尝试本章末尾的这些练习：P9.3、P9.4、P9.6。

## 编程提示 9.1

### 所有数据成员都应为私有；大多数成员函数应为公有

![](img/23fb3582e93ebc95909e1de029c3d388_429_1.png)

可以在类的公有部分定义数据成员，但在你自己的代码中不应这样做。始终使用封装，用私有数据成员并通过成员函数来操作它们。

通常，成员函数应为公有。然而，有时某个成员函数仅被其他成员函数用作辅助函数。在这种情况下，你可以将该辅助函数设为私有。只需在类的私有部分声明它即可。

## 编程提示 9.2

### const 正确性

![](img/23fb3582e93ebc95909e1de029c3d388_429_2.png)

在 C++ 中，应使用 const 保留字声明所有访问器函数。（回顾一下，访问器函数是不修改其隐式参数的成员函数。）

例如，假设你设计了以下类：

```cpp
class CashRegister
{
    void display(); // Bad style—no const
    ...
};
```

编译代码时不会报告错误。但现在假设另一位程序员在函数中使用你的 CashRegister 类：

```cpp
void display_all(const CashRegister registers[])
{
    for (int i = 0; i < NREGISTERS; i++) { registers[i].display(); }
}
```

那位程序员很认真，将 `registers` 参数变量声明为 const。但这样一来，调用 `registers[i].display()` 将无法编译。因为 `CashRegister::display` 未标记为 const，编译器怀疑调用 `registers[i].display()` 可能修改 `registers[i]`。但该函数承诺不修改 `registers` 数组。

如果你与其他认真对待 const 的团队成员一起编写程序，那么你做好自己这部分也非常重要。因此，你应养成对所有访问器成员函数使用 const 的习惯。

## 9.5 构造函数

> 每当创建对象时，都会自动调用构造函数。

构造函数是一个成员函数，用于初始化对象的数据成员。每当创建对象时，都会自动调用构造函数。通过提供构造函数，你可以确保在任何成员函数作用于对象之前，所有数据成员都已正确设置。

要理解构造函数的重要性，请考虑以下语句：

```cpp
CashRegister register1;
register1.add_item(1.95);
int count = register1.get_count(); // May not be 1
```

这里，程序员忘记在添加项目之前调用 `clear`。因此，`register1` 对象的数据成员被初始化为随机值。构造函数保证对象在定义时始终被完全初始化。

> 构造函数的名称与类名相同。

构造函数的名称与其类名完全相同。你在类定义中声明构造函数，例如：

```cpp
class CashRegister
{
    public:
        CashRegister(); // A constructor
    ...
};
```

构造函数从不返回值，但声明它们时不使用 `void` 保留字。

以下是该构造函数的定义：

```cpp
CashRegister::CashRegister()
{
    item_count = 0;
    total_price = 0;
}
```

在构造函数定义中，第一个 `CashRegister`（位于 `::` 之前）表示我们将要定义 `CashRegister` 类的一个成员函数。第二个 `CashRegister` 是该成员函数的名称。

*构造函数就像对象的一组汇编指令。*

![](img/23fb3582e93ebc95909e1de029c3d388_431_0.png)

> 默认构造函数没有参数。

你刚才看到的构造函数没有参数。这样的构造函数称为**默认构造函数**。每当你定义对象且未为构造指定任何参数时，就会使用它。例如，如果你定义

```cpp
CashRegister register1;
```

那么就会调用默认构造函数。它将 `register1.item_count` 和 `register1.total_price` 设置为零。

> 一个类可以有多个构造函数。

许多类有不止一个构造函数。这允许你以不同方式定义对象。例如，考虑一个有两个构造函数的 `BankAccount` 类：

```cpp
class BankAccount
{
public:
  BankAccount(); // Sets balance to 0
  BankAccount(double initial_balance); // Sets balance to initial_balance
  // Member functions omitted
private:
  double balance;
};
```

> 编译器会选择与构造实参匹配的构造函数。

两个构造函数都与类同名，即 `BankAccount`。但默认构造函数没有参数变量，而第二个构造函数有一个 double 参数变量。（这是**重载**的一个例子——见专题 9.2。）

当你构造对象时，编译器会选择与你提供的实参匹配的构造函数。例如，

```cpp
BankAccount joes_account;
  // Uses default constructor
BankAccount lisas_account(499.95);
  // Uses BankAccount(double) constructor
```

> 务必在构造函数中初始化所有数字和指针数据成员。

实现构造函数时，你需要特别注意所有为数字或指针的数据成员。这些类型不是类，因此没有构造函数。如果你有一个数据成员是某个类的对象（例如 string 对象），那么该类有构造函数，该对象将被初始化。例如，所有 string 对象都会自动初始化为空字符串。

考虑这个类：

```cpp
class Item
{
public:
    Item();
    // Additional member functions omitted
private:
    string description;
    double price;
};
```

在 `Item` 构造函数中，你需要将 `price` 设置为 0，但不必初始化 `description` 数据成员。它会自动初始化为空字符串。

如果你没有为类提供任何构造函数，编译器会自动生成一个默认构造函数。默认构造函数会用其默认构造函数初始化所有类类型的数据成员，并使其他数据成员保持未初始化状态。

![](img/23fb3582e93ebc95909e1de029c3d388_432_0.png)

## 自测

- 20. 为 `BankAccount` 类提供默认构造函数的实现。

- 21. 为 `BankAccount(double)` 构造函数提供实现。

- 22. 为 `Item` 类提供默认构造函数的实现。

- 23. 为 `CashRegister` 类提供默认构造函数的实现，并调用 `clear` 成员函数。

- 24. 在以下每个定义中调用的是哪个构造函数？
  - a. `Item item1;`
  - b. `Item item2("Corn flakes");`
  - c. `Item item3(3.95);`
  - d. `Item item4("Corn flakes", 3.95);`
  - e. `Item item5();`

**实践练习** 现在你可以尝试本章末尾的这些练习：R9.13、R9.14、P9.5、P9.8。

## 常见错误 9.2

### 试图调用构造函数

构造函数仅在对象首次创建时被调用。你不能再次调用它。例如，你不能调用构造函数来清除对象：

```cpp
CashRegister register1;
...
register1.CashRegister(); // Error
```

确实，默认构造函数会将新的 `CashRegister` 对象设置为已清除状态，但你不能对现有对象调用构造函数。

![](img/23fb3582e93ebc95909e1de029c3d388_432_1.png)

## 专题 9.1

### 初始化列表

当你构造一个其数据成员本身也是对象的对象时，那些对象会由其类的默认构造函数构造。然而，如果某个数据成员所属的类没有默认构造函数，你就需要显式调用该数据成员的构造函数。下面是一个例子。

这个 `Item` 类没有默认构造函数：

```cpp
class Item
{
```

![](img/23fb3582e93ebc95909e1de029c3d388_432_2.png)

