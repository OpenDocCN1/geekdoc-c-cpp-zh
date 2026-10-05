

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

