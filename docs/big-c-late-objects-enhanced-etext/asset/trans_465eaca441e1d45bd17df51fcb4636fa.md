

```
void display_all(const CashRegister registers[])
{
  for (int i = 0; i < NREGISTERS; i++) { registers[i].display(); }
}
```

那位程序员很细心，将registers参数变量声明为const。但随后调用`registers[i].display()`将无法编译。因为`CashRegister::display`没有被标记为const，编译器怀疑调用`registers[i].display()`可能会修改`registers[i]`。但该函数承诺不修改registers数组。

如果你与那些对const一丝不苟的团队成员一起编写程序，你也必须做好自己那份工作。因此，你应该养成在所有访问器成员函数中使用const的习惯。

## 9.6 构造函数

每当创建对象时，构造函数会自动被调用。

构造函数是一个初始化对象数据成员的成员函数。每当创建对象时，构造函数会自动被调用。通过提供构造函数，你可以确保在任意成员函数作用于对象之前，所有数据成员都已正确设置。

为了理解构造函数的重要性，请考虑以下语句：

```
CashRegister register1;
register1.add_item(1.95);
int count = register1.get_count(); // May not be 1
```

这里，程序员在添加商品前忘记调用clear。因此，register1对象的数据成员被随机值初始化。构造函数保证对象在定义时总是被完整初始化。

构造函数的名字与类名相同。你在类定义中声明构造函数，例如：

```
class CashRegister
{
public:
  CashRegister(); // A constructor
  ...
};
```

构造函数的名字与类名相同。

![](img/d61019b035dd82beb581604273c0ee6b_485_0.png)

构造函数就像一组针对对象的装配指令。
© Ann Marie Kurtz/Stockphoto.

构造函数从不返回值，但声明它们时不需要使用void保留字。

这是该构造函数的定义：

```
CashRegister::CashRegister()
{
    item_count = 0;
    total_price = 0;
}
```

在构造函数定义中，第一个CashRegister（在`::`之前）表示我们将要定义CashRegister类的一个成员函数。第二个CashRegister是该成员函数的名字。

默认构造函数没有参数。

你刚才看到的构造函数没有参数。这样的构造函数称为默认构造函数。每当你定义一个对象且未指定任何构造参数时，都会使用它。例如，如果你定义

```
CashRegister register1;
```

那么默认构造函数就会被调用。它将`register1.item_count`和`register1.total_price`设置为零。

一个类可以有多个构造函数。

许多类拥有不止一个构造函数。这允许你以不同的方式定义对象。例如，考虑一个具有两个构造函数的BankAccount类：

```
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

编译器会选择与构造参数匹配的构造函数。

两个构造函数都与类同名，即BankAccount。但默认构造函数没有参数变量，而第二个构造函数有一个double参数变量。（这是重载的一个例子——参见专题9.1。）

当你构造一个对象时，编译器会选择与你提供的参数匹配的构造函数。例如，

```
BankAccount joes_account;
// Uses default constructor
BankAccount lisas_account(499.95);
// Uses BankAccount(double) constructor
```

请务必在构造函数中初始化所有数值和指针数据成员。

在实现构造函数时，你需要特别关注所有类型为数值或指针的数据成员。这些类型不是类，因此没有构造函数。如果你有一个数据成员是某个类的对象（例如string对象），那么该类有构造函数，该对象会被初始化。例如，所有string对象都会自动初始化为空字符串。

考虑这个类：

```
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

在Item构造函数中，你需要将price设置为0，但无需初始化description数据成员。它会自动初始化为空字符串。

从C++11开始，你可以为数据成员指定默认值：

```
class Item
{
public:
    // No constructor
    // Member functions
private:
    string description;
    double price = 0;
};
```

如果你在构造函数中没有初始化price，它会被设置为零。

如果你没有为类提供任何构造函数，编译器会自动生成一个默认构造函数。自动生成的默认构造函数会初始化那些具有默认构造函数或默认值的数据成员，而保持其他数据成员未初始化。

## 示例代码

请参阅配套代码中的sec06，其中包含带单个构造函数的完整CashRegister类、带两个构造函数的BankAccount类，以及带三个构造函数的Item类。

![](img/d61019b035dd82beb581604273c0ee6b_487_0.png)

## 常见错误 9.2

### 试图调用构造函数

构造函数只在对象首次创建时被调用。你不能再次调用它。例如，你不能调用构造函数来清空一个对象：

```
CashRegister register1;
...
register1.CashRegister(); // Error
```

默认构造函数确实会将一个新的CashRegister对象设置为清空状态，但你不能在现有对象上调用构造函数。

在这种情况下，你可以直接调用clear成员函数：

```
register1.clear();
```

![](img/d61019b035dd82beb581604273c0ee6b_487_1.png)

## 专题 9.1

### 重载

当同一个函数名被用于多个函数时，这个名字就被重载了。在C++中，只要参数变量的类型不同，你就可以重载函数名。例如，你可以定义两个都叫做print的函数：

```
void print(CashRegister r)
void print(Item i)
```

当print函数被调用时，
`print(x);`
编译器会查看x的类型。如果x是一个CashRegister对象，则调用第一个函数。如果x是一个Item对象，则调用第二个函数。如果x两者都不是，编译器会生成一个错误。

通过给每个函数起一个唯一的名字，例如`print_register`或`print_item`，总是可以避免重载。但在构造函数上我们没有选择。C++要求构造函数的名字必须与类名相同。如果一个类有多个构造函数，那么这个名字就必须被重载。

除了名字重载，C++还支持运算符重载。可以为熟悉的C++运算符（如+、==和<<）赋予新的含义。这是一项高级技术，我们将在第13章中讨论。

![](img/d61019b035dd82beb581604273c0ee6b_488_0.png)

## 专题 9.2

### 初始化列表

当你构造一个其数据成员本身也是对象的对象时，这些对象会由它们类的默认构造函数来构造。然而，如果某个数据成员属于没有默认构造函数的类，你就需要显式调用该数据成员的构造函数。下面是一个例子。

这个Item类没有默认构造函数：

```cpp
class Item
{
public:
    Item(string item_description, double item_price);
    // No other constructors
    ...
};
```

这个Order类有一个Item类型的数据成员：

```cpp
class Order
{
public:
    Order(string customer_name, string item_description, double item_price);
    ...
private:
    Item article;
    string customer;
};
```

Order构造函数必须调用Item构造函数。这可以通过初始化列表来实现。初始化列表放在构造函数左花括号之前。列表以冒号开头，包含数据成员的名字及其构造参数。

```cpp
Order::Order(string customer_name, string item_description, double item_price)
    : article(item_description, item_price)
{
    customer = customer_name;
}
```

初始化项之间用逗号分隔。它们也可以用一个同类型的值来初始化数据成员。这是编写Order构造函数的另一种方式：

```cpp
Order::Order(string customer_name, string item_description, double item_price)
    : article(item_description, item_price), customer(customer_name)
{
}
```

