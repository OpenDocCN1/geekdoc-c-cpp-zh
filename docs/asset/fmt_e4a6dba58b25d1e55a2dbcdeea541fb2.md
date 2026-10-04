
异常是处理函数本身无法轻松处理的情况的正确方法，但这种情况又不至于让程序完全终止。所有异常都在短程返回和粗暴退出之间提供了一个灵活的控制水平。

本章将涵盖异常。首先给出一个异常与`setjmp` `longjmp`组合产生不同影响的示例。示例之后是对异常正式方面的讨论。我们将在本章末尾遇到这些析构函数的后果。

## 10.1 异常语法

在将传统的`goto`处理方式与异常进行对比之前，让我们介绍使用异常时涉及的元素。

- 异常由`throw`语句产生。`throw`关键字后面跟着特定类型的表达式，会将该表达式作为异常抛出。在 C++ 中，可以抛出任何内容作为异常：`int`、`bool`、`string`，然而可以使用标准异常类型（参见第 13 章）定义新异常。

- 异常在定义的局部环境中产生，`try`块系统确保程序的所有代码都被`try`块包裹。

这是一个在`try`块中抛出异常的示例：

```cpp
try {
  // 这里可以定义任何代码
  if (someConditionIsTrue)
    throw "this is the std::string exception";
  // 这里可以定义任何代码
}
```

`catch`：紧随`try`块定义一个或多个`catch`子句。一个`catch`子句由定义其可以捕获的异常类型的`catch`头和定义如何处理异常的复合语句组成：

```cpp
catch (const string &msg) {
  // 处理捕获的字符串对象的语句
}
```

多个`catch`子句可以出现，对应每个需要捕获的异常类型。通常，`catch`子句可以任何顺序出现，但某些异常需要特定的顺序。为了避免混淆，最好将最通用异常的`catch`子句放在最后。最多只会激活一个异常。C++ 不支持在完成`catch`子句后激活的 Java 式`finally`子句。

## 10.2 使用异常的示例

在以下示例中，使用了相同的基础程序。程序使用了两个类，`Outer`和`Inner`。

首先，在`main`中定义一个`Outer`对象，并调用其成员`Outer::fun`。然后，在`Outer::fun`中定义一个`Inner`对象。在定义`Inner`对象后，调用其成员`Inner::fun`。

就是这样。`Outer::fun`终止`inner`的析构函数。然后程序终止，激活`outer`的析构函数。这里是基础程序：

```cpp
#include <iostream>
using namespace std;

class Inner {
public:
    Inner();
    ~Inner();
    void fun();
};
Inner::Inner() {
    cout << "Inner constructor\n";
}
Inner::~Inner() {
    cout << "Inner destructor\n";
}
void Inner::fun() {
    cout << "Inner fun\n";
}

class Outer {
public:
    Outer();
    ~Outer();
    void fun();
};
Outer::Outer() {
    cout << "Outer constructor\n";
}
Outer::~Outer() {
    cout << "Outer destructor\n";
}
void Outer::fun() {
    Inner in;
    cout << "Outer fun\n";
    in.fun();
}

int main() {
    Outer out;
    out.fun();
}
/*
Generated output:
Outer constructor
Inner constructor
Outer fun
Inner fun
Inner destructor
Outer destructor
*/
```

编译并运行后，程序的输出完全符合预期：析构函数按照正确的顺序被调用（与构造函数的调用顺序相反）。

现在，让我们关注两种变体，我们在`Inner::fun`函数中模拟了一个非致命的灾难性事件。该事件应该在`main`结束附近处理。

我们考虑两种变体。第一种变体由`setjmp`和`longjmp`处理；第二种变体由 C++ 异常机制处理事件。

## 10.2.1 过时的机制：`setjmp`和`longjmp`

对上一节的基础程序进行细微修改，包含一个供`setjmp`和`longjmp`使用变量`jmp_buf jmpBuf`。

