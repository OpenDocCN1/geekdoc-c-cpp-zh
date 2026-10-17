
```cpp
catch (my_error &eObj) { // 异常声明为引用
    eObj.status = severeErr; // 修改异常
    throw; // 重新抛出
} catch (other_error eObj) { // 异常是非引用类型
    eObj.status = badErr; // 修改本地拷贝
    throw; // 异常对象保持不变
}
```

## 通能捕获处理器 (Catch-All Handler)

有时我们想要捕获可能发生的任何异常，无论其类型。捕获所有可能的异常可能是一个问题：即使我们知道所有的类型，为每种类型提供特定的 `catch` 可能很麻烦。为了捕获所有异常，我们在异常声明中使用省略号。此类处理器被称为通能处理器，形式为 `catch(...)`。匹配任何类型的异常。

[点击此处查看代码图像]

```cpp
void manip() {
  try {
    // 导致异常发生的操作
  } catch (...) {
    // 部分处理异常
    throw;
  }
}
```

`catch(...)` 子句可以单独使用，也可以作为多个 `catch` 子句之一。

> **注意**

如果 `catch(...)` 与其他 `catch` 子句一起使用，它必须放在最后。位于通能 `catch` 之后的永远无法被匹配。

## 18.1.3. 函数 try 块与构造函数

通常情况下，异常可以在程序执行的任何点发生。特别是，异常可能会在构造初始化期间发生。构造体内部的 `catch` 无法处理构造初始化抛出的异常，因为构造体内部的 `try` 块尚未生效。

## 练习 18.1.2 节

练习 18.4：查看图 18.1 (p. 783) 中的继承层次结构，解释以下 `try` 块的错误所在。修正它。

[点击此处查看代码图像]

```cpp
try {
    // 使用 C++ 库
} catch(exception) {
    // ...
} catch(const runtime_error &re) {
    // ...
} catch(overflow_error eobj) { /* ... */ }
}
```

![](img/3a7e14b77396239ca716fc2adb32975_954_0.png)

图 18.1 标准异常类层次

练习 18.5：修改下面的 `main` 函数以捕获图 18.1 (p. 783)所示的任何异常类型：

[点击此处查看代码图像]

```cpp
int main() {
    // 使用 C++ 标准库
}
```

处理程序应该在调用 `abort`（定义在头文件 `<cstddef>` 中）终止 main 之前打印与异常相关的错误消息。

练习 18.6：给定以下异常类型和 `catch` 子句，写一个 `throw` 表达式，创建一个可以被每个 `catch` 子句捕获的异常对象：

- **a)** class `exceptionType` { }; `catch(exceptionType *pet)` {}

- **(b)** `catch(...)` {}

- **(c)** `typedef int EXCPTYPE`;

```cpp
catch (EXCPTYPE) { 
```

为了处理来自构造函数初始化列表的异常，我们必须将构造函数写在一个 `try` 块中。函数 `try` 块允许我们将一组 `catch` 子句与构造函数的初始化阶段（或析构函数的析构阶段）以及构造函数（或析构函数）的函数体关联起来。例如，我们可以将 `Blob` 构造函数（§ 16.1.2,，第 662 页）封装在一个函数 `try` 块中：

# 点击此处查看代码图片

```cpp
template <typename T>
Blob<T>::Blob(initializer_list<T> il) : 
		data(std::make_shared<std::vector<T>>(il)) {
		/* 空函数体 */
	} catch(const std::bad_alloc&, handle_out_of_memory&);
```

注意，`try` 关键字出现在起始构造函数初始化列表的冒号之前，以及出现在形成（在本例中为空的）构造函数函数体的大括号之前。与此 `try` 关联的 `catch` 可用于处理从成员初始化列表抛出的异常，或从构造函数体内部抛出的异常。

值得注意的是，在初始化构造函数参数时可能会发生异常。此类异常*不是*函数 `try` 块的一部分。`try` 块只处理一旦构造函数开始执行后发生的异常。对于任何其他函数调用，如果在参数初始化期间发生异常，则该异常是调用表达式的一部分，并在调用者的上下文中被处理。

> 注意

 构造函数处理来自构造函数初始化列表异常的唯一方法是将构造函数写成一个函数 `try` 块。

## 练习章节 18.1.3

练习 18.7：定义第 16 章中定义的 `Blob` 和 `BlobPtr` 类，为它们的构造函数使用函数 `try` 块。

## 18.1.4. noexcept 异常规范

对于用户和编译器来说，知道一个函数不会抛出任何异常是有帮助的。知道函数不会抛异常简化了调用该函数的代码编写。此外，如果编译器知道不会抛出异常，它就可以（有时）执行某些必须对可能抛出异常的代码进行抑制的优化。

C++ 11

在新标准下，函数可以通过提供 `noexcept` 规范来指定它不抛出异常。函数参数列表后的 `noexcept` 关键字表示不会抛出异常的函数：

点击此处查看代码图片

```cpp
void recoup(int) noexcept;   // 不抛出
void alloc(int);             // 可能会抛出
```

这些声明表示 `recoup` 不抛出任何异常，而 `alloc` 可能会。我们说 `recoup` 具有一个**不抛出规范**。

