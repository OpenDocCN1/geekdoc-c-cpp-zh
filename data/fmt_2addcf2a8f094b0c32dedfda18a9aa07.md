
编译并运行后，程序的输出完全符合预期：析构函数按照正确的顺序被调用（与构造函数的调用顺序相反）。

现在，让我们关注两种变体，在这两种变体中，我们在 `Inner::fun` 函数中模拟的非致命灾难性事件必须在 `main` 附近处理。

我们将考虑两种变体。在第一种变体中，通过 `setjmp` 和 `longjmp` 处理事件；在第二种变体中，使用 C++ 异常机制处理事件。

### 10.2.1 时代错误的用法：‘setjmp’和‘longjmp’

基础程序经过微调，通过 `setjmp` 和 `longjmp` 处理在 `Inner::fun` 中模拟的灾难性事件。函数 `Inner::fun` 调用 `longjmp`，在 `main` 附近处理。

```cpp
#include <iostream>
#include <setjmp.h>
#include <stdlib.h>
using namespace std;
jmp_buf env;
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
    longjmp(env, 1);
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
    if (setjmp(env, 1) == 0) {
        Outer out;
        out.fun();
    } else {
        cout << "Exception handled via longjmp\n";
    }
    return 0;
}
/*
生成的输出:
Outer constructor
Inner constructor
Outer fun
Inner fun
Inner destructor
Outer destructor
Exception handled via longjmp
*/
```

基础程序经过微调，通过 C++ 异常处理在 `Inner::fun` 中模拟的灾难性事件。函数 `Inner::fun` 抛出异常，在 `main` 附近处理。

```cpp
#include <iostream>
#include <string>
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
        cout << "Exception handled via exception\n";
    }
    return 0;
}
/*
生成的输出:
Outer constructor
Inner constructor
Outer fun
Inner fun
Inner destructor
Outer destructor
Exception handled via exception
*/
```

### 10.2.2 异常：首选的替代方案

局部对象在函数终止时销毁。这与异常没有区别。定义在函数中的对象在被这些函数抛出时会自动销毁。异常也适用于此类对象。然而，在离开函数上下文之前，对象会被复制，而正是这个副本最终到达了合适的 `catch` 子句。

以下示例说明了这一过程。`Object::fun` 定义了一个局部对象 `toThrow`，异常在 `main` 中被捕获。但此时原始对象已经不存在了，`main` 接收的是副本：

```cpp
#include <iostream>
#include <string>
using namespace std;
class Object
{
    string d_name;
    public:
        Object(string d_name)
        {
            cout << "Constructor of " << d_name << "\n";
        }
        Object(const Object &other):d_name(other.d_name + " (copy)")
        {
            cout << "Copy constructor for " << d_name << "\n";
        }
        ~Object()
        {
            cout << "Destructor of " << d_name << "\n";
        }
        void toThrow("local object")
        {
            cout << "Calling function of " << d_name << "\n";
            throw toThrow();
        }
    };
};
```
