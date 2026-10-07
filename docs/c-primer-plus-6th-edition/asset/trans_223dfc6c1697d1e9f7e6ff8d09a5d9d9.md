

# 第10章 对象与类

> 注意：当你将一个对象赋给同一类的另一个对象时，默认情况下 C++ 会将源对象的每个数据成员的内容复制到目标对象的对应数据成员。

你可以用构造函数做的不只是初始化新对象。例如，程序在 main() 中有此语句：

```cpp
stock1 = Stock("Nifty Foods", 10, 50.0);
```

stock1 已经存在。因此，与其初始化 stock1，此语句为对象赋予新值。它通过让构造函数创建一个新的临时对象，然后将新对象的内容复制到 stock1 来实现。程序显示临时对象的 of，并在这样做的同时调用析构函数，如以下带注释的输出所示：

```
Using a constructor to reset an object
Constructor using Nifty Foods could >> temporary object created
Bye, Nifty Foods! >> temporary object destroyed
Revised stock1:
Company: Nifty Foods Shares: 10 >> data now copied to stock1
Share Price: $50.00 Total Worth: $500.00
```

某些编译器可能会稍后处理临时对象，从而延迟析构函数。最后，程序显示如下：

```
Done
Bye, NanoSmart!
Bye, Nifty Foods!
```

当 main() 函数终止时，其局部变量（stock1 和 stock2）将从你的存在平面中消失。因为此类自动变量位于栈上，所以先创建的对象先被删除，最后创建的对象最后被删除。（请回忆，“NanoSmart” 最初在 stock1 中但已转移到 stock2，而 stock1 被重置为“Nifty Foods”）。

输出指出以下两个语句之间存在根本差异：

```cpp
stock2 = Stock("Bofo Objects", 2, 2.0);
stock1 = Stock("Nifty Foods", 10, 50.0); // temporary object
```

这两个语句中的第一个调用初始化；它使用指示的值创建一个对象，并且可能创建也可能不创建临时对象。第二个语句调用赋值。以这种方式在赋值语句中使用构造函数总会在赋值发生前创建临时对象。

> 提示：如果可以通过初始化或赋值设置值，请选择初始化。它通常更高效。

# C++11 列表初始化

使用 C++11，你可以用类使用列表初始化语法？可以，只要大括号内容与构造函数参数列表匹配：

```cpp
Stock hot_tip = {"Derivatives Plus Plus", 100, 45.0};
Stock j {"Sport Age Storage, Inc."};
Stock temp {};
```

前两个声明中的大括号列表与以下构造函数匹配：
`Stock::Stock(const std::string& co, long n = 0, double pr = 0.0);`

因此，该构造函数将被用来创建这两个对象。对于 j，第二个和第三个参数将使用默认值 0 和 0.0。第三个声明与默认构造函数匹配，因此 temp 使用它构造。

此外，C++11 提供了类 std::initializer_list，可用作函数或方法参数的类型。此类可以表示任意长度的列表，前提是所有条目都是同一类型或可以转换为同一类型。第16章“字符串类和标准模板库”将回到此主题。

# const 成员函数

考虑以下代码片段：

```cpp
const Stock land = Stock("Kludgehorn Properties");
land.show();
```

使用当前 C++，编译器应反对第二行。为什么？因为 show() 的代码未能保证它不会修改调用对象，而该对象因为是 const 不应被更改。我们之前通过将函数声明为 const 引用或指向 const 的指针来解决此类问题。但存在语法问题：show() 方法没有任何参数可供 const 限定。相反，对象是方法调用隐式使用的。需要的是新语法，表示函数承诺不修改调用对象。C++ 的解决方案是将 const 关键字放在函数括号之后。也就是说，show() 的声明看起来像这样：

```cpp
void show() const; // promises not to change invoking object
```

同样，函数的定义应如下所示：

```cpp
void Stock::show() const // promises not to change invoking object
{
    // function body here
}
```

以这种方式声明和定义的类函数称为 const 成员函数。就像你应该在适当时使用 const 引用和指针作为形式参数一样，你也应该在方法不修改调用对象时将其设为 const。我们将从此以后遵循此规则。

# 构造函数与析构函数回顾

现在我们已经通过了几个构造函数和析构函数的示例，你可能想暂停并消化所学内容。为帮助你，这里是对这些方法的总结。

构造函数是特殊类成员函数，每当创建该类的对象时调用。类构造函数与类同名，但通过函数重载，你可以有多个同名构造函数，前提是每个都有自己的签名或参数列表。此外构造函数没有声明类型。通常构造函数用于初始化类的成员。你的初始化方法应与构造函数的参数列表匹配。例如，假设 Bozo 类有以下类构造函数的原型：

