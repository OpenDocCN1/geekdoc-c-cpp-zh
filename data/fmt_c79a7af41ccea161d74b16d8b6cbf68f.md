
注意，这个类只包含函数原型（或函数声明）。成员函数的实际实现将在类声明之外。尽管如此，类声明也可以包含函数实现。

在类内部声明的函数被称为成员函数或方法。成员函数可以访问其所属类的任何其他成员。

这包含了所有私有元素。

类声明中的成员数据变量具有一些局限性：

- 成员变量不能被声明为 `extern` 或 `register` 变量。
- 非静态成员变量不能通过赋值进行初始化（在类中声明它的点）。

作为一个一般规则，我们应该强制执行数据的封装。也就是说，类中的所有数据成员都应该声明为 `private`。

## 访问公共成员

访问公共成员的语法如下：指定对象的名称，然后是点运算符 `.`，最后是成员变量或成员函数。

```cpp
#include <iostream>
using namespace std;

class Foo {
public:
    // 这些数据变量整个程序都可以访问
    int i, j, k;
};

int main() {
    Foo a, b;
    // 访问 i, j 和 k 是允许的
    a.i = 100;
    a.j = 4;
    a.k = a.i * a.j;

    b.k = 12; // 不同的类实例

    cout << a.k << " " << b.k;
    return 0;
}

// 输出
400 12
```

## 作用域解析运算符

`::` 作用域运算符将成员与类名关联。它告诉编译器该成员属于哪个类。作用域解析运算符还有另一个用途：它可以允许访问某些作用域内的名称。这允许访问某些作用域内与本地声明同名的名称。

下面的示例展示了它是如何工作的：

```cpp
int i;      // 全局变量 i
void f() {
    int i;      // 局部变量 i
    i = 10;     // 使用局部 i
}

void g() {
    int i;      // 局部变量 i
    ::i = 10;    // 指向全局变量 i
}
```

## 类函数实现

考虑以下类规范：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

class Foo {
public:
    void buildstr(char *s);
    void showstr();

private:
```

```cpp
char str[255];

void Foo::buildstr(char *s) {
  // 初始化成员字符串变量
  strcpy(str, s);
}

void Foo::showstr() {
  cout << str << "\n";
}
```

此示例中的类仅包含类成员函数的原型。类类函数的实现位于类之后，并使用作用域解析运算符来识别每个函数所属的类。这是类的声明方式。然而，我们可以在类内部提供函数实现。

## 静态类成员

类的成员函数和成员变量可以声明为 `static`。静态成员由该类的所有实例共享。适用以下限制：

- 静态成员函数只能引用该类的其他静态成员函数和静态数据成员。
- 静态成员函数没有 `this` 指针。
- 我们不能让同一个成员函数拥有静态和非静态的版本。
- 静态函数不能声明为具有 `const` 或 `volatile` 属性。

以下是一个示例：

```cpp
#include <iostream>
using namespace std;

class Foo
```

```cpp
static int resource;
public:
    static int get_resource();
    void free_resource() { resource = 0; }
};
```

```cpp
int Foo::resource = 0; // 初始化 resource

int Foo::get_resource() {
    if(resource)
        return 0;
    else
        {
            resource = 1;
            return 1;
        }
}
```

```cpp
int main() {
    int ret = Foo::get_resource();
    cout << "resource = " << ret << endl;
    return 0;
}
```

```cpp
// 输出
resource = 1
```

注意此示例中 `Foo` 没有被实例化。

## 对象赋值

假设两个对象是相同类型，我们可以使用常用的赋值运算符 `=` 将一个对象赋值给另一个对象。这会导致右侧的数据按位拷贝到左侧的对象中。

## 局部类

局部类是在函数内部定义的类。下面的示例在函数内部内部定义了一个类：

```cpp
#include <iostream>
using namespace std;

// 函数 f 的前声明
void f();

