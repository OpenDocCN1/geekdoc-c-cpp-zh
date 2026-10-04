
```
cout << "Allocating objects: " << size << " bytes\n";

return ::operator new(size);

}

void operator delete[](void* mem)

{

cout << "Deleting memory at " << mem << ", containing: " <<

::static_cast<int*>(mem) << "\n";

::operator delete(mem);

}

// 类X内部
```

```cpp
int main()

{

try {

X *xp = new X[5];

cout << "Memory at " << xp << '\n';

delete[] xp;

} catch (...) {

cout << "Caught exception.\n";

}

// 此程序的输出（你的 0xXXX 地址地址可能有所不同）

// Allocating objects: 24 bytes

// Object 1

// Object 2

// Destroyed 0x84282010

// Destroyed 0x8428000c

// Deleting memory at 0x8428008, containing: 5

// Caught exception.

}
```

## 11.11 函数对象

函数对象是通过重载函数调用运算符 `operator()` 创建的。通过定义函数调用运算符，对象可以伪装成一个函数，因此，函数对象也被称为仿元函数（functors）。

在使用泛型算法时，函数对象是非常重要的。相比函数指针等替代方案，优于使用函数对象。函数对象在泛型算法内容中的重要性这一事实使我们陷入了教学上的困境。在 C++ 注释中，如果已经涵盖了泛型算法就太好了，因为讨论泛型算法需要关于函数对象的知识。这种“引导启动”问题通过一种众为人知的方法，即暂时忽略这种依赖关系，目前集中在函数概念上。

函数对象是指定义了 `operator()` 的对象。函数对象不仅与泛型算法结合使用，还作为函数指针的（优先）替代方案。

## 11.11 函数对象

函数对象经常用于实现谓词函数。谓词函数返回布尔值。谓词函数和谓词对象通常被称为“谓词”（predicates）。泛型算法（如模板 19 中的 `count_if` 算法）经常使用谓词。标准模板库包含了许多谓词：一元谓词接受一个参数，二元谓词接受两个参数。

假设我们有一个 `Person` 数组，并且假设该数组不是排序的。在数组中查找 `Person` 对象的常用程序是使用 `lsearch` 函数，它在数组中执行线性搜索。示例：

```cpp
Person &target = targetPerson(); // 确定要找的人
Person *pArray;
size_t n = fillPerson(&pArray);
cout << "The target person is";
if (!lsearch(&target, pArray, sizeof(Person), compareFunction))
    cout << "not";
else 
    cout << "found\n";
```

函数 `targetPerson` 决定了我们要找的人，而 `fillPerson` 用于填充数组。然后使用 `lsearch` 来定位目标人物。

比较函数必须可用，因为它的地址是 `lsearch` 参数之一。它必须是一个具有地址的真实函数。如果它被定义为内联（inline），那么编译器只能忽略，因为内联函数没有地址。`CompareFunction` 可以这样实现：

```cpp
int compareFunction(void const *p1, void const *p2)
{
    return *static_cast<Person const*>(p1) // lsearch 想要 0
           !=
           *static_cast<Person const*>(p2); // 用于相等对象
}
```

这假设 `Person` 类中已经重载了 `operator!=`。重载 `operator!=` 并不困难，让我们假设 `operator!=` 实际上可用的。

平均每 2 次发生以下操作：

1. 将比较函数的两个参数推入栈；
2. 确定 `lsearch` 最后一个参数的值，产生 `compareFunction` 的地址；
3. 调用比较函数；
4. 然后，在比较函数内部，将 `Person::operator!=` 右参数的地址推入栈中；
5. 求值 `Person::operator!=`；
6. `Person::operator!=` 的参数从栈中弹出；
7. 比较函数的两个参数从栈中弹出。

使用函数对象会得到一个不同的局面。假设我们构造了一个函数 `PersonSearch`，具有以下原型（然而，这并不是首选方法。目前，泛型算法优于自定义的函数）。但现在我们使用 `PersonSearch` 来说明函数对象的使用和实现：

```cpp
Person const *PersonSearch(Person *base, size_t nmemb, Person const &target);
```

该函数可以如下使用：

```cpp
Person &target = targetPerson();
Person *pArray;
size_t n = fillPerson(&pArray);
cout << "The target person is";
if (!PersonSearch(pArray, n, target))
    cout << " not";
```

到目前为止，变化不大。我们把对 `lsearch` 的调用替换为对另一个函数的调用：`PersonSearch`。现在看 `PersonSearch` 本身：

```cpp
Person const *PersonSearch(Person *base, size_t nmemb, Person const &target);
```