`noexcept` 规范必须出现在函数的所有声明和相应的定义中，或者全一个都不出现。该规范出现在末尾的波浪号（6.3.3,，第 229 页）之前。我们还可以在函数指针的声明和定义中指定 `noexcept`。它不可以出现在 `typedef` 或类型别名中。在成员函数中，`noexcept` 规范位于任何 `const` 或引用修饰符之后，并位于虚函数的 `final`、`override` 或 `= 0` 之前。

## 违反异常规范

重要一点是，编译器在编译时并不检查 `noexcept` 规范。事实上，编译器不允许仅仅因为一个带有 `noexcept` 规范的函数包含 `throw` 或调用了可能抛出异常的函数就拒绝该函数（尽管某些友好的编译器会对此类用法发出警告）：

点击此处查看代码图片

```cpp
// 此函数将通过编译，尽管它显然违反了它的异常规范
void f() noexcept                // 承诺不抛出任何异常
{
    throw exception(); // 违反了异常规范
}
```

结果是，如果 `noexcept` 函数在参数初始化期间发生异常，该异常是调用表达式的一部分，并在调用者的上下文中被处理。但是，如果 `noexcept` 函数在运行时抛出异常，将调用 `terminate`。因此，`noexcept` 应该在以下情况下使用：如果我们确定函数不会抛出异常，或者我们不确定是否会抛出异常。`noexcept` 规范是调用者可以信任的，即使函数是抛出异常的。

> 警告

 编译器通常不会在运行时验证 `noexcept` 规范。

## 后兼容性：异常规范

早期的 C++ 版本中，异常规范允许 `throw`  own函数可能会抛出异常。`noexcept` 规范在虚函数中广泛使用，如果基类允许抛出异常：

点击此处查看代码图片

```cpp
class Base {
public:
    virtual double f1(double) noexcept; // 不抛出
    virtual int f2(int) noexcept(false); // 可能抛出
    virtual void f3(); // 可能抛出
};

class Derived : public Base {
public:
    double f1(double); // 错误：Base::f1 承诺不抛出
    int f2(int) noexcept(false); // 正确：与Base::f2相同
    void f3() noexcept; // 正确：Derived f3 限制性更
};
```

## noexcept 运算符

`noexcept` 运算符可以用于指定函数是否会抛出异常。`noexcept` 运算符在函数参数列表之后，表示该函数不会抛出异常。如果如果构造构造函数函数调用的任何操作可能抛出异常，那么该函数就是 `noexcept(false)`。的，抛出：

```cpp
// 不抛出
noexcept(true); // 可能会抛出
```

## noexcept 运算符

`noexcept` 运算符可以用于指定函数是否会抛出异常。`noexcept` 运算符在函数参数列表之后，表示该函数不会抛出异常。如果构造构造构造函数调用的任何操作可能抛出异常，那么该函数就是 `noexcept(false)`。的，抛出：

```cpp
// 不抛出
noexcept(true); // 可能会抛出
```

标准库异常类（§ 5.6.3，第 197 页）构成了图 18.1 所示的继承体系（第 15 章）。

异常类型定义的唯一操作是拷贝构造函数、拷贝赋值运算符、一个虚析构函数和一个名为 `what` 的虚成员函数。`what` 函数返回一个指向以空结尾的字符数组的 `const char*`，并保证不会抛出任何异常。

`bad_cast` 和 `bad_alloc` 类还定义了默认构造函数。`runtime_error` 和 `logic_error` 类没有默认构造函数，但接受一个 C 字符字符串或 `string` 参数。这些参数旨在提供有关错误的额外信息。在这些类中，`what` 返回用于初始化异常对象时所使用的消息。由于 `what` 是虚函数，如果我们捕获的是基类类型的引用，调用 `what` 函数将执行与异常对象的动态类型相对应的版本。

## 书店应用程序的异常类

应用程序通常通过派生 `exception`（或派生自 `exception` 的库类）来扩展异常层次结构。这些特定于应用程序的类表示特定于应用程序领域的异常情况。

如果我们正在构建一个真实的书店应用程序，我们的类将比本《入门教程》中展示的复杂得多。其中一个复杂性就是这些类如何处理异常。事实上，我们可能会定义自己的异常层次结构来表示特定于应用程序的问题。我们的设计可能包含如下类：

点击此处查看代码图像

```
// 书店应用程序的假设异常类
class out_of_stock: public std::runtime_error {
public:
    explicit out_of_stock(const std::string& s):
        std::runtime_error(s) {}
};
class isbn_mismatch: public std::logic_error {
public:
    explicit isbn_mismatch(const std::string& s):
        std::logic_error(s) {}
    isbn_mismatch(const std::string& lhs, const std::string& rhs):
        std::logic_error(left(lhs), right(rhs)) {}
    const std::string& left, right;
};
```

我们的特定应用程序异常类型继承自标准异常类。与任何层次结构一样，我们可以认为异常类被组织成不同的层。随着层次结构的加深，每一层都变成更具体的异常。例如，层次结构的第一层也是最通用的层由 `exception` 类表示。我们所知道的捕获一个 `exception` 类型的对象意味着发生了某些错误。

