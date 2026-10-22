
当该引用是传统的隐式 `*this` 参数时，绑定到非 const 类型的左值引用是允许的；但如果显式请求了左值引用处理，则这种（有点危险的）特殊情况不再适用。因此，按上面给出的 `S` 定义：

```
int main()
{
    S().f1(); // OK: old rule allows rvalue S() to match implied
              // lvalue reference type S& of *this
    S().f2(); // OK: rvalue S() matches rvalue reference type
              // of *this
    S().f3(); // ERROR: rvalue S() cannot match explicit lvalue
              // reference type of *this
}
```

### C.2.2 细化完美匹配

对于类型为 `X` 的参数，有四种常见的参数类型构成完美匹配：`X`、`X&`、`X const&` 和 `X&&`（`X const&&` 也是精确匹配，但很少使用）。然而，在两种引用类型上重载函数是很常见的。在 C++11 之前，这意味着如下情况：

```
void report(int&);       // #1
void report(int const&); // #2

int main()
{
    for (int k = 0; k < 10; ++k) {
        report(k);  // calls #1
    }
    report(42);     // calls #2
}
```

这里，没有额外 `const` 的版本对于左值是首选的，而只有带 `const` 的版本才能匹配右值。

随着 C++11 中右值引用的引入，另一个需要区分两个完美匹配的常见情况如下例所示：

```
struct Value {
    ...
};
void pass(Value const&); // #1
void pass(Value&&);      // #2

void g(X&& x)
{
    pass(x);             // calls #1, because x is an lvalue
    pass(X());           // calls #2, because X() is an rvalue (in fact, prvalue)
    pass(std::move(x));  // calls #2, because std::move(x) is an rvalue (in fact, xvalue)
}
```

这一次，接受右值引用的版本被认为是右值的更好匹配，但它不能匹配左值。

注意，这也适用于成员函数调用的隐式参数：

```
class Wonder {
public:
    void tick();       // #1
    void tick() const; // #2
    void tack() const; // #3
};

void run(Wonder& device)
{
    device.tick(); // calls #1
    device.tack(); // calls #3, because there is no non-const version
                   // of Wonder::tack()
}
```

最后，对我们之前示例的以下修改说明，如果在有无引用的情况下进行重载，两个完美匹配也可能产生歧义：

```
void report(int);       // #1
void report(int&);      // #2
void report(int const&); // #3

int main()
{
    for (int k = 0; k < 10; ++k) {
        report(k);  // ambiguous: #1 and #2 match equally well
    }
    report(42);     // ambiguous: #1 and #3 match equally well
}
```

## C.3 重载细节

上一节涵盖了日常 C++ 编程中遇到的大多数重载情况。不幸的是，这些规则还有更多的规则和例外——比一本并非专门讨论 C++ 函数重载的书所合理呈现的还要多。尽管如此，我们在这里讨论其中一些，部分原因是它们比其他规则更常适用，部分原因是让读者了解细节的深度。

### C.3.1 优先选择非模板或更特化的模板

当重载决议的所有其他方面都相同时，非模板函数优先于模板实例（无论该实例是从通用模板定义生成的，还是作为显式特化提供的，都没有关系）。例如：

```
template<typename T> int f(T); // #1
void f(int);                   // #2

int main()
{
    return f(7); // ERROR: selects #2, which doesn’t return a value
}
```

这个例子也清楚地说明了重载决议通常不涉及所选函数的返回类型。

然而，当重载决议的其他方面略有不同（例如具有不同的 `const` 和引用限定符）时，首先适用重载决议的一般规则。当成员函数被定义为接受与复制或移动构造函数相同的参数时，这种效应很容易意外地导致令人惊讶的行为。详见第 333 页第 16.2.4 节。

如果在两个模板之间进行选择，则更特化的模板会被优先考虑（前提是其中一个确实比另一个更特化）。关于这一概念的详细解释，请参见第 330 页第 16.2.2 节。这种区别的一个特殊情况是：两个模板仅在其中一个添加了尾随参数包时不同。没有参数包的模板被认为更特化，因此如果它匹配调用，则会被优先选择。第 57 页第 4.1.2 节讨论了这种情况的一个示例。

