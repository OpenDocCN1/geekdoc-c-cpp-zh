
## static_assert

`static_assert` 声明允许你在编译时测试程序的某些方面。`static_assert` 声明接受一个常量整型表达式和一个字符串字面量。如果表达式求值为 0（false），编译器会报告错误。错误消息包含声明中提供的字符串字面量。`static_assert` 声明可用于命名空间、类或局部作用域。

添加 `static_assert` 使学习 C++ 更容易。当新手犯下常见错误（例如在函数调用或模板实例化中使用错误类型的实参）时，这些断言可用于提供信息更丰富的错误消息。它们在库开发中也很有用——可以更有效地报告库的不正确用法。

## 与新 C99 特性的兼容性

C++0x 将纳入 1999 年 C 标准中新增的许多变更。这些变更包括对 C 预处理器的更改、增加 long long 整数类型，以及对添加额外整数类型（例如 128 位整数类型）的扩展施加规则。这些变更使现代 C 代码能够正确地作为 C++ 编译。

## 委托构造函数

此特性允许一个构造函数委托给该类的另一个构造函数（即调用该类的另一个构造函数）。这使得编写重载构造函数更容易。目前，重载构造函数必须重复其他构造函数所共有的代码。这会导致重复且容易出错的代码。一个构造函数中的错误可能导致对象初始化不一致。通过调用构造函数的另一个版本，公共代码无需重复，出错的可能性也会降低。

## 右尖括号

目前，在使用嵌套模板类型时，必须在末尾的右尖括号（>）之间加一个空格。如果没有空格，编译器会假定这两个括号是右移运算符（`>>`）。这意味着编写 `vector<vector<int>>` 会导致编译器错误。该语句必须写成 `vector<vector<int> >`。许多新手会被 C++ 的这个怪癖绊倒。在 C++0x 中，C++ 编译器将能够识别 `>>` 是模板的一部分，而不是右移运算符。

## 从初始化器推导变量类型[^22]

此提案为关键字 auto 定义了新功能——它根据初始化表达式自动确定变量类型。auto 可用于替代那些冗长复杂、手工输入难以管理的类型。auto 还可以与 const 和 volatile 限定符一起使用。你可以像使用完整类型名那样，使用 auto 创建指针和引用。auto 支持在一条语句中声明多个变量（例如 `auto x = 1, y = 2`）。auto 关键字旨在节省时间、简化学习过程并改进泛型编程。以下代码创建一个包含假想 `Class<T>` 实例的 vector。

```cpp
vector<Class<T>> myVector;
vector<Class<T>>::const_iterator iterator = myVector.begin();
```

使用 auto，iterator 的声明可以写成

```cpp
auto iterator = myVector.begin();
```

iterator 的类型是 `vector<Class<T>>::const_iterator`。你也可以在一条声明中创建两个相同类型的变量。以下声明中的两个变量都以 `vector<Class<T>>::const_iterator` 类型创建：

```cpp
auto iteratorBegin = myVector.begin(), iteratorEnd = myVector.end();
```

你还可以将 auto 与 const 或 volatile 限定符一起使用，并创建指针或引用。语句

```cpp
const auto &iteratorRef = myVector.begin();
```

创建了一个指向 `vector<Class<T>>::const_iterator` 的 const 引用。auto 通过自动确定你所声明变量的类型，可以为你节省大量时间——尤其是在处理复杂模板类型时，例如第 22.6 节中使用的那些类型。

## 可变参数模板[^23]

目前，每个类模板或函数模板都有固定数量的模板参数。如果你需要一个具有不同数量模板参数的类模板或函数模板，就必须为每种情况定义一个模板。可变参数模板接受任意数量的实参，这可以极大地简化模板编程。例如，你可以提供一个可变参数函数模板，而不是提供许多具有不同参数的重载函数模板。许多模板库（如 Boost.Bind、Boost.Tuple 和 Boost.Function）包含大量重复代码，或利用复杂的预处理器宏来生成所有必要的模板定义。可变参数模板将使实现此类库更加容易。