第二层将 `exception` 细化为两类：运行时错误或逻辑错误。运行时错误是那些在程序执行时可以检测到的错误。逻辑错误从原则上说是在我们可以在应用程序中本可以检测到的错误。

我们的书店异常类进一步细化了这些类别。名为 `out_of_stock` 的类代表我们应用程序特有的、可以在运行时发生的错误。它被用于信号订单无法交付。`isbn_mismatch` 类代表 `logic_error` 的更具体的形式。原则上讲，程序可以通过比较对象上 `isbn()` 的结果来预测并处理这种错误。

## 使用自定义异常类型

我们使用异常类的方式与使用标准库类相同。程序的一个部分抛出这些类型之一的对象，另一部分则捕获并处理指示出的问题。例如，我们可能会为 `Sales_data` 类定义复合加运算符，如果检测到 ISBN 不匹配，则抛出 `isbn_mismatch` 类型的异常：

点击此处查看代码图像

```
// 如果两个对象不引用同一本书，则抛出异常
Sales_data&
Sales_data::operator+=(const Sales_data& rhs)
{
    if (isbn() != rhs.isbn())
        throw isbn_mismatch("wrong isbns: ", isbn(), rhs.isbn());
    units_sold += rhs.units_sold;
    revenue += rhs.revenue;
    return *this;
}
```

使用复合加运算符（或普通加运算符，后者本身使用复合加运算符）的代码可以检测到这种错误，编写适当的错误信息并继续执行：

点击此处查看假设的异常

```
// 使用假设的书店异常
Sales_data item1, item2, sum;
while (cin >> item1 >> item2) { // 读取两次交易
    try {
        sum = item1 + item2; // 计算它们的和
// 使用 sum
} catch (const isbn_mismatch &e) {
    cerr << e.what() << " " << left isbn(" << e.left << ") " << right isbn(" << e.right << ")" << endl;
}
```

## 练习第 18.5 版

**练习 18.9：** 定义本节描述的书店异常类，并重写你使用的 `Sales_data` 复合赋值运算符以抛出异常。

**练习 18.10：** 编写一个程序，在具有不同 ISBN 的对象上使用 `Sales_data` 加运算符。编写两个版本的程序：一个处理异常，另一个不处理。比较两者的行为，以便熟悉当发生未捕获异常时发生的情况。

**练习 18.11：** 为什么 `what` 函数不抛出异常很重要？

## 18.2 命名空间

大型程序倾向于使用独立开发的库。这些库倾向于定义大量的全局名称，例如类、函数和模板。当应用程序使用多个供应商的库时，这些名称冲突几乎不可避免。将名称放入全局命名空间的库被称为命名空间污染。传统上，程序员通过使用长名称来避免命名污染。这些名称通常包含指示哪个库定义的：

点击此处查看代码图像

```
class plus_primer_Query { ... };
string plus_primer_make(size_t, string&);
```

这种解决方案远非理想：对于编写和阅读使用此类名称的程序来说。

命名空间为防止命名冲突提供了更有效的机制。命名空间划分了全局命名空间。命名空间是一个作用域。通过在命名空间内定义库名称，库作者（以及用户）可以避免限制。

### 18.2.1 命名空间定义

命名空间定义以 `namespace` 关键字开头，后跟命名空间名称。命名之后是由花括号分隔的声明和定义。任何可以在全局作用域出现的声明都可以放入命名空间中：类、变量（带有初始化）、函数（带有定义）、模板和其他命名空间：

点击此处查看代码图像

```
namespace plus_primer {
    class Sales_data { /* ... */ };
    Sales_data operator+(const Sales_data&,
                         const Sales_data&);
    class Query { /* ... */ };
    class Query_base { /* ... */ };
} // 与块一样，命名空间不需要分号结尾
```

这段代码定义了一个名为 `plus_primer` 的命名空间，包含四个成员：三个类和一个重载运算符。

与任何名称一样，命名空间名称在定义的作用域内必须是唯一的。命名空间可以定义在全局作用域或另一个命名空间内部。它们不能定义在函数或类内部。

> 注意

命名空间作用域不以分号结尾。

### 每个命名空间都是作用域

与任何作用域一样，命名空间中的每个名称必须指向该命名空间内的唯一实体。由于不同的命名空间引入了不同的作用域，不同的命名空间可以具有相同的成员。

命名空间定义的名称可以通过命名空间其他成员直接访问，包括嵌套在其内部的作用域。命名空间外部的代码必须指示名称所在的命名空间：

点击此处查看代码图像

```
plus_primer::Query q =
    plus_primer::Query("hello");
```

如果另一个命名空间（例如，AddisonWesley）提供了 `Query` 类，且我们想使用它代替 `plus_primer` 中定义的类，我们可以通过如下修改代码来实现：

AddisonWesley::Query q = AddisonWesley::Query("hello");

# 命名空间是非连续的

正如我们在 § 16.5 (709) 中看到的，与其他作用域不同，命名空间可以在几个部分定义。编写命名空间定义：

```cpp
namespace nsp {
    // 声明
}
```
