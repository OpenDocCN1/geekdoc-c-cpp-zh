
首先，看看 C++ 通常如何处理函数调用和返回。C++ 通常通过将信息放在栈上来处理函数调用（见第 9 章“内存模型与命名空间”）。特别是，程序将调用函数的地址（返回地址）放在栈上。当被调用函数完成时，程序使用该地址确定继续执行程序的位置。此外，函数调用会将任何参数放在栈上，它们被处理为自动变量。如果被调用函数创建了任何自动变量，它们也会被添加到栈上。如果被调用函数调用了另一个函数，它的信息会被添加到栈上，依此类推。当函数终止时，程序执行传递到函数时存储的地址，栈顶被释放。该函数通常返回到调用它的函数，每个函数在终止时释放其自动变量。如果自动变量是一个类对象，则调用析构函数（如果有）。

假设函数通过抛出异常而不是返回调用终止。同样，程序从栈中释放内存。但程序没有停在栈上的第一个返回地址，而是继续释放栈直到到达位于 `try` 块中的返回地址（见图 15.3）。控制传递给块末尾的异常处理器，而不是函数调用后的第一个语句。这个过程被称为回溯。异常机制的一个重要特点是，就像函数返回一样，该函数栈上的任何自动类对象都会调用析构函数，而 `throw` 语句处理由 `try` 块和 `throw` 之间的整个函数调用序列放在栈上的对象。如果没有回溯功能，`throw` 将导致中间函数调用放在栈上的自动类对象的析构函数无法执行。

列表 15.12 提供了一个回溯的示例。在其中，`main()` 调用 `mean()`，`mean()` 继调用 `hmean()` 和 `gmean()`。`mean()` 函数由于没有别的事要做，计算了算术平均数、调和平均数和几何平均数的平均数。`main()` 和 `mean()` 都创建了 `demo` 类型的对象（一种在构造函数和析构函数被使用时宣布的喧闹类），这样就可以看到当抛出异常时这些对象发生了什么。`main()` 中的 `try` 块捕获了 `bad_hmean` 和 `bad_gmean` 异常，`mean()` 中的 `try` 块只捕获 `bad_hmean` 异常。这个 `catch` 块具有以下代码：

```cpp
catch (bad_hmean & bg) // catch 块开始
  bg.msg();
  std::cout << "Caught in mean()\n";
  throw;              // 重抛出异常
}
```

# 第 15 章 朋友、异常及更多

```cpp
int main() {
  ...
  try {
    afunct();
    nextfunc();
  }
  catch(const char * s) {
    ...
  }
}
```

```cpp
void afunct() {
  ...
  bfunct();
  return;
  ...
}
```

```cpp
void bfunct() {
  ...
  cfunct();
  return;
  ...
}
```

```cpp
void cfunct() {
  ...
  if(oops) throw "Help!";
  return;
  ...
}
```

### 使用 return

```cpp
int main() {
  ...
  try {
    afunct();
    nextfunc();
  }
  catch(const char * s) {
    ...
  }
}
```

```cpp
void afunct() {
  ...
  bfunct();
  return;
  ...
}
```

```cpp
void bfunct() {
  ...
  cfunct();
  return;
  ...
}
```

```cpp
void cfunct() {
  ...
  if(oops) throw "Help!";
  return;
  ...
}
```

### 使用 throw

图 15.3 `throw` 与 `return`。

代码通过显示消息来响应重新抛出异常，这意味着在这种情况下，它将异常传递给 `main()`。（通常情况下，重新抛出的异常会由下一个 `try-catch` 组合来捕获特定类型的异常。如果没有找到处理程序，默认会中止。）列表 15.12 使用了相同的处理程序（`exc_mean.h`）15.10 作为 15.11 `error5.cpp`

```cpp
error5.cpp -- 回溯堆栈
#include <iostream>
#include <cmath> // math.h, 用户可能需要
#include <string>
#include "exc_mean.h"
```

```cpp
class demo {
private:
  std::string word;
public:
  demo (const std::string & str)
{
    word = str;
    std::cout << "demo" << word << " created\n";
}
  ~demo()
{
    std::cout << "demo" << word << " destroyed\n";
}
  void hmean() const
{
    std::cout << "demo" << word << " lives!\n";
}
};
```