## 模板别名[^24]

库经常使用带有很多参数的模板来实现泛型编程。有时可能需要为模板指定某些保持不变的具体实参，同时仍能让其余实参变化。这可以通过模板别名来实现。**模板别名**类似于 typedef——它引入一个用于指代模板的名称。在 typedef 中，所有模板参数都被指定。使用模板别名时，某些参数被指定，而其他参数仍可变化。你可以通过使用模板别名来设置保持一致的参数，同时仍能改变每次实例化中发生变化的参数，从而将通用模板用于更具体的角色，其中许多实参始终相同。例如，以下代码声明了一个模板 `MyStack`，它使用 `list<T>` 作为其底层实现，而不是 `std::stack` 中默认使用的 deque。

```cpp
template<typename T> using MyStack =
    stack<T, list<T>>;
```

## 用户定义类型的初始化器列表[^25]

目前，初始化器列表只能用于数组和结构体。在 C++0x 中，类可以定义一个构造函数，它接受一个 `std::initializer_list<T>` 类型的参数。然后就可以使用初始化器列表来初始化该类的对象，如下所示：

```cpp
vector<int> second = { 4, 5, 6 }; // legal in C++0x
```

初始化器值存储在一个 `initializer_list` 对象中，该对象被传递给类的构造函数。所有标准库容器类都将更新为具有接受 `initializer_list` 的构造函数。

## 基于范围的 for 语句[^26]

for 语句的一个常见用途是遍历元素容器。目前，内置数组和库容器的语法不同——内置数组使用索引或原始指针，而容器类使用由 `begin` 和 `end` 成员函数返回的迭代器。新的**基于范围的 for 语句**除了提供更简单的语法外，还允许你对数组和容器使用相同的语法进行遍历。以下代码遍历一组 int 值。

```cpp
for (int &item : items) // items can be an array or container
    item *= 2;
```

## Lambda 表达式[^27]

许多库函数接受函数指针或函数对象作为参数。目前，函数或函数对象必须先定义，然后才能作为实参传递给这些库函数。**Lambda 表达式**（或 lambda 函数）使你能够在将函数对象传递给函数时定义它们。它们在函数内部局部定义，并且可以“捕获”（按值或按引用）外围函数的局部变量，然后在 lambda 函数体中操作这些变量。Lambda

[^22]: Jaakko Järvi、Bjarne Stroustrup 和 Gabriel Dos Reis，“从初始化表达式推导变量类型”，文档编号 N1984=06-0054，2006年4月6日，www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n1984.pdf.

[^23]: Douglas Gregor、Jaakko Järvi 和 Gary Powell，“可变参数模板”，文档编号 N2080-06-0150，2006年9月9日，www.osl.iu.edu/~dgregor/cpp/variadic-templates.pdf.

[^24]: Gabriel Dos Reis 和 Mat Marcus，“向 C++ 添加模板别名的提案”，文档 N1149-03-0032，2003年4月7日，www.open-std.org/jtc1/sc22/wg21/docs/papers/2003/n1449.pdf.

[^25]: J. Stephen Adamczyk、Gabriel Dos Reis 和 Bjarne Stroustrup，“初始化器列表 WP 措辞（修订版 2）”，文档编号 N2531-08-0041，www.open-std.org/jtc1/sc22/wg21/docs/papers/2008/n2531.pdf

[^26]: Thorsten Ottosen，“基于范围的 for 循环措辞（修订版 3）”，文档编号 N2934=07-0254，www.open-std.org/jtc1/sc22/wg21/docs/papers/2007/n2934.html

[^27]: Jaakko Järvi、John Freeman 和 Lawrence Crowl，“Lambda 表达式与闭包：单态 Lambda 的措辞（修订版 4）”，文档编号 N2550=08-0060，www.open-std.org/jtc1/sc22/wg21/docs/papers/2008/n2550.pdf