```cpp
Bozo(const char* fname, const char* lname);
```

构造函数是特殊类成员函数，每当创建该类的对象时调用。类构造函数与类同名，但通过函数重载，你可以有多个同名构造函数，前提是每个都有自己的签名或参数列表。此外构造函数没有声明类型。通常构造函数用于初始化类的成员。你的初始化方法应与构造函数的参数列表匹配。例如，假设 Bozo 类有以下类构造函数的原型：

```cpp
Bozo(const char* fname, const char* lname);
```

构造函数是特殊类成员函数，每当创建该类的对象时调用。类构造函数与类同名，但通过函数重载，你可以有多个同名构造函数，前提是每个都有自己的签名或参数列表。此外构造函数没有声明类型。通常构造函数用于初始化类的成员。你的初始化方法应与构造函数的参数列表匹配。例如，假设 Bozo 类有以下类构造函数的原型：

```cpp
Bozo(const char* fname, const char* lname);
```

构造函数是特殊类成员函数，每当创建该类的对象时调用。类构造函数与类同名，但通过函数重载，你可以有多个同名构造函数，前提是每个都有自己的签名或参数列表。此外构造函数没有声明类型。通常构造函数用于初始化类的成员。你的初始化方法应与构造函数的参数列表匹配。例如，假设 Bozo 类有以下类构造函数的原型：

```cpp
Bozo(const char* fname, const char* lname);
```

构造函数没有参数，并且在你创建对象而不初始化它时使用。它可以为所有参数提供默认值：

```cpp
Bozo(); // default constructor prototype
Bistro(const char* s = "Chez Zero"); // default for Bistro
```

程序对未初始化对象使用默认构造函数：

```cpp
Bozo bubi; // use default
Bozo *pb = new Bozo; // use default
```

正如程序在创建对象时调用构造函数一样，它在对象被销毁时调用析构函数。你每个类只能有一个析构函数。它没有返回类型（甚至不是 void），没有参数，其名称是在名称前加上波浪号。例如，Bozo 类析构函数有以下原型：

```cpp
~Bozo(); // class destructor
```

当类构造函数使用 new 时，类析构函数使用 delete 变得必要。

# 认识你的对象：this 指针

构造函数没有参数，并且在你创建对象而不初始化它时使用。它可以为所有参数提供默认值：

```cpp
Bozo(); // default constructor prototype
Bistro(const char* s = "Chez Zero"); // default for Bistro
```

程序对未初始化对象使用默认构造函数：

```cpp
Bozo bubi; // use default
Bozo *pb = new Bozo; // use default
```

正如程序在创建对象时调用构造函数一样，它在对象被销毁时调用析构函数。你每个类只能有一个析构函数。它没有返回类型（甚至不是 void），没有参数，其名称是在名称前加上波浪号。例如，Bozo 类析构函数有以下原型：

```cpp
~Bozo(); // class destructor
```

如果构造函数有一个参数，则用于初始化对象。例如，假设 Bozo 类有以下原型：

```cpp
Bozo(int age);
```

那么你可以使用以下任何形式来初始化对象：

```
Bozo drizzle(44); // primary form
Bozo roon(66); // secondary form
Bozo tubby(32); // special form for one-argument
```

实际上，第三个示例是一个新点，而不是回顾，但似乎是讲这个的好时机。

# 警告

你可以用赋值使用的构造函数可能导致惊喜，因为它可能被阻止。

```cpp
class object = value;
```

此功能可能被阻止，如第11章所述。

# 认识你的对象：this 指针

你仍然可以用 Stock 类做一些事情。到目前为止，每个类成员函数都处理单个对象：调用它的对象。有时，方法可能需要处理两个对象，而这样做可能涉及一个奇特的 C++ 指针 called this。让我们看看这是如何展开的。

尽管 Stock 类声明了数据，但它在分析能力上不足。例如，通过查看 show() 输出，你可以判断你的持仓中哪一个价值最大，但程序无法直接访问 total_val。让程序了解存储数据的最直接方法是提供返回值的 方法。通常，你对它使用内联代码，如以下示例：

```cpp
class Stock
{
private:
    ...
    double total_val;

public:
    double total() const { return total_val; }
    ...
};
```

此定义在效果上使 total_val 对于直接程序访问而言成为只读内存。也就是说，你可以使用 total_val() 方法获得值，但类不提供专门重置值的方法