（注：此处原文文本似乎出现了逻辑重复或中断，已根据上下文完成翻译可逻辑部分）

## 11.1.1 构造操作符

在第 6 章中，我们看到了如何构造 `cout << hex << 13` 以十六进制格式显示 13。人们可能会好奇 `hex` 操作符是如何实现这些点的。在本节中将涵盖如 `hex` 等操作符的构造。

实际上操作符的构造非常简单。首先需要定义操作符。假设我们要创建一个 `w10` 操作符，它将 `ostream` 对象写入的下一个字段宽度设置为 10。这个操作符被构造为一个函数。`w10` 函数需要知道设置宽度的 `ostream` 对象。通过为函数提供一个 `ostream&` 参数，它获取了这种知识。现在函数知道了我们所指的 `ostream` 对象，它可以在其中设置宽度。

接下来，必须能够在插入序列中使用操作符。这意味着操作符的返回值必须是 `ostream` 对象的引用。

根据上述内容，我们现在来构造 `w10` 函数：

```cpp
#include <iostream>
#include <iomanip>

std::ostream& w10(std::ostream& str)
{
    return str << std::setw(10);
}
```

# 第 11 章. 更多运算符重载

```cpp
extern ostream &wlo(ostream &str);

int main() {
    wlo(cout) << 3 << " ships sailed to America\n";
    cout << "And " << wlo(cout) << 3 << " more ships sailed too.\n";
}
```

`wlo` 函数可以被用作操作符，因为 `ostream` 类重载了 `operator<<`，能够接受一个指针，该指针指向一个 `ostream &` 并返回一个 `ostream &`。它的定义如下：

```
ostream &operator<<(*func) (ostream &str) {
    return (*func)(str);
}
```

例如 `std::ostream::(*func)(std::ostream &str)` 函数就是 `std::endl` 操作符的签名。

除了重载的 `operator<<` 之外，还定义了另一个

```cpp
ios_base &operator<<((ios_base &(*func)) (ios_base &base)) {
    (*func)(base);
    return *this;
}
```

后者用于插入例如十六进制（hex）或内部格式（internal）。

上述方法对于需要参数的操作符不起作用。当然，可以重载 `operator<<` 来接受一个 `ostream` 引用和一个指向期望 `ostream &` 以及（例如）一个 `int` 的函数的地址，虽然可以通过 `<<-operator` 指定此类函数的地址，但参数本身无法被指定。因此，人们奇奇以下构造是如何实现的：

```cpp
cout << setprecision(3)
```

在这种情况下，该操作符被定义为一个宏。然而，宏是预处理器的范畴，并且很容易受到不受欢迎的副作用的影响。在 C++ 程序中，应尽可能避免使用宏。本节介绍了一种在不诉助于宏的情况下，使用匿名对象来实现需要参数的操作符的方法。

## 11.1.1. 需要参数的操作符

带参数的操作符是以宏的形式实现的；它们由预处理器处理，并且在预处理阶段之后不可用。需要参数的操作符也可以在不使用宏的情况下定义。一种适用于修改全局可用对象（如 `cin` 和 `cout`）的解决方案基于匿名对象：

- 首先，定义一个类，例如 `Align`，其构造函数接收所需的参数。在我们的示例中，分别是字段宽度和对齐类型。
- 该类还支持重载的插入（或提取）运算符。例如，`ostream &operator<<(ostream &str, Align const align)`。
- 接下来，将（匿名）对象插入到流中。插入运算符将流传递给 `Align::align`，允许成员函数配置（并返回）提供的流。

下面是这种期望多个参数的自定义操作符的示例：

```cpp
#include <iostream>
#include <iomanip>

class Align
{
    unsigned d_width;
    std::ios::fmtflags flags;

public:
    Align(unsigned width, std::ios::fmtflags alignment);
    std::ostream& operator()(ostream &str) const;
};

Align::Align(unsigned width, std::ios::fmtflags alignment)
    : d_width(width), flags(alignment) {}

std::ostream &Align::operator()(ostream &str) const
{
    str.setf(flags);
    return str << std::setw(d_width);
}

std::ostream&operator<<(ostream &str, Align const align)
{
    return align(str);
}

using namespace std;

int main()
{
    cout << Align(5, left) << "hi"
         << Align(10, right) << "there" << "\n";
}
```

生成的输出：

```
hi there
```