`Inner::fun`函数调用`longjmp`来模拟一个灾难性事件，并在`main`结束附近处理。跳转的目标通过函数`setjmp`定义。`setjmp`返回 0 表示`jmp_buf`变量已初始化，此时会调用`Outer::fun`。这代表了“正常”流。

如果`Outer::fun`正常终止，程序的返回值为 0。然而，程序的设计使得这种情况不会发生：`Inner::fun`调用了`longjmp`。结果执行流返回到`setjmp`函数。在这种情况下，它不返回 0。因此，在从`Outer::fun`调用`Inner::fun`后，进入了`main`的`if`语句，程序以返回值 1 终止。在学习以下程序源码时请遵循这些步骤，该源码是对 10.2 节中基础程序的直接修改：

```cpp
#include <iostream>
#include <setjmp.h>
#include <stdlib>

using namespace std;

jmp_buf jmpBuf;

class Inner {
public:
    Inner();
    ~Inner();
    void fun();
};

Inner::Inner() {
    cout << "Inner constructor\n";
}
void Inner::fun() {
    cout << "Inner fun\n";
    longjmp(jmpBuf, 0);
}
Inner::~Inner()
{
    cout << "Inner destructor\n";
}

class Outer
{
public:
Outer();
~Outer();
void fun();
};

Outer::Outer()
{
    cout << "Outer constructor\n";
}
Outer::~Outer()
{
    cout << "Outer destructor\n";
}

void Outer::fun()
{
Inner in;
    cout << "Outer fun\n";
in.fun();
}

int main()
{
Outer out;

if (setjmp(jmpBuf) != 0)
    return 1;

out.fun();
}
/*
Generated output:
Outer constructor
Inner constructor
Outer fun
Inner fun
Outer destructor
*/
```

该程序的输出清楚地显示`inner`的析构函数没有被调用。这是`longjmp`执行非局部跳转的直接结果。处理立即从`Inner::fun`中的`longjmp`调用跳转到`main`中的`setjmp`。它的返回值不等于 0，程序以返回 1 终止。非局部的`Inner::~Inner`永远不会执行：返回`main`的`setjmp`时，现有的栈直接被分解，忽略了任何等待调用的析构函数。

这个例子说明使用`longjmp`和`setjmp`很容易跳过对象的析构函数，因此 C++ 程序应该避免使用这些函数。

## 10.2.2 异常：优选替代方案

异常是 C++ 对`setjmp`和`longjmp`引起问题的解答。这里再次是一个源自 10.2 基础程序的示例：

```cpp
#include <iostream>
using namespace std;

class Inner {
public:
    Inner();
    ~Inner();
    void fun();
};
Inner::Inner() {
    cout << "Inner constructor\n";
}
Inner::~Inner() {
    cout << "Inner destructor\n";
}
void Inner::fun() {
    cout << "Inner fun\n";
    throw 1;
}
class Outer {
public:
    Outer();
    ~Outer();
    void fun();
};
Outer::Outer() {
    cout << "Outer constructor\n";
}
Outer::~Outer() {
    cout << "Outer destructor\n";
}
void Outer::fun() {
    Inner in;
    cout << "Outer fun\n";
    in.fun();
}

int main() {
    Outer out;
    try {
        out.fun();
    } catch (int x) {
    }
}
```

## 10.3 抛出异常

异常由`throw`语句产生。`throw`关键字后面跟着一个表达式，该表达式定义异常值。

```cpp
#include <iostream>
#include <string>
using namespace std;

class Object {
    string d_name;

public:
    Object(string name)
        : d_name(name)
    {
        cout << "Constructor of " << d_name << "\n";
    }
    Object(const Object& other) : d_name(other.d_name + " (copy)") {
        cout << "Copy constructor for " << d_name << "\n";
    }
    ~Object() {
        cout << "Destructor of " << d_name << "\n";
    }
    void toThrow() {
        Object out("local object");
        cout << "Calling fun of " << d_name << "\n";
        throw toThrow();
    }
    void hello() {
        cout << "Hello by " << d_name << "\n";
    }
};

int main() {
    Object out("main object");
    try {
        out.fun();
    } catch (Object o) {
        cout << "Caught exception\n";
        o.hello();
    }
}
```

