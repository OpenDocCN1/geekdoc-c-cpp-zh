
最后，假设至少存在一个拷贝或移动构造函数，编译器可能会使用*复制省略*来避免调用它们。编译器可以在任何可能的地方自由使用复制省略；然而，这从来不是一项要求。因此，编译器始终可以决定不使用复制省略。在所有原本会使用拷贝或移动构造函数的情况下，编译器都可以考虑使用复制省略。

## 第10章：异常

C++ 支持程序对破坏程序正常顺畅流程的情况作出反应的几种方式：

-   函数可能注意到异常情况并发出消息。这可能是程序所能表现出的最不灾难性的反应。
-   观察到异常情况的函数可能决定停止其预期任务，向调用者返回错误码。这是推迟决策的一个绝佳例子：现在调用函数面临一个问题。当然，调用函数也可以采取类似行动，将错误码向上传递给它的调用者。
-   函数可能决定事情正在失控，并可能调用 `exit` 完全终止程序。这是一种强硬的问题处理方式，哪怕只是因为局部对象的析构函数不会被激活。
-   函数可能使用 `setjmp` 和 `longjmp` 函数的组合来强制执行非局部退出。该机制实现了一种 `goto` 跳转，允许程序在外层继续，跳过如果使用一系列从嵌套函数返回时本来必须经过的中间层级。

在 C++ 中，所有这些破坏流程的方法仍然可用。然而，在所提到的替代方案中，`setjmp` 和 `longjmp` 在 C++（甚至 C）程序中并不常见，因为程序流程被完全打乱。

C++ 提供异常作为首选替代方案，例如替代 `setjmp` 和 `longjmp`。异常允许 C++ 程序执行受控的非局部返回，而没有 `longjmp` 和 `setjmp` 的缺点。

异常是摆脱以下情况的正确方式：该情况无法由函数自身轻松处理，但又不足以灾难性到让程序完全终止。此外，异常在短距离 `return` 和粗暴的 `exit` 之间提供了一层灵活的控制。

本章将讨论异常。首先给出一个示例，说明异常和 `setjmp`/`longjmp` 组合对程序产生的不同影响。该示例之后讨论异常的形式方面。在这一部分中，将介绍我们的软件在面对异常时应能够提供的保证。异常及其保证会对构造函数和析构函数产生影响。我们将在本章末尾遇到这些影响。

### 10.1 异常语法

在对比传统的 C 语言处理非局部 goto 的方式与异常之前，让我们先介绍使用异常时所涉及的语法元素。

```cpp
    };
    Inner::Inner()
    {
        cout << "Inner constructor\n";
    }
    Inner::~Inner()
    {
        cout << "Inner destructor\n";
    }
    void Inner::fun()
    {
        cout << "Inner fun\n";
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

编译并运行后，程序的输出完全符合预期：析构函数按正确顺序调用（与构造函数的调用顺序相反）。

### 10.2. 使用异常的示例

现在让我们关注两个变体，在其中我们模拟 `Inner::fun` 函数中的一个非致命灾难性事件。据设想，该事件必须在 `main` 的末尾附近处理。

我们将考虑两个变体。在第一个变体中，事件由 `setjmp` 和 `longjmp` 处理；在第二个变体中，事件使用 **C++** 的异常机制处理。

### 10.2.1 时代错误：‘setjmp’ 和 ‘longjmp’

上一节的基本程序被稍作修改，以包含一个由 `setjmp` 和 `longjmp` 使用的变量 `jmp_buf jmpBuf`。

函数 `Inner::fun` 调用 `longjmp`，模拟一个灾难性事件，该事件将在 `main` 的末尾附近处理。在 `main` 中，通过函数 `setjmp` 定义了长跳转的目标位置。`setjmp` 的零返回值表示 `jmp_buf` 变量的初始化，在这种情况下会调用 `Outer::fun`。这种情况代表“正常流程”。

仅当 `Outer::fun` 正常终止时，程序的返回值才为零。然而，程序的设计方式使得这不会发生：`Inner::fun` 调用 `longjmp`。结果，执行流返回到 `setjmp` 函数。在这种情况下，它不会返回零值。因此，在从 `Outer::fun` 调用 `Inner::fun` 之后，会进入 `main` 的 if 语句，程序以返回值 1 终止。在学习下面的程序源代码时，请尝试遵循这些步骤，该源代码是对第 10.2 节中给出的基本程序的直接修改：

```cpp
#include <iostream>
#include <setjmp.h>
#include <cstdlib>

