
图 19.15 | `BasePlusCommissionEmployee` 继承自 `CommissionEmployee` 类，但无法直接访问该类的私有数据。（2 部分中的第 2 部分）。

### BasePlusCommissionEmployee 成员函数 earnings

`BasePlusCommissionEmployee` 类的 `earnings` 函数（图 19.15，第 34–37 行）重定义了 `CommissionEmployee` 的 `earnings` 成员函数（图 19.14）。`BasePlusCommissionEmployee` 的 `earnings` 函数通过调用 `CommissionEmployee::earnings()`（图 19.15，第 36 行）来获取基类值，而不是直接访问基类。这封装了对数据成员 `baseSalary` 实现的更改。例如，如果我们决定重命名数据成员 `baseSalary` 或更改其类型，则只需要更改 `baseSalary` 成员函数。

（注：此处原文描述中似乎存在逻辑混乱或排码错误，已根据语意进行对应翻译）

常见编程错误 19.2

当派生类中重定义基类函数时，派生类版本通常会调用基类版本。在引用基类时未使用基类名称作用域解析符会导致无限递归。

### BasePlusCommissionEmployee 成员函数 print

同样，`BasePlusCommissionEmployee` 的 `print` 函数（图 19.15，第 40–48 行）重定义了 `CommissionEmployee` 的 `print` 函数（图 19.14）以输出基类信息。`BasePlusCommissionEmployee` 的 `print` 函数通过调用限定名称 `CommissionEmployee::print()`（图 19.15，第 47 行）输出剩余信息。

### 修改后的类测试

再次，此示例使用 `BasePlusCommissionEmployee` 测试图 19.9 并产生相同的 "base-salaried employee"。

### CommissionEmployee—BaseCommissionEmployee 示例总结

在本节中，设计的示例旨在教授你继承的核心能力。你学习了如何使用继承创建派生类，如何使用保护类成员允许派生类访问基类数据，以及如何重定义基类函数以提供派生类的版本。此外，你还学习了如何应用第 17 章和本章的软件工程技术创建易维护、修改和调试的类。

## 19.4 派生类中的构造函数和析构函数

如前所述，实例化派生类对象会开始构造函数调用链，派生类构造函数在执行任务时会调用其直接基类的构造函数（显式通过基类成员初始化或隐式调用基类的默认构造函数）。同样，如果基类派生自另一个类，则基类构造函数需要调用层次结构中下一个类的构造函数，依此类推。此链中的最后一个构造函数是基类的，其函数体最早执行。最底层派生类的构造函数最后执行。每个基类构造函数都会初始化派生类继承的基类成员。在我们研究的 `CommissionEmployee`/`BasePlusCommissionEmployee` 层次结构中，当程序创建一个 `BasePlusCommissionEmployee` 对象时，会调用 `CommissionEmployee` 构造函数。由于 `CommissionEmployee` 是层次结构的基类，它的构造函数会执行，初始化 `BasePlusCommissionEmployee` 对象的私有 `CommissionEmployee` 数据成员。当 `CommissionEmployee` 构造函数完成后，它返回 `BasePlusCommissionEmployee` 构造函数，初始化 `BasePlusCommissionEmployee` 对象的 `baseSalary`。

软件 工程观察 19.6

![](img/fa81e30d8bce030c9060826ba9997d7b_791_0.png)

当程序创建一个派生类对象时，派生类立即调用基类构造函数，执行基类构造体，然后执行派生类的成员初始化，最后执行派生类的函数体。如果层次结构包含两个以上级别，此过程将向上级联。

当派生类对象被销毁时，程序会调用该析构函数。这会在派生类析构函数以及直接和间接基类的析构函数中引发一链的析构函数调用（或级联调用），并且类成员的执行顺序与构造函数执行的顺序是相反的。当调用一个派生类对象时，析构函数执行其任务，然后调用层次结构顶端的派生基类的析构函数。该过程会一直重复进行，直到层次结构顶端的最终基类的析构函数被调用。然后，对象将从内存中移除。

## 软件工程观察 19.7

假设我们创建了一个派生类的对象，其中基类和派生类都（通过组合）包含了其他类的对象。当该派生类的对象被创建时，基类成员的构造函数执行，接着执行基类的构造函数体，然后执行派生类成员的构造函数，最后执行派生类的构造函数体。析构函数的调用顺序与其相应的构造函数被调用的顺序相反。

基类的构造函数、析构函数和重载的赋值运算符（第 18 章）不会被类继承。派生类的构造函数、析构函数和重载的赋值运算符可以调用基类的版本。

## C++11：继承基类构造函数

有时，派生类的构造函数仅仅是模仿基类的构造函数。C++11 一个经常被请求的功能是可以继承基类的构造函数。现在你可以在派生类定义中的任何地方显式使用如下形式的声明来实现：

```
using BaseClass::BaseClass;
```

在上述声明中，`BaseClass` 是基类的名称。除了少数例外（下文所示）之外，对于基类中的每个构造函数，编译器都会生成一个与基类构造函数对应的派生类构造函数。生成的构造函数仅对派生类额外的数据成员执行默认初始化。当你继承构造函数时：

- 默认情况下，每个继承的构造函数具有与其相应的基类构造函数相同的访问级别（public、protected 或 private）。
- 默认、拷贝构造函数和移动构造函数不会被继承。
- 如果在基类中通过在原型中放置 `= delete` 删除了构造函数，则派生类中的该构造函数也会被删除。
- 如果派生类没有显式定义构造函数，编译器会在派生类中生成一个默认构造函数——即使它继承了其他构造函数。
- 如果你在派生类中显式定义的构造函数与基类构造函数具有相同的参数列表，则基类构造函数不会被继承。
- 基类构造函数的默认参数不会被继承。相反，编译器会在派生类中生成重载的构造函数。例如，如果基类声明了构造函数：

```
BaseClass( int = 0, double = 0.0 );
```

![](img/fa81e30d8bce030c9060826ba9997d7b_792_0.png)

## 19.5 public, protected 和 private 继承

编译器生成以下两个没有默认参数的派生类构造函数：

```
DerivedClass( int );

DerivedClass(int, double);
```
