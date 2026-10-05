

# C++ 友元函数与友类

通过使用 `friend` 关键字，我们可以允许非成员函数访问类的私有成员。友元函数可以访问其所属类的所有私有成员和受保护成员。要声明一个友元函数，将其声明包含在类内部，并在该声明前加上 `friend` 关键字。

```cpp
#include <iostream>
using namespace std;

class Foo {
    int a, b;
public:
    friend int sum(Foo);
    void setAb(int i, int j);
};

void Foo::setAb(int i, int j) {
    a = i;
    b = j;
}

// 注意：sum() 并不是任何类的成员函数。
int sum(Foo f) {
    /* 因为 sum() 是 Foo 的友元，它可以
       直接访问私有成员 a 和 b。 */
    return f.a + f.b;
}

int main() {
    Foo klass;
    klass.setAb(3, 4);
    cout << sum(klass) << endl;
}

// output
7
```

在这个示例中，`sum()` 函数不是 Foo 的成员。然而，由于它是 Foo 的友元，它仍然具有访问 Foo 私有成员的权限。

# 前置声明或前向引用

当对象在声明之前被使用时，需要进行前置声明。以下示例了如何对类进行前置声明：

```cpp
// 类 C2的前置声明
class C2
{
  int status;
public:
  void setStatus(int);
  int getStatus(C2);
}
```

# 友类

也可以使一个类成为另一个类的友类。在这种情况下，友类的所有成员函数都可以访问宿主类的私有和受保护成员。例如：

```cpp
#include <iostream>
using namespace std;

// 类 Min的前置声明
class Min;

class TwoValues
{
  int a;
  int b;
public:
  TwoValues(int i, int j) { a = i; b = j; }
  friend class Min;
};

class Min
{
public:
  int minimum(TwoValues x);
};

int Min::minimum(TwoValues x)
{
    return x.a < x.b ? x.a : x.b;
}

int main()
{
    TwoValues obj(10, 20);
    Min m;
    cout << m.minimum(obj);
    return 0;
}
// output
10
```

# C++ 内联函数

在 C++ 中，我们可以创建实际上并没有被调用的短函数；相反，它们的代码会在声明处进行内联展开。这会导致代码运行更快，因为不需要使用栈来加载参数。我们可以通过在函数声明前加上 `inline` 关键字，使函数被内联展开而不是调用。

```cpp
#include <iostream>
inline int max(int a, int b)
{
    return a > b ? a : b;
}
int main()
{
    std::cout << max(10, 20) << std::endl;
    std::cout << max(99, 88) << std::endl;
    return 0;
}
```

内联函数之所以是 C++ 的重要补充，是因为它们允许我们创建非常高效的代码。由于类通常需要几个频繁执行的接口函数（提供对私有数据的访问），这些函数的效率是至关重要的。每当调用函数时，调用和返回机制都会产生大量的开销。通常情况下，在调用函数时会将参数推入栈中并保存各种寄存器，然后在函数返回时恢复这些寄存器。问题在于这些指令是非常耗时的。然而，如果函数是内联的，这些操作就不会发生。

虽然内联函数可以提高运行速度，但由于代码重复，它会导致代码体积增大。因此，最好的做法仅对那些对程序性能有显著影响的小函数使用 `inline`。`inline` 实际上只是一个请求，而不是命令，编译器可以选择忽略它。

# 在类内定义内联函数

类成员函数可以在类内隐式声明，也可以显式声明，如下：

```cpp
#include <iostream>
class Foo
{
    int a, b;
public:
    void init(int i, int j);
    // 隐式内联
    void show() { std::cout << a << " " << b << "\n"; };
}

// 显式创建内联成员函数
inline void Foo::init(int i, int j)
{
    a = i;
    b = j;
}

int main()
{
    Foo foo;
    foo.init(1, 3);
    foo.show();
}

// output
1 3
```

如示例所示，我们可以在类内部完全定义内联函数，也可以在类外部显式定义。当函数定义在类内部时，它会自动变成内联函数（如果可能）。在这种情况下不需要在函数声明前加上 inline 关键字。

# 构造函数与析构函数

析构函数的名称与类名相同，但带有 `~` 前缀。

当对象产生时会调用对象的构造函数，当对象被销毁时会自动调用对象的析构函数。

全局对象的构造函数在 main 开始执行之前执行。在同一个文件中，全局构造函数按照声明顺序执行。当全局构造函数分布在多个文件中时，它们的执行顺序是未知的。全局析构函数在 main 结束后按反顺序执行。

局部对象的构造函数在遇到对象定义时执行。局部对象的析构函数按照构造函数的相反顺序执行。

# 私有析构函数

```cpp
#include <iostream>
class Foo {
private:
    ~Foo();
};
int main() {
    Foo foo;
}

// output
error: 'Foo::~Foo()' 在此上下文中是私有的
```

此程序无法编译。原因是 foo 在栈上创建的，一旦 foo 离开作用域，由于析构函数是私有的，将无法调用。将类的析构函数设为私有可以确保只有类对象自己可以销毁。例如，引用对象可以在计数变为零时销毁自己。