```cpp
// 函数原型
double hmean(double a, double b);
double gmean(double a, double b);
double means(double a, double b);
```

```cpp
int main()
{
    using std::cout;
    using std::cin;
    using std::endl;

    double x, y, z;
    {
    demo d1("found in block in main()");
    cout << "Enter two numbers: ";
    while (cin >> x >> y) {
        try { // try 块开始
            z = means(x,y);
            cout << "The mean of " << x << " and " << z << std::endl;
            cout << "Enter next pair: ";
        } // try 块结束
        catch (bad_hmean & bg) { // catch 块开始
            bg.msg2();
            cout << "Try again.\n";
            continue;
        } catch (bad_gmean & h) {
            cout.msgg();
            cout << "Values used: " << v1 << ", " << v2 << endl;
            cout << "Sorry, you don't get any more.\n";
            break;
        } // catch 块结束
    }
    d1.show();
    }
    cout << "Bye!\n";
    cin.get();
    cin.get();
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
        throw bad_gmean(a, b);
    return std::sqrt(a * b);
}
```

```cpp
double means(double a, double b)
{
    double am, hm, gm;
    demo d2("found in means()");
    am = (a + b) / 2.0; // 算术平均
    try{
        hm = hmean(a,b);
        gm = gmean(a,b);
    } catch (bad_hmean & bg) { // catch 块开始
        bg.msg2();
        std::cout << "Caught in means()\n";
        throw; // 重新抛出异常
    }
    d2.show();
    return (am + hm + gm) / 3.0;
}
```

## 异常

以下是程序的示例运行：

```
demo found in block in main() created
Enter two numbers: 6 12
demo found in means() created
demo found in means() lives!
demo found in means() destroyed
The mean of 6 and 12 is 8
6 -6
demo found in means() created
mean(6, -6): invalid arguments: a = -b
Caught in means()
demo found in means() destroyed
mean(6, -6): invalid arguments: a = -b
Try again.
6 -8
demo found in means() created
demo found in means() destroyed
gmean() arguments should be 0
Values used: 6, 8
Sorry, you don’t get any more.
demo found in block in main() lives!
demo found in main() destroyed
Bye!
```

## 程序说明

让我们追踪示例运行的过程。首先，正如构造函数宣告的那样，在 `main()` 块中创建了一个对象。接下来，调用了 `means()`，创建了另一个 `demo` 对象。`means()` 函数将值 6 和 12 传递给 `hmean()` 和 `gmean()`，这些函数返回到 `means()`，后者计算结果并返回。在返回结果之前，`means()` 调用了 `d2.show()`。返回结果后，`means()` ，`d2` 的析构函数被调用：

```
demo found in means() lives!
demo found in means() destroyed
```

下一个输入循环将值 6 和 -6 发送给 `means()`，然后 `means()` 创建了一个新的 `demo` 对象并将值传递给 `hmean()`。`hmean()` 函数抛出一个 `bad_gmean` 异常，该异常被 `means()` 中的 `catch` 块捕获。

### 异常异常

尽管 `throw-catch` 机制与函数参数和返回机制相似，但它们有几处不同。其中一点你已经遇到的，是 `return` 语句在函数中将执行权传递给具有 `try-catch` 组合的，而 `throw` 语句在在这种情况下，将重新抛出的异常传递到 `main()`。

另一个区别是编译器在抛出异常时总是创建一个临时副本，即使异常规范和 `catch` 块指定的是引用。例如，考虑以下代码：

```cpp
class problem {};
...
void super() throw (problem)
{
    if (oh_no)
    {
        problem oops; //构造对象
        throw oops; // 抛出它
        ...
    }
}
try {
    super();
}
catch(problem & p)
{
// 
}
```

在这里，`p` 指向 `oops` 的副本而不是 `oops` 本身。这是一件好事，因为 `oops` 在 `super()` 终止就不复存在了。顺便说，将构造与 `throw` 结合更为简单：

```cpp
throw object(); // 构建并抛出默认对象
```

