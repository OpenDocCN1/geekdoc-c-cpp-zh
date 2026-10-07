

# 第 15 章 朋友、异常与更多

```cpp
void mesg();
inline void bad_hmean::mesg()
{
    std::cout << "hmean(" << v1 << ", " << v2 << "): "
    << "invalid arguments: a = -b\n";
}
```

![](img/cd111a87c1db9aff4db4b18834327463_918_0.png)

```cpp
while (cin >> x >> y)
{
    try {
        z = hmean(x,y);
    } // try 块结束
    catch (const char * s) // 异常处理程序开始 {
        cout << s << "\n";
        cout << "Enter new pair of numbers: ";
        continue;
    } // 处理程序结束
    cout << "Harmonic mean of " << x << " and " << y
    << " is " << z << "\n";
    cout << "Enter next set of numbers <q to quit: ";
}
```

```cpp
double hmean(double a, double b)
{
    if (a == -b)
        throw "bad hmean() arguments: a = -b not allowed";
    return 2.0 * a * b / (a + b);
}
```

- 1. 程序在 try 块中调用 hmean()。
- 2. hmean() 抛出一个异常，将执行权转移到 catch 块，并将异常字符串赋值给 s。
- 3. catch 块将执行权传回 while 循环。

# 图 15.2 带有异常的程序流。

bad_hmean 对象可以初始化为传递给 hmean() 的值，并可以使用 mesg() 方法来报告问题（包括这些值）。hmean() 函数可以使用如下所示的代码：

```cpp
if (a == -b)
    throw bad_hmean(a,b);
```

# 异常 905

这调用了 bad_hmean() 构造函数，初始化对象以持有参数值。

列表 15.10 和 15.11 增加了第二个异常类 bad_gmean 以及第二个函数 gmean()，该函数会抛出 bad_gmean 异常。gmean() 函数计算两个数的几何平均数，即它们乘积的平方根。该函数在两个参数均为非数时定义，因此如果检测到负数参数，它将抛出异常。列表 15.10 是包含异常类定义的头文件，而列表 15.11 是使用该头文件的示例程序。注意，try 块之后有两个连续的 catch 块：

```cpp
try {
  // try 块开始
  // try 块结束
}
catch (bad_hmean & bg) {
  // catch 块开始
}
catch (bad_gmean & hg) {
  // catch 块结束
}
```

假设 hmean() 抛出一个 bad_hmean 异常，那么第一个 catch 块会捕获它。如果 gmean() 抛出一个 bad_gmean 异常，该异常将跳过第一个 catch 块并被第二个捕获。

# 列表 15.10 exc_mean.h

```cpp
// exc_mean.h -- 用于 hmean(), gmean() 的异常类
#include <iostream>

class bad_hmean {
private:
  double v1;
  double v2;
public:
  bad_hmean(double a = 0, double b = 0) : v1(a), v2(b) {}
  void msg();
};

inline void bad_hmean::msg() {
  std::cout << "hmean(" << v1 << ", " << v2 << "): "
    << "invalid arguments: a = -b\n";
}
```

# 第 15 章 朋友、异常与更多

```cpp
class bad_gmean
{
public:
    double v1;
    double v2;
    bad_gmean(double a = 0, double b = 0) : v1(a), v2(b){}
    const char * mesg();
};
```

```cpp
inline const char * bad_gmean::mesg()
{
    return "gmean() arguments are >=\n";
}
```

# 列表 15.11 error4.cpp

```cpp
// error4.cpp - 使用异常类
#include <iostream>
#include <cmath> // math.h, unix 用户可能需要 -lm 标志
#include "exc_gmean.h"
// 函数原型
double hmean(double a, double b);
double gmean(double a, double b);
int main()
{
    using std::cout;
    using std::cin;
    using std::endl;

    double x, y, z;

    cout << "Enter two numbers: ";
    while (cin >> x >> y)
    {
        try {
            z = hmean(x,y);
            cout << "Harmonic mean of " << x << " and " << y << "\n";
            cout << " is " << z << endl;
            cout << "Geometric mean of " << x << " and " << y << "\n";
            cout << " is " << gmean(x,y) << endl;
            cout << "Enter next set of numbers <q to quit: ";
        }
        catch (bad_hmean & bg)
        {
            bg.msg();
            cout << "Values used: " << bg.v1 << endl;
            cout << "Sorry, you don't get to play more.\n";
            continue;
        }
        catch (bad_gmean & hg)
        {
            hg.msg();
            cout << "Values used: " << hg.v2 << endl;
            cout << "Try again.\n";
            break;
        } // catch 块结束
    }
    cout << "Bye!\n";
    return 0;
}
```

```cpp
double hmean(double a, double b)
{
  if (a == -b)
    throw bad_hmean(a,b);
  return 2.0 * a * b / (a + b);
}
```

```cpp
double gmean(double a, double b)
{
  if (a < 0 || b < 0)
    throw bad_gmean(a,b);
  return std::sqrt(a * b);
}
```