- 不要抛出局部对象的指针；

- 可以抛出动态生成对象的指针。在这种情况下，必须确保异常处理程序能够正确删除已生成的对象，以防止内存泄漏。

当函数无法完成其分配的任务但程序仍能够继续时，就会抛出异常。想象一个提供交互式计算器的程序。该程序期望数值型异常，并对其进行求值。异常可能包含语法错误，或者在数学上无法进行求值。也许计算器允许我们定义变量，用户可能会引用不存在的变量：表达式求值失败的原因有很多，抛出异常的理由也很多。这些情况都不应该终止程序。相反，程序会通知用户问题的性质，并邀请他们输入另一个异常。例如：

```cpp
if (parse(expressionBuffer)) // 解析失败
    throw "Syntax error in expression"

if (lookup(variableName)) // 未找到变量
    throw "Variable not defined"

if (divisionByZero()) // 无法进行除法
    throw "Division by zero is not defined"
```

这些`throw`语句相关的地方：它们可能深度嵌套在程序内部，也可能在更高层。此外，可以使用函数来管理异常。异常对象可能支持流插入操作，例如可以使用：

```cpp
if (lookup(variableName))
    throw Exception() << "Undefined variable " << variableName << "";
```

## 10.4 空的`throw`语句

有时需要检查异常。异常捕获器可能决定忽略异常、处理异常、在检查后重新抛出异常或将其转换为另一种类型的异常。例如，在服务器-客户端应用程序中，客户端可以通过将请求输入队列来向服务器提交请求。通常，每个请求最终都会得到服务器的回答。服务器可能会回复请求已成功处理，或者发生了某种错误。另一方面，服务器可能已经崩溃，客户端应该能够发现这一点，而不是无限等待服务器回复。

在这种情况下，会调用一个中间异常处理程序。抛出的异常首先在中间层进行检查。如果可能，则在该层进行处理。如果不在中间层处理该异常，它将原封不动地传递给更高层，由更高层处理真正的异常。

通过在异常处理器的代码中放置空语句，异常将传递给下一个可能处理该特定类型异常的层。重新抛出的异常不会由相邻的异常处理程序处理；它总是会被传递到更高级别的异常处理器。

在我们的服务器-客户端场景中，

```cpp
initialExceptionHandler(string &exception)
```

可以被设计为处理字符串异常。接收到的消息会经过检查。如果是一个简单消息，对其进行处理，并将异常传递到外层。在`initialExceptionHandler`的实现中使用了空`throw`语句：

```cpp
void initialExceptionHandler(string &exception)
{
    if (!plainMessage(exception))
        throw;

    handleMessage(exception);
}
```

在下方（第 10.5节），`throw`语句用于传递`catch`块接收到的异常。因此，像`initialExceptionHandler`这样的函数可以用于各种异常，只要它们的类型与`initialExceptionHandler`的参数（即`string`）匹配即可。

下一个示例跳跃了，使用了第 14 章涵盖的一些主题。不过，可以跳过该示例而不影响连贯性。

可以从派生自特定异常类型的类构建基础异常处理类。假设我们有一个`Exception`类，它有一个成员函数`ExceptionType::severity`。该成员函数告诉我们（难怪！）异常的严重程度。它可能是`Info`、`Notice`、`Warning`、`Error`或`Fatal`。其中包含的信息取决于其严重程度，并由`handle`函数处理。此外，所有异常都使用类似`textMsg`的成员函数，用`string`返回有关异常的文本信息。

通过定义多态的`handle`，可以使其在从基类`Exception`指针或引用调用时，根据抛出的异常的性质表现出不同的行为。
