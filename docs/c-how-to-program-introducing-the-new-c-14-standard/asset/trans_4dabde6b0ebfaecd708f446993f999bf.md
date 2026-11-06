
其中类型参数的所有出现都被替换为指定类型。另一个关键区别是，我们*没有*将类模板的接口与其实现分离。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2235_0.png)

### 软件工程观察 18.2

*模板通常定义在头文件中，然后在相应的客户端源代码文件中被* `#include` *包含。对于类模板，这意味着成员函数也定义在头文件中——通常是在类定义的主体内部，就像我们在* ***图 18.2*** *中所做的那样。*

```cpp
// Fig. 18.2: Stack.h
// Stack class template.
#ifndef STACK_H
#define STACK_H
#include <deque>

template<typename T>
class Stack {
public:
    // return the top element of the Stack
    const T& top() {
        return stack.front();
    }

    // push an element onto the Stack
    void push(const T& pushValue) {
        stack.push_front(pushValue);
    }

    // pop an element from the stack
    void pop() {
        stack.pop_front();
    }

    // determine whether Stack is empty
    bool isEmpty() const {
        return stack.empty();
    }

    // return size of Stack
    size_t size() const {
        return stack.size();
    }

private:
    std::deque<T> stack; // internal representation of the Stack
};

#endif
```

图 18.2 Stack *类模板。*

### 18.2.2 类模板 `Stack<T>` 的数据表示

**第15.7.1节** 表明，标准库的 `stack` 适配器类可以使用各种容器来存储其元素。当然，`stack` *只* 在其 *顶部* 需要插入和删除。因此，例如，可以使用 `vector` 或 `deque` 来存储 `stack` 的元素。`vector` 支持在其 *后端* 进行快速插入和删除。`deque` 支持在其 *前端* 和 *后端* 进行快速插入和删除。`deque` 是标准库 `stack` 适配器的默认表示，因为 `deque` 的增长比 `vector` 更高效。`vector` 被维护为一块 *连续* 的内存——当该块已满并且要添加新元素时，`vector` 会分配一块更大的连续内存，并将旧元素 *复制* 到新块中。另一方面，`deque` 通常实现为一系列固定大小的内置数组——必要时会添加新的固定大小内置数组，并且当新项添加到前端或后端时，不会复制任何现有元素。出于这些原因，我们使用 `deque`（第36行）作为 `Stack` 类的底层容器。

### 18.2.3 类模板 `Stack<T>` 的成员函数

类模板的成员函数定义是 *函数模板*，但当它们定义在类模板的主体内部时，前面不会带 `template` 关键字和尖括号（`<` 和 `>`）中的模板参数。不过，如你所见，它们确实使用类模板的模板参数 `T` 来表示元素类型。我们的 `Stack` 类模板*没有*定义自己的构造函数——编译器提供的 *默认构造函数* 将调用 `deque` 的默认构造函数。我们还在**图 18.2**中提供了以下成员函数：

- `top`（第11–13行）返回对 `Stack` 栈顶元素的 `const` 引用。
- `push`（第16–18行）将一个新元素放到 `Stack` 的顶部。
- `pop`（第21–23行）移除 `Stack` 的栈顶元素。
- `isEmpty`（第26–28行）返回一个 `bool` 值——如果 `Stack` 为空则为 `true`，否则为 `false`。
- `size`（第31–33行）返回 `Stack` 中元素的数量。

这些成员函数中的每一个都会调用类模板 `deque` 的相应成员函数——这称为**委托**。

### 18.2.4 在类模板定义之外声明类模板的成员函数

尽管我们在 `Stack` 类模板中*没有*这样做，但成员函数定义可以出现在类模板定义的*外部*。如果这样做，每个成员函数定义都必须以 `template` 关键字开头，后跟与类模板*相同*的一组模板参数。此外，成员函数必须用类名和作用域解析运算符限定。例如，可以在类模板定义之外定义 `pop` 函数，如下所示：

```cpp
template<typename T>
inline void Stack<T>::pop() {
    stack.pop_front();
}
```

