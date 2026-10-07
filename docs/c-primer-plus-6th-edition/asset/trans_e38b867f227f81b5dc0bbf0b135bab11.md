

# 第18章 访问新的 C++ 标准

```
int fn(int j) { ... }
double fn(double w) { ... }
void fn(const char * s) { ... }

class C2 : public C1
{
public:

    using C1::fn;
    double fn(double) { ... };
};

C2 c2;
int k = c2.fn(3); // uses C1::fn(int)
double z = c2.fn(2.4); // uses C2::fn(double)
```

C2 中的 using 声明使 C1 中的三个 fn() 方法对 C2 对象可用。C2 中定义的 fn(double) 方法优先于来自 C1 的方法。
C++11 将同样的技术带到了构造函数。基类的所有构造函数，除默认、拷贝和移动构造函数外，都作为派生类的可能构造函数引入，但与类构造函数签名匹配的那些被使用：

```
class BS
{
int q;
double w;
public:
BS() : q(0), w(0) {}
BS(int k) : q(k), w(100) {}
BS(double x) : q(-1), w(x) {}
BS(int k, double x) : q(k), w(x) {}
void Show() const {std::cout << q << ", " << w << '\n';}
};
```

```
class DR : public BS
{
short j;
public:
    using BS::BS;
DR() : j(-100) {} // DR 需要自己的默认构造函数
DR(double x) : BS(2*x), j(int(x)) {}
DR(int i) : j(-2), BS(i, 0.5* i) {}
void Show() const {std::cout << j << ", "; BS::Show();}
};
```

```
int main()
```

## 新的类特性

```
DR o01; // use DR()
DR o2(18.81); // use DR(double) instead of BS(double)
DR o3(10, 1.8); // use BS(int, double)
...
```

由于没有 DR(int, double) 构造函数，继承的 BS(int, double) 用于 o3。请注意，继承的基类构造函数只初始化基类成员。如果您还需要初始化派生类成员，可以使用成员初始化语法而不是继承：

## 管理虚方法：override 和 final

虚方法是在实现多态层次结构时的重要组成部分，在这种层次结构中，基类引用或指针可以调用适用于所引用对象类型的虚方法。虚方法会带来一些编程陷阱。例如，假设基类有一个特定的虚方法，您决定为派生类提供一个不同版本。这就是覆盖旧版本。但正如第13章“类继承”中所讨论的，如果函数签名不匹配，您会隐藏而不是覆盖旧版本：

```
class Action
{
int a;
public:
Action(int i = 0) : a(i) {}
int val() const { return a; }
virtual void f(char ch) const { std::cout << val(ch) << "\n"; }
};
class Bingo : public Action
{
public:
Bingo(int i = 0) : Action(i) {}
virtual void f(char * ch) const { std::cout << val(ch) << "\n"; }
};
```

由于类 Bingo 有 f(char* ch) 而不是 f(char ch)，f(char ch) 对 Bingo 对象是隐藏的。这会阻止程序使用如下代码：

```
Bingo b(10);
b.f('f'); // works for Action object, fails for Bingo object
```

使用 C++11，您可以使用 virtual 关键字 override 来表示您打算覆盖一个虚函数。将其放在参数列表之前。如果您的声明与基方法不匹配，编译器会报错。因此，以下 Bingo::f() 版本将生成编译时错误消息：

```
virtual void f(char * ch) const override { std::cout << val()
                << ch << "\n"; }
```

例如，Microsoft Visual C++ 2010 这样说：
method with override specifier 'override' did not override any
base class methods

specifier final 解决了一个不同的问题。您可能希望禁止派生类覆盖某个特定的虚方法。为此，将 final 放在参数列表之后。例如，以下代码将创建基于 Action 的类来定义 f() 函数：

```
virtual void f(char ch) const final { std::cout << ch << "\n"; }
```

specifiers override 和 final 并没有完全成为关键字的地位。相反，它们被标记为“具有特殊含义的标识符”。这意味着编译器使用它们出现的上下文来决定它们是否有特殊含义。在其他上下文中，它们可以作为普通标识符或类使用（例如，作为变量名或枚举）。

## Lambda 函数

当您看到 lambda 函数（又名 lambda 表达式，或简称为 lambdas）一词时，您可能会怀疑这不是 C++11 为初学者程序员添加的功能之一。当您看到 lambda 函数实际看起来如何时，您的怀疑会得到证实——这里有一个例子：

```
[](int x) { count += (x % 13 == 0); }
```