当必须操作（局部）对象时，该类必须考虑将函数调用运算符作为所需的参数。例如，一个 `Matrix` 类应该允许用户在将矩阵插入到 `ostream` 时指定值分隔符和行分隔符。定义了两个数据成员（例如 `char const *d_valueSep` 和 `char const *d_lineSep`）并将其初始化为可接受的值。插入函数在值之间插入 `d_valueSep`，在插入的行末尾插入 `d_lineSep`。`operator()(char const *valueSep, char const *lineSep)` 简单地将值分配给相应的数据成员。

给定一个对象矩阵，此时可以调用 `matrix(" ", "\n")`。该函数调用运算符不应该插入矩阵，因为操作符的责任是不插入；因此，要插入矩阵，可能应该使用这样的语句：

```cpp
cout << matrix(" ", "\n");
```

操作符（即函数调用运算符）将适当的值分配给 `d_valueSep` 和 `d_lineSep`，这些值将在实际插入期间被使用。

函数调用运算符的返回值仍待确定。返回值应该是可插入的，但实际上不应该插入任何内容。可以返回一个空的 OTS（输出流类型），但这有点权宜之计。相反，可以返回一个不执行任何操作的操作符的地址。以下是这种空操作符的实现：

```cpp
// 静态（或者也可以使用自由函数）
std::ostream &Matrix::nop(ostream &out)
{
    return out;
}
```

因此，`Matrix` 操作符的实现变为：

```cpp
std::ostream &
*Matrix::operator()(char const *valueSep, char const *lineSep)(ostream &str)
{
    d_valueSep = valueSep;
    d_lineSep = lineSep;
    return nop(str);
}
```

或者（取决于个人口味），返回一个空函数操作符的地址可以先设置所需的插入特定值，然后返回自身：`Matrix` 将被插入到分配给插入变量的值：

```cpp
Matrix const &Matrix::operator()(char const *valueSep, char const *lineSep)(ostream &str)
{
    d_valueSep = valueSep;
    d_lineSep = lineSep;
    return *this;
}
```

在这种情况下，插入语句被简化为

```cpp
cout << matrix(" ", "\n") << '\n";
```

## 11.12 Lambda 表达式

C++ 支持 lambda 表达式。正如我们在 19 章中将看到的，泛型算法通常接受函数对象或普通函数作为参数。例如 `sort`（参见 19.1.54 节）和 `find_if`（参见 19.1.15 节）泛型算法。准则是：当函数需要记住状态时，函数对象是合适的，否则可以使用普通函数。

通常，函数或函数对象并不容易获取，它们必须在使用的位置附近定义。这通常通过在匿名命名空间中定义（例如：类或函数 A）来实现，并将 A 传递给需要它的代码。如果该代码本身是类 B 的成员函数，那么 A 的实现可能会从访问 B 的成员中受益。

### 11.12.1 Lambda 表达式：语法

lambda 表达式被求值后产生一个临时函数对象（闭包对象），或简单的闭包。

当 lambda 表达式位于块、类或命名空间内部时（即几乎任何地方），它们的隐含闭包类型定义在包含 lambda 表达式的最小作用域中。闭包的可见性从其定义点开始，到闭包类型结束（即其可见性与普通变量的可见性相同）。

闭包类型定义了一个公共的 lambda 引入符内联函数调用运算符。这里有一个 lambda 表达式的示例：

```cpp
[] // lambda 引入符
(int x, int y) // lambda 声明符
{
    return x * y; // 的复合语句
}
```

# 第 11 章 更多运算符重载

该函数（正式名称：由此 lambda 表达式创建的闭包类型的调用运算符）调用 `int` 类型参数并返回它们的乘积。该函数是其闭包类型的一个内联 `const` 成员。如果 lambda 表达式指定了 `mutable`，其 `const` 属性会被移除。例如：

```cpp
[](int x, int y) mutable
```

如果没有定义参数，可以省略 lambda 声明符（lambda-declarator），但在指定 `mutable`（或 `constexpr`，见下文）时必须指定 lambda 声明符（至少是一组空括号）。lambda 声明中的参数不能有默认参数。

指定符可以是 `mutable`、`constexpr` 或两者兼有。`constexpr` lambda 表达式本身是 `constexpr` 的，如果参数符合 `const` 条件，则可以在编译时求值。由此推导，如果 lambda 表达式定义在 `constexpr` 函数内部，那么 lambda 表达式本身就是 `constexpr`，并且不需要 `constexpr` 声明符指定符。因此，以下函数是等价：

```cpp
int constexpr change10(int n)
{
    return [n]
    {
        return n > 10 ? n : n + 10;
    };
}

int constexpr change10(int n)
() constexpr
{
    return [n]
    {
```