`Stack<T>::` 表示 `pop` 位于类 `Stack<T>` 的作用域中。标准库的容器类倾向于在其类定义*内部*定义所有成员函数。

### 18.2.5 测试类模板 `Stack<T>`

现在，让我们考虑练习 `Stack` 类模板的驱动程序（图 18.3）。该驱动程序首先实例化对象 `doubleStack`（第8行）。该对象被声明为 `Stack<double>`（读作“`double` 的 `Stack`”）。编译器将类型 `double` 与类模板中的类型参数 `T` 关联起来，以生成一个元素类型为 `double` 的 `Stack` 类的源代码，该类实际上将其元素存储在 `deque<double>` 中。

```cpp
// Fig. 18.3: fig18_03.cpp
// Stack class template test program.
#include <iostream>
#include "Stack.h" // Stack class template definition
using namespace std;

int main() {
    Stack<double> doubleStack; // create a Stack of double
    const size_t doubleStackSize{5}; // stack size
    double doubleValue{1.1}; // first value to push

    cout << "Pushing elements onto doubleStack\n";

    // push 5 doubles onto doubleStack
    for (size_t i{0}; i < doubleStackSize; ++i) {
        doubleStack.push(doubleValue);
        cout << doubleValue << ' ';
        doubleValue += 1.1;
    }

    cout << "\n\nPopping elements from doubleStack\n";

    // pop elements from doubleStack
    while (!doubleStack.isEmpty()) { // loop while Stack is not empty
        cout << doubleStack.top() << ' '; // display top element
        doubleStack.pop(); // remove top element
    }

    cout << "\nStack is empty, cannot pop.\n";

    Stack<int> intStack; // create a Stack of int
    const size_t intStackSize{10}; // stack size
    int intValue{1}; // first value to push

    cout << "\nPushing elements onto intStack\n";

    // push 10 integers onto intStack
    for (size_t i{0}; i < intStackSize; ++i) {
        intStack.push(intValue);
        cout << intValue++ << ' ';
    }

    cout << "\n\nPopping elements from intStack\n";

    // pop elements from intStack
    while (!intStack.isEmpty()) { // loop while Stack is not empty
        cout << intStack.top() << ' '; // display top element
        intStack.pop(); // remove top element
    }

    cout << "\nStack is empty, cannot pop." << endl;
}
```

```text
Pushing elements onto doubleStack
1.1 2.2 3.3 4.4 5.5

Popping elements from doubleStack
5.5 4.4 3.3 2.2 1.1
Stack is empty, cannot pop.

Pushing elements onto intStack
1 2 3 4 5 6 7 8 9 10

Popping elements from intStack
10 9 8 7 6 5 4 3 2 1
Stack is empty, cannot pop.
```

**图 18.3** Stack 类模板 `test` 程序。

第15–19行调用 `push`（第16行），将 `double` 值 1.1、2.2、3.3、4.4 和 5.5 放入 `doubleStack`。接下来，第24–27行在 *while* 循环中调用 `top` 和 `pop`，从栈中移除这五个值。请注意，在**图 18.3**的输出中，这些值按*后进先出*的顺序 `pop` 出。当 `doubleStack` 为空时，`pop` 循环终止。

第31行通过以下声明实例化 `int` 栈 `intStack`：

```cpp
Stack<int> intStack;
```

（读作“`intStack` 是一个由 `int` 构成的 `Stack`”）。第38–41行反复调用 `push`（第39行）将值放入 `intStack`，然后第46–49行反复调用 `top` 和 `pop`，从 `intStack` 中移除值，直到它为空。再次注意，在输出中，这些值按后进先出的顺序 `pop` 出。

## 18.3 用于操作类模板特化对象的函数模板

**图 18.3** 中函数 `main` 里的代码，对于第8–29行中的 `doubleStack` 操作和第31–51行中的 `intStack` 操作来说，*几乎完全相同*。这提供了另一个使用函数模板的机会。**图 18.4** 定义了函数模板 `testStack`（第10–36行），以执行与**图 18.3**中的 `main` 相同的任务——将一系列值 *推入* `Stack<T>`，并从 `Stack<T>` 中 *弹出* 这些值。