但它们看起来虽然晦涩，但并不神秘，并且提供了有用的服务，特别是使用函数谓词的 STL 算法。

## 函数指针、仿函数和 Lambda 的用法

让我们看一个使用三种方法向 STL 算法传递信息的示例：函数指针、仿函数和 lambda。（为方便起见，我们将这三种形式称为函数对象，这样我们就不必一直重复“函数指针或或 lambda”。）假设您想生成一个随机整数列表，并确定其中有多少个能被 3 整除，有多少个能被 13 整除。如果需要，这是一项您绝对觉得非常迷人的任务。

生成列表相当直接。一个选项是使用 vector<int> 数组来保存数字，并使用 STL generate() 算法用随机数填充数组：

```
#include <vector>
#include <algorithm>
#include <cmath>

std::vector<int> numbers(1000);
std::generate(vector.begin(), vector.end(), std::rand);
```

generate() 函数接收一个范围，由前两个参数指定，并将每个元素设置为第三个参数返回的值，该参数是一个不带参数的函数对象。在这种情况下，函数对象是指向标准 rand() 函数的指针。

在 count_if() 算法的帮助下，很容易计算能被 3 整除的元素数量。前两个参数应指定范围，就像 generate() 一样。第三个参数应是一个返回 true 或 false 的函数对象。然后 count_if() 函数会计算函数返回 true 的所有元素。要查找能被 3 整除的元素，可以使用此函数定义：

```
bool f3(int x) { return x % 3 == 0; };
```

类似地，您可以使用以下函数定义来查找能被 13 整除的元素：

```
bool f13(int x) { return x % 13 == 0; };
```

有了这些定义，您可以按如下方式计数元素：
int count3 = std::count_if(numbers.begin(), numbers.end(), f3);
cout << "Count of numbers divisible by 3: " << count3 << "\n";
count13 = std::count_if(numbers.begin(), numbers.end(), f13);
cout << "Count of numbers divisible by 13: " << count13 << "\n";

接下来，让我们回顾一下如何使用仿函数完成此任务。正如您从第 16 章回忆的那样，如果类定义了 operator() 作为类方法，则该类是一个可以像函数名一样使用的对象。仿函数的一个优点是您可以使用同一个仿函数完成两个任务。以下是一个可能的定义：

```
class f_mod {
private:
  int dv;
public:
  f_mod(int d = 1) : dv(d) {}
  bool operator()(int x) { return x % dv == 0; };
};
```

回想一下其工作原理。您可以使用构造函数创建一个存储特定整数值的 f_mod 对象：

```
f_mod obj(3); // f_mod.dv set to 3
```

此对象可以使用 operator() 方法返回一个 bool 值：

```
bool is_div_by_3 = obj(7); // same as obj.operator(7)
```

构造函数本身可以用作 count_if 等函数的参数：
count3 = std::count_if(numbers.begin(), numbers.end(), f_mod(3));

参数 f_mod(3) 创建值 3，count_if() 使用创建的对象调用 operator() 方法，将参数 x 设置为 numbers 的一个元素。要计算有多少个数字能被 13 整除而不是使用 f_mod(13) 作为第三个参数。

最后，让我们检查 lambda 方法。名称来自 lambda 演算，一种用于定义和应用函数的数学系统。该系统允许使用匿名函数——也就是说，它允许您放弃函数名称。在 C++11 上下文中，您可以将匿名函数定义（lambda）作为使用函数指针的函数的参数。对应于 f3() 函数的 lambda 是：

```
[] (int x) { return x % 3 == 0 };
```

它看起来像 f3 的定义：

```
bool f3(int x) { return x % 3 == 0 };
```

两个区别是函数名被 [] 替换（多么匿名！）并且没有声明的返回类型。相反，返回类型从返回值的 decltype 推导出来，在本例中为 bool。如果 lambda 没有 return 语句，类型推导为 void。在我们的示例中，您将按如下方式使用此 lambda：

```
count3 = std::count_if(numbers.begin(), numbers.end(),
[](int x) { return x % 3 == 0 });
```

也就是说，您将整个 lambda 表达式用作指针或仿函数构造函数一样使用。

lambda 的自动推导仅在主体由单个 return 语句组成时才有效。否则，您需要使用尾随返回类型语法：
[] (double x, int y) -> double { return x - y }; // return type is double

清单 18.4 说明了刚刚讨论的要点。

## 清单 18.4 lambda0.cpp

```
// lambda0.cpp using lambda expressions
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
#include <ctime>
const long Size1 = 39L;
const long Size2 = 100*Size1;
const long Size3 = 100*Size2;
```

