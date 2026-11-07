
```cpp
...
}
```

这是错误的。构造函数参数并不代表类成员；它们代表要赋给类成员的值。因此，它们必须具有不同的名称，否则最终会得到像下面这样令人困惑的代码：

```cpp
shares = shares;
```

一种有助于避免此类混淆的常见编码做法是使用 m_ 前缀来标识数据成员名：

```cpp
class Stock
{
private:
    string m_company;
    long m_shares;
    ...
```

另一种常见做法是为成员名使用下划线后缀：

```cpp
class Stock
{
private:
    string company_;
    long shares_;
    ...
```

采用任一约定后，你就可以在公共接口中使用 `company` 和 `shares` 作为参数名。

## 使用构造函数

C++ 提供了两种使用构造函数初始化对象的方式。第一种是显式调用构造函数：

```cpp
Stock food = Stock("World Cabbage", 250, 1.25);
```

这会将 food 对象的 company 成员设置为字符串 `"World Cabbage"`，将 shares 成员设置为 250，依此类推。

第二种是隐式调用构造函数：

```cpp
Stock garment("Furry Mason", 50, 2.5);
```

这种更紧凑的形式等价于以下显式调用：

```cpp
Stock garment = Stock("Furry Mason", 50, 2.5);
```

每当你创建该类的对象时，C++ 都会使用类构造函数，即使使用 new 进行动态内存分配时也是如此。下面是如何将构造函数与 new 一起使用：

```cpp
Stock *pstock = new Stock("Electroshock Games", 18, 19.0);
```

第二种方法是使用函数重载定义第二个构造函数，一个没有参数的构造函数：

```cpp
Stock();
```

默认构造函数只能有一个，所以确保不要同时提供两种。实际上，通常应初始化对象，以确保所有成员都以已知、合理的值开始。因此，用户提供的默认构造函数通常为所有成员值提供隐式初始化。例如，下面是为 Stock 类定义默认构造函数的一种方式：

```cpp
Stock::Stock()          // default constructor
{
    company = "no name";
    shares = 0;
    share_val = 0.0;
    total_val = 0.0;
}
```

> **提示**
> 
> 设计类时，通常应提供一个默认构造函数，隐式初始化所有类成员。

使用任一方法（无参数或为所有参数提供默认值）创建默认构造函数后，就可以声明对象变量而无需显式初始化它们：

```cpp
Stock first;                 // calls default constructor implicitly
Stock first = Stock();        // calls it explicitly
Stock *pfirst = new Stock;    // calls it implicitly
```

不过，不要被非默认构造函数的隐式形式误导：

```cpp
Stock first("Concrete Conglomerate");     // calls constructor
Stock second();                            // declares a function
Stock third;                               // calls default constructor
```

这里的第一个声明调用非默认构造函数，即接受参数的那个构造函数。第二个声明表示 second() 是一个返回 Stock 对象的函数。隐式调用默认构造函数时，不要使用括号。

## 析构函数

当你使用构造函数创建对象时，程序承担跟踪该对象直到其过期的责任。届时，程序会自动调用一个特殊成员函数，其令人生畏的名称为析构函数。析构函数应清理任何残留物，因此它实际上有有用的作用。例如，如果你的构造函数使用 new 分配内存，析构函数应使用 delete 释放该内存。Stock 构造函数没有做像使用 new 这样的花哨事情，因此 Stock 类析构函数实际上没有任何任务要执行。在这种情况下，你可以直接让编译器生成一个隐式的、什么都不做的析构函数，这正是 Stock 类的第一个版本所做的。另一方面，研究如何声明和定义析构函数当然值得，所以让我们为 Stock 类提供一个析构函数。

与构造函数一样，析构函数有一个特殊名称：它由类名前面加一个波浪号（~）构成。因此，Stock 类的析构函数称为 ~Stock()。同样与构造函数一样，析构函数不能有返回值，也没有声明的类型。与构造函数不同，析构函数必须没有参数。因此，Stock 析构函数的原型必须如下：

```cpp
~Stock();
```

由于 Stock 析构函数没有重要职责，你可以将其编码为不做任何事的函数：

```cpp
Stock::~Stock()
{
}
```

不过，为了让你看到析构函数何时被调用，我们这样编写它：

```cpp
Stock::~Stock()   // class destructor
{
    cout << "Bye, " << company << "!\n";
}
```

析构函数应在何时被调用？编译器处理此决定；通常不应显式调用析构函数。（例外情况见第12章“类和动态内存分配”中的“再看‘定位 new’”一节。）如果创建静态存储类对象，其析构函数会在程序终止时自动调用。如果创建自动存储类对象，正如示例一直在做的那样，其析构函数会在程序退出定义该对象的代码块时自动调用。如果对象通过使用 new 创建，它位于堆内存或自由存储区中，其析构函数会在你使用 delete 释放内存时自动调用。最后，程序可以创建临时对象来执行某些操作；在这种情况下，程序在完成使用该对象后会自动调用其析构函数。

由于类对象过期时会自动调用析构函数，所以应该有一个析构函数。如果你不提供，编译器会隐式声明一个默认析构函数，并且如果检测到导致对象销毁的代码，它会提供该析构函数的定义。

## 改进 Stock 类

此时，我们需要将构造函数和析构函数并入类和方法定义中。鉴于添加构造函数的重要性，我们将文件名从 stock00.h 推进到 stock10.h。类方法放入名为 stock10.cpp 的文件中。最后，我们将使用这些资源的程序放入第三个文件 usestock2.cpp 中。

### 头文件

程序清单10.4展示了 stock 程序的头文件。它将构造函数和析构函数的原型添加到原始类声明中。它还去掉了 acquire() 函数，既然类现在已有构造函数，该函数不再必要。该文件还使用了第9章描述的 #ifndef 技术，以防止此文件被多次包含。

程序清单10.4  stock10.h

```cpp
// stock10.h -- Stock class declaration with constructors, destructor added
#ifndef STOCK10_H_
#define STOCK10_H_
#include <string>

class Stock
{
private:
    std::string company;
    long shares;
    double share_val_;
    double total_val_;
    void set_tot() { total_val_ = shares * share_val_; }
public:
    // two constructors
    Stock();        // default constructor
    Stock(const std::string & co, long n = 0, double pr = 0.0);
    ~Stock();       // noisy destructor
    void buy(long num, double price);
    void sell(long num, double price);
    void update(double price);
    void show();
};

#endif
```

### 实现文件

程序清单10.5提供了 stock 程序的方法定义。它包含 stock10.h 文件以提供类声明。（回想一下，将文件名括在双引号中而不是方括号中，会使编译器在源文件所在位置搜索它。）程序清单10.5还包含 iostream 头文件以提供 I/O 支持。该清单还提供了 using 声明和限定名（例如 std::string），以访问头文件中的各种声明。此文件将构造函数和析构函数方法定义添加到先前的方法中。为了帮助你看出这些方法何时被调用，它们各自显示一条消息。这
