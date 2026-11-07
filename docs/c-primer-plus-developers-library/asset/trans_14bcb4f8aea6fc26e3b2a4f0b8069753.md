
### 清单 10.5 stock10.cpp

```cpp
// stock10.cpp -- Stock class with constructors, destructor added
#include <iostream>
#include "stock10.h"

// constructors (verbose versions)
Stock::Stock()        // default constructor
{
    std::cout << "Default constructor called\n";
    company = "no name";
    shares = 0;
    share_val = 0.0;
    total_val = 0.0;
}

Stock::Stock(const std::string & co, long n, double pr)
{
    std::cout << "Constructor using " << co << " called\n";
    company = co;

    if (n < 0)
    {
        std::cout << "Number of shares can't be negative; "
                  << company << " shares set to 0.\n";
        shares = 0;
    }
    else
        shares = n;
    share_val = pr;
    set_tot();
}
// class destructor
Stock::~Stock()        // verbose class destructor
{
    std::cout << "Bye, " << company << "!\n";
}

// other methods
void Stock::buy(long num, double price)
{
    if (num < 0)
    {
        std::cout << "Number of shares purchased can't be negative. "
    }
else
{
    shares += num;
    share_val = price;
    set_tot();
}
}

void Stock::sell(long num, double price)
{
    using std::cout;
    if (num < 0)
    {
        cout << "Number of shares sold can't be negative. "
             << "Transaction is aborted.\n";
    }
    else if (num > shares)
    {
        cout << "You can't sell more than you have! "
             << "Transaction is aborted.\n";
    }
    else
    {
        shares -= num;
        share_val = price;
        set_tot();
    }
}

void Stock::update(double price)
{
    share_val = price;
    set_tot();
}

void Stock::show()
{
    using std::cout;
    using std::ios_base;
    // set format to #.###
    ios_base::fmtflags orig =
        cout.setf(ios_base::fixed, ios_base::floatfield);
    std::streamsize prec = cout.precision(3);

    cout << "Company: " << company
```

```cpp
stock1.show();
cout << "Done\n";
}
return 0;
}
```

编译由清单 10.4、10.5 和 10.6 表示的程序会生成一个可执行程序。下面是某个编译器运行该可执行程序后的输出：

```text
Using constructors to create new objects
Constructor using NanoSmart called
Company: NanoSmart  Shares: 12
  Share Price: $20.00  Total Worth: $240.00
Constructor using Boffo Objects called
Company: Boffo Objects  Shares: 2
  Share Price: $2.00  Total Worth: $4.00
Assigning stock1 to stock2:
Listing stock1 and stock2:
Company: NanoSmart  Shares: 12
  Share Price: $20.00  Total Worth: $240.00
Company: NanoSmart  Shares: 12
  Share Price: $20.00  Total Worth: $240.00
Using a constructor to reset an object
Constructor using Nifty Foods called
Bye, Nifty Foods!
Revised stock1:
Company: Nifty Foods  Shares: 10
  Share Price: $50.00  Total Worth: $500.00
Done
Bye, NanoSmart!
Bye, Nifty Foods!
```

有些编译器生成程序后，其初始输出可能如下，其中多了一行：

```text
Using constructors to create new objects
Constructor using NanoSmart called
Company: NanoSmart  Shares: 12
  Share Price: $20.00  Total Worth: $240.00
Constructor using Boffo Objects called
Bye, Boffo Objects!                         << additional line
Company: Boffo Objects  Shares: 2
  Share Price: $2.00  Total Worth: $4.00
...
```

下面的“程序说明”部分解释了该输出中的“Bye, Boffo Objects!”这一行。