using namespace std;

jmp_buf jmpBuf;

class Inner
{
    public:
        Inner();
        ~Inner();
        void fun();
};

Inner::Inner()
{
    cout << "Inner constructor\n";
}
void Inner::fun()
{
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

该程序的输出清楚地表明，`Inner` 的析构函数没有被调用。这是由 `longjmp` 执行的非局部跳转的直接结果。处理立即从 `Inner::fun` 内部的 `longjmp` 调用转到 `main` 中的 `setjmp`。在那里，其返回值不等于零，程序以返回值 1 终止。由于非局部跳转，`Inner::~Inner` 永远不会被执行：返回到 `main` 的 `setjmp` 时，现有栈被简单拆解，而析构函数还在等待被调用。

这个例子说明，在使用 `longjmp` 和 `setjmp` 时，对象的析构函数很容易被跳过，因此 C++ 程序应当像躲避瘟疫一样避免使用这些函数。

### 10.2.2 异常：首选的替代方案

异常是 C++ 对 `setjmp` 和 `longjmp` 所造成问题的回答。下面是一个使用异常的示例。该程序再次派生自第 10.2 节的基本程序：

```cpp
#include <iostream>
using namespace std;

class Inner
{
public:
    Inner();
    ~Inner();
    void fun();
};
Inner::Inner()
```

当抛出一个 int 值时，该值会重新出现在 `try` 块之后的 `catch` 子句中。

现在 `Inner::fun` 通过抛出异常而不是调用 `longjmp` 来终止。异常在 `main` 中被捕获，程序终止。现在我们看到 `Inner` 的析构函数被正确调用。有趣的是，`Inner::fun` 的执行确实在 `throw` 语句处终止：紧跟在 `throw` 语句之后的 `cout` 语句不会被执行。

这个例子教会了我们什么？

-   异常提供了一种手段，可以打破函数（以及程序）的正常流程，而无需使用一连串的 `return` 语句，也无需使用像函数 `exit` 这样粗暴的工具来终止程序。
-   异常不会破坏析构函数的正确激活。由于 `setjmp` 和 `longjmp` 确实会破坏析构函数的正确激活，因此它们在 C++ 中被强烈不推荐使用。

### 10.3 抛出异常

异常由 `throw` 语句生成。`throw` 关键字后跟一个表达式，定义所抛出的异常值。示例：

```cpp
throw "Hello world";          // throws a char *
throw 18;                    // throws an int
throw string("hello");       // throws a string
```

当函数终止时，局部对象不复存在。对于异常而言也是如此。

函数中局部定义的对象，一旦这些函数抛出的异常离开这些函数，就会被自动销毁。作为异常抛出的对象也是如此。然而，就在离开函数上下文之前，该对象会被复制，而最终到达相应 `catch` 子句的正是这个副本。

下面的示例说明了这个过程。`Object::fun` 定义了一个局部 `Object` `toThrow`，它作为异常被抛出。该异常在 `main` 中被捕获。但到那时，最初抛出的对象已不复存在，而 `main` 接收到的是一个副本：

```cpp
#include <iostream>
#include <string>
using namespace std;

class Object
{
    string d_name;

    public:
        Object(string name)
        :
            d_name(name)
        {
            cout << "Constructor of " << d_name << "\n";
        }
        Object(Object const &other)
        :
            d_name(other.d_name + " (copy)")
        {
            cout << "Copy constructor for " << d_name << "\n";
        }
```