此时你可能会疑惑，为什么在抛出生成副本的情况下仍然使用引用？毕竟，通常使用返回值的理由是为了避免复制的效率。答案是引用还有另一个重要属性：基类引用也可以指向派生类对象。假设你有一组通过继承派生的异常类型。在这种情况下，异常规范只需要列出基类的引用，它就可以匹配任何派生对象。

假设你有一个异常类层次结构，并且你想单独处理不同的类型。基类引用可以捕获整个家族的对象，但派生类对象只能捕获该对象以及派生自该类的对象。被抛出的对象会被匹配它的第一个 `catch` 块捕获。这建议按照派生关系的反序来排列 `catch` 块：

```cpp
class bad_1 {...}; ownclass bad_2 : public bad_1 {...};
class bad_3 : public bad_2 {...};
```

```cpp
void duper() {
{
    if (oh_no)
        throw bad_1();
    if (rats)
        throw bad_2();
    if (drat)
        throw bad_3();
}
}
```

```cpp
try {
    duper();
}
catch(bad_3 &be) {
    // statements
}
catch(bad_2 &be) {
    // statements
}
catch(bad_1 &be) {
    // statements
}
```

如果 `bad_1 &` 处理器在前，它将捕获 `bad_1`、`bad_2` 和 `bad_3` 异常。如果反过来，`bad_3` 异常将由 `bad_3 &` 处理器捕获。

## 提示

如果你有一个异常类的继承层次结构，你应该安排 `catch` 块的顺序，使得最派生类的异常（即位于类层次序列中最底部的类）首先被捕获，而基类异常最后被捕获。

按照正确的顺序排列 `catch` 块允许你选择性地处理每种类型的异常。但有时你可能不知道预期会遇到什么种类型的异常。例如，假设你写了一个调用另一个函数的函数，而你不知道另一个函数是否会抛出异常。即使你不知道类型，你仍然可以捕获该异常。捕获任何异常的技巧是在异常类型处使用省略号 `...`：

```cpp
catch (...) { // statements } // 捕获任何类型的异常
```

如果你知道某些会被抛出的异常，可以将这种全捕获形式放在 `catch` 块序列的末尾，有点类似于 `switch` 语句的 `default` 情况：

```cpp
try {
  duper();
} catch(bad_3 &be) {
  // statements
} catch(bad_2 &be) {
  // statements
} catch(bad_1 &be) {
  // statements
} catch(bad_hmean & h) {
  // statements
} catch (...) // 捕获剩余的所有内容
  // statements }
```

你可以设置一个处理器来捕获对象而不是引用。基类对象会捕获派生类，但派生部分会被剥离。因此，将使用虚方法的基版本。

# exception 类

C++ 异常的主要意图是为设计容错性程序提供语言级支持。也就是说，异常使得将错误处理整合到程序中变得更容易，这样你不必在事后承担某种更僵化的错误处理形式。如果合适，异常的灵活性和相对便利性应该鼓励程序员将故障处理集成到程序设计过程中。简而言之，异常是像类那样的、可以改变你编程方法的关键特征。

较新的 C++ 编译器正在将异常整合到语言中。例如，异常头文件（以前是 `exception.h` 或 `.h`）定义了一个异常类，C++ 使用该类作为异常类的基类以支持该语言。你的代码也可以抛出异常对象，或使用异常作为基类。其中一个虚成员函数命名为 `what()`，它返回一个字符串，其性质取决于实现。然而，由于该方法是虚函数，你可以在派生自该类的类中重新定义它：

```cpp
#include <exception>
class bad_hmean : public std::exception {
public:
  const char * what() { return "bad arguments to hmean()"; }
};
class bad_gmean : public std::exception {
public:
  const char * what() { return "bad arguments to gmean()"; }
};
```

如果你不想以不同的方式分别处理这些派生异常，可以使用同一个基类处理器来捕获它们：

```cpp
try {
  ...
} catch(std::exception& e) {
  cout << e.what() << endl;
}
```

或者你也可以单独捕获不同的类型。

C++ 库基于 `exception` 定义了许多异常类型。

# stdexcept 异常类

`stdexcept` 头文件定义了几个异常类。首先，该文件定义了 `logic_error` 和 `runtime_error` 类，它们都公继承自 `exception`：

```cpp
class logic_error : public exception {
public:
  explicit logic_error(const string& what_arg);
};
```