> **注意**
>
> 你可能已经注意到，清单 10.6 在 `main()` 开头和接近结尾处多了一对大括号。像 `stock1` 和 `stock2` 这样的自动变量会在程序退出包含其定义的块时销毁。如果没有这对额外的大括号，该块就会是 `main()` 的函数体，因此析构函数直到 `main()` 执行完毕后才会被调用。在窗口环境中，这意味着窗口会在最后两次析构函数调用之前关闭，使你无法看到最后两条消息。但有了这对大括号，最后两次析构函数调用会在到达 `return` 语句之前发生，因此这些消息会显示出来。

## 程序说明

在清单 10.6 中，语句

```cpp
Stock stock1("NanoSmart", 12, 20.0);
```

创建一个名为 `stock1` 的 Stock 对象，并将其数据成员初始化为指定的值：

```text
Constructor using NanoSmart called
Company: NanoSmart Shares: 12
```

下面的语句使用另一种语法创建并初始化一个名为 `stock2` 的对象：

```cpp
Stock stock2 = Stock ("Boffo Objects", 2, 2.0);
```

C++ 标准为编译器提供了几种执行这第二种语法的方式。一种是让它表现得与第一种语法完全相同：

```text
Constructor using Boffo Objects called
Company: Boffo Objects Shares: 2
```

第二种方式是允许构造函数调用创建一个临时对象，然后将其复制到 `stock2`。随后丢弃该临时对象。如果编译器采用这种方式，就会为临时对象调用析构函数，从而改为产生如下输出：

```text
Constructor using Boffo Objects called
Bye, Boffo Objects!
Company: Boffo Objects Shares: 2
```

产生该输出的编译器立即处理掉了临时对象，但编译器也可能等待更长时间，在这种情况下，析构函数消息会稍后显示。

下面的语句说明，可以将一个对象赋给另一个同类型的对象：

```cpp
stock2 = stock1;      // object assignment
```

与结构体赋值一样，类对象赋值默认情况下会将一个对象的成员复制到另一个对象。在本例中，`stock2` 的原始内容会被覆盖。

> **注意**
> 当你将一个对象赋给同一类的另一个对象时，默认情况下，C++ 会将源对象的每个数据成员的内容复制到目标对象的对应数据成员中。

构造函数的用途不仅限于初始化新对象。例如，程序在 `main()` 中有如下语句：
`stock1 = Stock("Nifty Foods", 10, 50.0);`

`stock1` 对象已经存在。因此，这条语句不是初始化 `stock1`，而是为该对象赋新值。它通过让构造函数创建一个新的临时对象，然后将新对象的内容复制到 `stock1` 来实现这一点。随后，程序处理掉临时对象，并在此过程中调用析构函数，如下面的带注释输出所示：

```text
Using a constructor to reset an object
Constructor using Nifty Foods called >> temporary object created
Bye, Nifty Foods!                >> temporary object destroyed
Revised stock1:
Company: Nifty Foods  Shares: 10      >> data now copied to stock1
Share Price: $50.00  Total Worth: $500.00
```

有些编译器可能会稍后处理临时对象，从而延迟析构函数调用。最后，在程序结束时，会显示如下内容：

```text
Done
Bye, NanoSmart!
Bye, Nifty Foods!
```

当 `main()` 函数终止时，其局部变量（`stock1` 和 `stock2`）便从你的存在层面消失了。由于这类自动变量位于栈上，最后创建的对象最先被删除，最先创建的对象最后被删除。（回想一下，“NanoSmart”最初在 `stock1` 中，但后来被转移到 `stock2`，而 `stock1` 被重置为“Nifty Foods”。）

输出指出了下面两条语句之间存在根本区别：

```cpp
Stock stock2 = Stock ("Boffo Objects", 2, 2.0);
stock1 = Stock("Nifty Foods", 10, 50.0); // temporary object
```

这两条语句中的第一条调用初始化；它用指定的值创建一个对象，并且可能会也可能不会创建临时对象。第二条语句调用赋值。以这种方式在赋值语句中使用构造函数，总是会在赋值发生之前创建一个临时对象。

> **提示**
> 如果你既可以通过初始化也可以通过赋值来设置对象的值，请选择初始化。它通常更高效。