### C.3.2 转换序列

一般来说，隐式转换可以是基本转换的序列。考虑以下代码示例：

```
class Base {
public:
    operator short() const;
};

class Derived : public Base {
};

void count(int);

void process(Derived const& object)
{
    count(object); // matches with user-defined conversion
}
```

调用 `count(object)` 之所以有效，是因为 `object` 可以隐式转换为 `int`。然而，这种转换需要几个步骤：

1. 将 `object` 从 `Derived const` 转换为 `Base const`（这是一个 glvalue 转换；它保留了对象的身份）
2. 将得到的 `Base const` 对象通过用户定义转换转换为 `short` 类型
3. 将 `short` 提升为 `int`

这是最一般的转换序列：一个标准转换（本例中是派生类到基类的转换），紧接着一个用户定义转换，再紧接着另一个标准转换。虽然一个转换序列中最多只能有一个用户定义转换，但也可能只包含标准转换。

重载决议的一个重要原则是：一个转换序列如果是另一个转换序列的子序列，则优于后者。如果例子中还有一个候选函数 `void count(short);`，那么对于调用 `count(object)` 来说它会被优先选择，因为它不需要转换序列中的第三步（提升）。

### C.3.3 指针转换

指针和成员指针会经历各种特殊的标准转换，包括：

- 转换为 `bool` 类型
- 从任意指针类型转换为 `void*`
- 指针的派生类到基类转换
- 成员指针的基类到派生类转换

尽管所有这些都可能导致“仅通过标准转换匹配”，但它们的优先级并不相同。

首先，转换为 `bool` 类型（无论是从普通指针还是从成员指针）被认为比其他任何标准转换都差。例如：

```
void check(void*); // #1
void check(bool);  // #2

void rearrange(Matrix* m)
{
    check(m); // calls #1
    ...
}
```

在普通指针转换的类别中，转换为 `void*` 类型被认为比从派生类指针到基类指针的转换更差。此外，如果存在转换为通过继承关联的不同类的情况，则优先选择转换为最派生的类。下面是另一个简短示例：

```
class Interface {
    ...
};

class CommonProcesses : public Interface {
    ...
};

class Machine : public CommonProcesses {
    ...
};

char* serialize(Interface*);       // #1
char* serialize(CommonProcesses*); // #2

void dump(Machine* machine)
{
    char* buffer = serialize(machine); // calls #2
    ...
}
```

从 `Machine*` 到 `CommonProcesses*` 的转换优先于到 `Interface*` 的转换，这是相当直观的。

一个非常相似的规则适用于成员指针：在相关成员指针类型的两次转换之间，继承图中“最近的基类”（即派生程度最低的）会被优先选择。

### C.3.4 初始化列表

初始化列表参数（以花括号传递的初始化器）可以转换为几种不同类型的参数：初始化列表、具有 `initializer_list` 构造函数的类类型、初始化列表元素可以被视为构造函数的（单独）参数的类类型，或其成员可以由初始化列表元素初始化的聚合类类型。以下程序说明了这些情况：

*overload/initlist.cpp*

```
#include <initializer_list>
#include <string>
#include <vector>
#include <complex>
#include <iostream>

void f(std::initializer_list<int>) {
    std::cout << "#1\n";
}

void f(std::initializer_list<std::string>) {
    std::cout << "#2\n";
}

void g(std::vector<int> const& vec) {
    std::cout << "#3\n";
}

void h(std::complex<double> const& cmplx) {
    std::cout << "#4\n";
}

struct Point {
    int x, y;
};

void i(Point const& pt) {
    std::cout << "#5\n";
}

int main()
{
    f({1, 2, 3});               // prints #1
    f({"hello", "initializer", "list"}); // prints #2
    g({1, 1, 2, 3, 5});         // prints #3
    h({1.5, 2.5});              // prints #4
    i({1, 2});                  // prints #5
}
```