int main()
{
    f();
    return 0;
}
```

```cpp
void f()
{
    // 在 f 内部定义一个局部类
class Foo {
    int i;
    public:
    void put_i(int n) { i=n; }
    int get_i() { return i; }
}

Foo foo;

```

```cpp
foo.put_i(10);
cout << "foo i data member = " << foo.get_i() << endl;
```

```cpp
// 输出
foo i data member = 10
```

对局部类的使用有严格的限制：

- 所有成员函数必须在类声明内部定义。
- 局部类可能访问其定义处函数中的任何局部变量；在函数内部声明的静态变量除外。
- 局部类内部不能声明静态变量。

局部类可以访问 `typedef` 和。

## C++ 命名空间

命名空间的目的是将名称局部化以避免冲突。在命名空间发明之前，如果我们的程序定义了一个函数，可能会发生冲突。命名空间通过将名称局部化到它们声明的作用域来解决这个问题。这允许在不同的上下文中中使用相同的名称。命名空间通过创建区域来允许我们划分全局命名空间。

如果我们的程序定义了一个名为 `abs()` 的函数，可能会覆盖标准库函数，因为它们都在全局命名空间中。命名空间的创建解决了这个问题。命名空间允许在不同的上下文中使用相同的名称。

命名namespace的语法如下：

```cpp
namespace name {
// 声明
}
```

命名空间内任何名称的可见性限于其定义的作用域。

```cpp
namespace counter_namespace {
int upperbound;
int lowerbound;
class Counter {
int count;
public:
counter(int n) {
    if(n <= upperbound)
        count = n;
    }
}
```

```cpp
else
    count = upperbound;
}
void reset(int n)
{
    if(count > lowerbound)
        return count--;
    else
        return lowerbound;
}
```

这里 `upperbound`、`lowerbound` 和 `Counter` 类的可见性限于 `counter_namespace`。

命名空间块内部定义的标识符可以在没有任何命名限定的情况下引用。例如，在 `counter_namespace` 内部，`run()` 函数可以直接引用 `lowerbound`。然而，由于命名空间定义了作用域，我们需要使用作用域运算符来从外部引用命名空间内声明的对象。

例如，从 `counter_namespace` 外部为 `upperbound` 赋值 10，我们必须使用作用域运算符：

```cpp
counter_namespace::upperbound = 10;
```

并且从 `counter_namespace` 外部声明 `Counter` 类型的对象，我们使用：

```cpp
counter_namespace::Counter foo;
```

## 全局命名空间

如果标识符没有在任何命名空间定义，它是全局命名空间的一部分。通常，我们应该避免在全局命名空间中进行声明，入口函数 `main` 必须在全局命名空间中。

要使用全局命名空间中的标识符如 `someFunction()`，我们使用没有任何前缀的作用域运算符，例如：

```cpp
::someFunction(x);
```

## 最佳实践

当你想引用全局变量（它在全局命名空间中）时，在变量前加上作用域运算符。这将让我们知道变量定义在全局命名空间中。示例：

```cpp
foo(int x) {
  return x + ::y;
}
```

## 将标识符引入作用域

我们可以通过使用作用域运算符限定标识符将其引入另一个命名空间的作用域中。语法如下：

```cpp
void foo() {
  std::cout << std::string("Hello World");
}
```

这会将 `std` 命名空间中的 `cout` 和 `string` 引入作用域。

### 命名空间：using 指令

如果我们的程序频繁引用命名空间中的标识符，那么每次引用这些标识符时都要指定命名空间和作用域解析运算符，很快就会变得繁琐。`using` 语句缓解了这个问题。`using` 语句有两种通用的形式：

```
using namespace foo;
using foo::bar;
```

在第一种形式中，`foo` 指定我们想要访问的命名空间名称。`foo` 命名空间内定义的所有成员都被引入作用域（它们成为当前命名空间的一部分），并且可以使用而不带作用域解析运算符（例如使用 `vector` 而不是 `std::vector`）。在第二种形式中，只有 `foo` 命名空间中的特定成员 `bar` 被引入作用域。

假设如所示 `counter_namespace`，以下 `using` 语句和赋值是有效的：

```
// 只有 lowerbound 可见
using counter_namespace::lowerbound;

// OK，因为 lowerbound 在当前作用域内是的
lowerbound = 10;
```

### using namespace 的危险

在头文件中声明 `using namespace <some identifier>` 被认为是一种不良实践，因为会将该命名空间引入整个程序中。

在实现文件中声明 `using namespace` 也不被推荐，因为可能会导致非常难以调试的歧义（ambiguity）。考虑这个示例：

```
#include <iostream>

namespace my_library {
    double calculate(double x) { return x + x; }
}

namespace foreign_lib {
    int calculate(int x) { return x + x; }
}

using namespace my_library;
using namespace foreign_lib;

int main() {
    calculate(2);
    calculate(2.3);
}
```

这段代码的问题在于，调用的 `calculate` 版本取决于 `calculate` 参数的类型。这可能会在程序中引入非常难以追踪的错误。

最佳实践是始终为标识符加上命名空间前缀。

## 匿名命名空间

有一种特殊的命名空间类型称为匿名命名空间（unnamed namespace），它允许我们创建在命名空间内唯一且在命名空间外不可见的标识符。

匿名命名空间也称为匿名命名空间（anonymous namespaces）。它们具有以下语法：

```
namespace {
    // declarations
}
```

匿名命名空间允许我们建立仅在命名空间作用域内已唯一标识符。考虑一个内容被匿名命名空间封装的文件。在包含该匿名命名空间的文件内部，命名空间的成员可以直接使用而无需限定。但在文件外部，这些标识符是未知的且无法被访问的。

## 合并命名空间

可以有多个相同（命名空间）名称的命名空间声明。这允许将命名空间拆分到多个文件中，甚至在文件中拆分开。

```
#include <iostream>
using namespace std;

namespace NS {
int i;
}

// 间隙代码
namespace NS {
int j;
}
int main() {
NS::i = NS::j = 10;

// 特别地引用 NS
cout << NS::i * NS::j << endl;

// 使用 NS 命名空间
using namespace NS;
cout << i * j << endl;
}

// 输出
100
```

在这个示例中，命名空间 `NS` 被分成了两个部分。然而，每个部分的内容仍然同一个命名空间 `NS` 中。

命名空间可以嵌套在另一个命名空间内部。但是，命名空间不能声明在函数体内部。不过我们可以在函数内部使用 `using namespace name`。

```
#include <iostream>
using namespace std;

namespace NS {
    int i;
    namespace NS2 { // 一个嵌套的命名空间
    int j;
} // NS2 结束
} // NS1 结束

int main() {
    NS1::i = 19;
    // NS2::j = 10; // 错误，NS2 嵌套在 NS1 内部
    NS1::NS2::j = 10; // 这是正确的

    cout << NS1::i << endl;

    // 使用 NS1
    using namespace NS1;

    // 现在 NS1 可见，NS2 可以
    // 独立使用来引用 j
    cout << i * NS2::j;

    return 0;
}

// 输出
19
190
```

## std 命名空间

标准 C++ 库将其整个库定义在自己的名为 `std` 的命名空间中。

`using namespace std;`

这条 `using` 语句将 `std` 命名空间中的标识符引入当前命名空间，使我们直接访问库中定义的函数和类的名称，而无需为每个名称加上 `std` 限定。

## 命名空间别名

命名空间标识符可以被别名替换。例如：

```
namespace newfarm = farm;
```

现在可以使用 `newfarm` 别名来代替 `farm` 命名空间：

```
newfarm::pets = 5; // 等同于 farm::pets;
```

```
#include <iostream>
namespace T {
    int ctr = 0;
}
int main() {
    namespace Z = T;
    std::cout << Z::ctr << std::endl;
}
// 输出
0
```

## C++ 结构体与联合体

在 C++ 中，`struct` 仅仅是所有数据成员和成员函数默认都是公开的类。与 C 不同，C++ `struct` 可以包含成员函数。

这里是一个 C++ `struct` 声明的示例：

```cpp
// 一个 C++ struct
#include <iostream>
#include <cstring>

using namespace std;

struct Foo {
    // public
    void buildString(const char *s);
    void showWord();

private:
    unsigned short u;
    unsigned char c[2];
};

void Foo::buildString(const char *s) {
    // 初始化
    strcpy(c[0], s);
}

void Foo::showWord() {
    cout << u;
}

void Foo::setColor(unsigned short i) {
    u = i;
}

int main() {
    // 使用 struct
    Foo foo;
    foo.buildString("hello world");
    foo.showWord();
}

// 输出
hello world
```

## 联合体与类

在 C++ 中，`union`（联合体）可以同时包含成员函数和数据成员。它们还可以包含构造函数和析构函数。对于联合体，所有元素共享相同的内存位置。联合体成员默认是公开的。像 `struct` 一样，联合体成员默认是公开的。

这是一个示例：