这是一个程序的示例运行，它因输入问题终止：
```
enter two numbers: 4 12
Harmonic mean of 4 and 12 is 6
Geometric mean of 4 and 12 is 6
Enter next set of numbers <q to quit>: 5 -5
hmean(5,-5): invalid arguments: a = -b
Try again.
enter two numbers: 5 -2
Harmonic mean of 5 and -2 is -6
gmean() arguments should be >= 0
Values used: 5,2
Sorry, you don't get to play more.
Bye!
```

注意点之一是 bad_hmean 处理程序使用了 `continue` 语句，而 bad_gmean 处理程序使用了 `break` 语句。因此，hmean() 的输入导致程序跳过循环的剩余部分并开始循环。这说明程序可以确定抛出了什么异常（通过异常类型）并对其响应。另一个注意点是 bad_gmean 的设计技术与 hmean 使用的不同，特别是 bad_gmean 使用公共数据并返回字符串。

# 异常遇上 C++11

有时一个想法在原理上看起来很有前景，但在实践中并不顺利。这就是异常规范的故事，这是一个 C++98 添加的特性，然后被 C++11 弃用。这意味着该特性仍在标准中，但在未来可能不再，因此建议不要使用。然而，在忽略异常规范之前，至少应该知道它们是什么样的：它们如下：

```cpp
double harm(double a) throw(bad_thing); // 抛出 bad_thing
double harm();                         // 不抛出异常
```

`throw()` 无论是否带有类型列表，异常规范都会出现在函数原型和定义中。异常规范的一个原因是为了提醒用户 try 块的可能需要，但这可以通过注释轻松实现。第二个原因是允许编译器在运行时添加代码检查是否违反了异常规范。这很容易发生。例如，harm() 可能会抛出一个异常，但它可能调用了一个抛出异常的函数。在你编写代码时，该函数没有抛出异常，但在库更新后它有了。总之，编程社区（特别是那些努力编写异常安全代码的人）的共识是忽略这一特性。而且在 C++11 的帮助下，你也可以忽略异常规范。

然而，C++11 允许一种特殊的规范——新关键字 `noexcept` 用于指示函数不抛出异常：

```cpp
double harm() noexcept; // 不抛出异常
```

关于这种规范的必要性和用处存在一些争论，因此最好避免使用（至少在大多数情况下）。但强烈需要引入一个新关键字。认为知道函数不应该抛出异常可以帮助优化代码。这种用法被视为程序员的一种承诺。还有一个 `noexcept()` 运算符（见附录 E），报告其操作数是否可能抛出异常。

# 回溯

假设 try 块没有包含对抛出异常函数的直接调用，但它调用了一个调用抛出异常函数的函数。执行跳转到抛出异常的函数和处理器。这样做涉及到回溯，我们现在来讨论。

首先，看看 C++ 通常如何处理函数调用和返回。C++ 通常通过将信息放在栈上来处理函数调用（见第 9 章“内存模型与命名空间”）。特别是，程序将调用函数的地址（返回地址）放在栈上。当被调用函数完成时，程序使用该地址确定继续执行程序的位置。此外，函数调用会将任何参数放在栈上，它们被处理为自动变量。如果被调用函数创建了任何自动变量，它们也会被添加到栈上。如果被调用函数调用了另一个函数，它的信息会被添加到栈上，依此类推。当函数终止时，程序执行传递到函数时存储的地址，栈顶被释放。该函数通常返回到调用它的函数，每个函数在终止时释放其自动变量。如果自动变量是一个类对象，则调用析构函数（如果有）。

假设函数通过抛出异常而不是返回调用终止。同样，程序从栈中释放内存。但程序没有停在栈上的第一个返回地址，而是继续释放栈直到到达位于 try 块中的返回地址（见图 15.3）。控制传递给块末尾的异常处理器，而不是函数调用后的第一个语句。这个过程被称为回溯。异常机制的一个重要特点是，就像函数返回一样，该函数栈上的任何自动类对象都会调用析构函数，而 `throw` 语句处理由 try 块和 `throw` 之间的整个函数调用序列放在栈上的对象。如果没有回溯功能，throw 将导致中间函数调用放在栈上的自动类对象的析构函数无法执行。

列表 15.12 提供了一个回溯的示例。在其中，main() 调用 `mean()`，`mean()` 继调用 `hmean()` 和 `gmean()`。`mean()` 函数由于没有别的事要做，计算了算术平均数、调和平均数和几何平均数的平均数。`main()` 和 `mean()` 都创建了 demo 类型的对象（一种在构造函数和析构函数被使用时宣布的喧闹类），这样就可以看到当抛出异常时这些对象发生了什么。`main()` 中的 try 块捕获了 bad_hmean 和 bad_gmean 异常，`mean()` 中的 try 块只捕获 bad_hmean 异常。这个 catch 块具有以下代码：

```cpp
catch (bad_hmean & bg) // catch 块开始
  bg.msg();
  std::cout << "Caught in mean()\n";
  throw;              // 重抛出异常
}
```

