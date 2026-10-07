

```
class bad_1 {...};
class bad_2 : public bad_1 {...};
class bad_3 : public bad_2 {...};
```

```
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

```
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

如果 `bad_1 &` 处理程序是自由的，它会捕获 `bad_1`、`bad_2` 和 `bad_3` 异常。采用相反的顺序，`bad_3` 异常将被 `bad_3 &` 处理程序捕获。

# Tip

如果你有一个异常类的继承层次结构，你应该安排 catch 块的顺序，使得最派生类的异常（即在类层次序列中最底层的类）先被捕获，而基类异常最后被捕获。

按正确顺序排列 catch 块可以让你选择性地处理每种类型的异常。但有时你可能不知道会抛出什么类型的异常。例如，假设你编写了一个调用另一个函数的函数，而你不知道另一个函数是否抛出异常。你仍然可以在不知道类型的情况下捕获异常。捕获任何异常的技巧是使用省略号作为异常类型：

```
catch (...) { // statements } // catches any type exception
```

如果你知道某些被抛出的异常，可以将这种捕获所有形式放在 catch 块序列的末尾，有点像 switch 的 default 分支：

```
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
} catch (...) // catch whatever is left {
  // statements }
```

你可以设置一个处理程序来捕获对象而不是引用。基类对象会捕获派生类，但派生特性会被剥离。因此，将使用基类版本的虚方法。

# The exception Class

C++ 异常的主要目的是为设计容错程序提供语言级支持。也就是说，异常使将错误处理纳入程序变得更容易，这样你就不必事后采用某种更僵化的错误处理形式。异常的灵活性和相对便利性应鼓励程序员在程序设计过程中集成故障处理，如果合适的话。简而言之，异常是该关键特性，就像类一样，可以改变你的编程方法。

更新的 C++ 编译器正在将异常纳入语言中。例如，exception 头文件（以前是 exception.h 或 .h）定义了一个 exception 类，C++ 将其用作异常类的基类以支持语言。你的代码也可以抛出异常对象或使用 exception 作为基类。一个虚成员函数名为 what()，它返回一个字符串，其性质取决于实现。然而，由于该方法是虚的，你可以在派生类中重新定义它：

```
#include <exception>
class bad_hmean : public std::exception {
public:
  const char * what() { return "bad arguments to hmean()"; }
};
class bad_gmean : public std::exception {
```

public:
const char * what() { return "bad arguments to gmean()"; }
..

如果你不想对这些派生异常进行不同处理，可以用同一个基类处理程序捕获它们：

```
try {
...
} catch(std::exception& e) {
  cout << e.what() << endl;
}
```

或者你可以分别捕获不同的类型。
C++ 库定义了基于 exception 的许多异常类型。

# The stdexcept Exception Classes

stdexcept 头文件定义了几个异常类。首先，文件定义了 logic_error 和 runtime_error 类，两者都公有地派生自 exception：

```
class logic_error : public exception {
public:
explicit logic_error(const string& what_arg);
};
```

```
class domain_error : public logic_error {
public:
explicit domain_error(const string& what_arg);
..
};
```

请注意，构造函数接受一个 string 对象作为参数；该参数提供 what() 方法作为 C 风格字符串返回的字符数据。
这些新类依次作为两个派生类族的基类。logic_error 族描述了，正如你可能预期的那样，典型的逻辑错误。原则上，良好的编程可以避免此类错误，但在实践中，这类错误可能会出现。每个类的名称表示它 intended 报告的错误类型：

- domain_error
- invalid_argument
- length_error
- out_of_bounds

# Exceptions 919

每个类都有一个像 logic_error 的构造函数，允许你提供 what() 方法返回的字符串。

也许一点扩充会有帮助。数学函数具有定义域和值域。定义域由函数有定义的取值组成，值域由函数返回的取值组成。例如，正弦函数的定义域是从负无穷到正无穷，因为正弦对所有实数都有定义。正弦函数的值域是从 -1 到 +1，因为那些是角度正弦的极值。另一方面，反函数的定义域是 -1 到 +1，而其值域是 [-pi] 到 [+pi]。如果你编写了一个将参数传递给 std::sin(int) 的函数，你可以让你的函数在参数超出 -1 到 +1 时抛出 domain_error。

invalid_argument 异常提醒你有一个意外的值被传递给函数。例如，如果一个函数期望接收一个每个字符都是 '0' 或 '1' 的字符串，它可以在字符串中出现其他字符时抛出 invalid_argument 异常。

length_error 异常用于指示没有足够的空间用于所需操作。例如，string 类有一个 append() 方法，如果字符串结果会大于最大可能字符串，则抛出 length_error 异常。

out_of_bounds 异常通常用于指示索引错误。例如，你可以定义一个类似数组的类，其中 operator[] 在索引对该数组无效时抛出 out_of_bounds 异常。

接下来，runtime_error 描述了可能在运行时出现但难以预测和防止的错误。每个类的名称表示它 intended 报告的错误类型：

- range_error
- overflow_error
- underflow_error

每个类都有一个像 runtime_error 的构造函数，允许你提供 what() 方法返回的字符串。

在浮点计算中可能发生下溢错误。一般来说，浮点类型可以表示的最小幅度有一个下限。会产生更小值的计算会导致下溢错误。溢出错误可能发生在整数或浮点类型中，当计算结果的幅度会超出函数的有效范围而没有下溢或溢出时，你可以使用 range_error 异常用于此类情况。

一般来说，logic_error 族的异常标识了一个容易受到编程事实影响的问题，而 runtime_error 异常只是一些不可避免的麻烦。所有这些错误类具有相同的一般特征。区别在于不同的类名允许你单独处理每种类型的异常。

另一方面，继承关系允许你如果愿意将它们归为一组。例如，以下代码单独捕获 out_of_bounds 异常，将其余 logic_error 族的异常作为一组捕获，并将 exception 对象、runtime_error 族的对象和派生自 exception 的任何剩余异常类型集体处理：

```
try {
  ...
  catch(out_of_bounds & oe) // catch out_of_bounds error
  {...}
  catch(logic_error & oe) // catch remaining logic_error family
  {...}
  catch(exception & oe) // catch runtime_error, exception objects
  {...}
```

如果这些库类不能满足你的需求，从 logic_error 或 runtime_error 派生一个异常类是有意义的，这样你就可以将你的异常融入到通用层次结构中。

# The bad_alloc Exception and new

当前 C++ 处理 new 的分配问题的方式是让其抛出 bad_alloc 异常。new 头文件包含 bad_alloc 类的声明，该类公有地派生自 exception 类。在过去的日子里，new 在无法分配请求内存时会返回空指针。

Listing 15.13 演示了当前方法。如果捕获到异常，程序会显示由继承的 what() 方法返回的实现相关消息并提前终止。

Listing 15.13 newex.cpp

```
// newex.cpp -- the bad_alloc exception
#include <iostream>
#include <new>
#include <cstdlib> // for exit(), EXIT_FAILURE
using namespace std;

struct Big {
  double stuff[20000];
};

int main() {
  Big * pb;
  try {
```

