
## 13.0.1 栈

![](img/d61a6c83410484053b8892275d2fcc4f_605_0.png)

`std::stack`¹ 遵循 LIFO 原则（后进先出）。栈 `sta` 需要头文件 `<stack>`，它有三个成员函数。

使用 `sta.push(e)` 可以在栈顶插入新元素 `e`，使用 `sta.pop()` 从栈顶移除它，并使用 `sta.top()` 引用它。该栈支持比较运算符，并且知道自身大小。栈的操作具有常数复杂度。

```cpp
#include <stack>
...
std::stack<int> myStack;

std::cout << myStack.empty() << '\n';   // true
std::cout << myStack.size() << '\n';    // 0

myStack.push(1);
myStack.push(2);
myStack.push(3);
std::cout << myStack.top() << '\n';     // 3

while (!myStack.empty()){
    std::cout << myStack.top() << " ";
    myStack.pop();
}
std::cout << '\n';                      // 3 2 1

std::cout << myStack.empty() << '\n';   // true
std::cout << myStack.size() << '\n';    // 0
```

下面我逐步实现并发栈。

### 13.0.1.1 简化实现

我的第一个实现只支持 `push` 成员函数。类 `ConcurrentStackPush` 是 `std::stack` 的一层薄封装。

¹http://en.cppreference.com/w/cpp/container/stack

### 一个支持 push 的并发栈

```cpp
// concurrentStackPush.cpp

#include <list>
#include <mutex>
#include <stack>
#include <string>
#include <utility>
#include <vector>

template<typename T, template <typename, typename> class Cont = std::deque>
class ConcurrentStackPush{
public:
    void push(T val){
        std::lock_guard<std::mutex> lockStack(mutexStack);
        myStack.push(std::move(val));
    }
    ConcurrentStackPush() = default;
    ConcurrentStackPush(const ConcurrentStackPush&) = delete;
    ConcurrentStackPush& operator= (const ConcurrentStackPush&) = delete;
private:
    mutable std::mutex mutexStack;
    std::stack<T, Cont<T, std::allocator<T> >> myStack;
};

int main(){

    ConcurrentStackPush<int> conStack;
    conStack.push(5);

    ConcurrentStackPush<double, std::vector> conStack2;
    conStack2.push(5.5);

    ConcurrentStackPush<std::string, std::list> conStack3;
    conStack3.push("hello");

}
```

从并发的角度看，类型 ConcurrentStackPush 支持 push 成员函数（第 13 至 16 行），该函数将一个新元素复制到内部的 myStack（第 22 行）。得益于第 21 行的 mutexStack，该复制操作是线程安全的。我猜你会对第二个模板参数感到困惑：`template <typename, typename> class Cont = std::deque`。第二个模板参数是所谓的模板模板参数。其默认值是 `std::deque`。Cont 是用于存放元素的容器。Cont 需要其参数的类型和分配器。在第 22 行，可以看到参数 Cont 的用法。Cont 是内部 std::stack 的第二个参数。第 27、30 和 33 行展示了如何用各种容器实例化 ConcurrentStackPush。conStack（第 27 行）使用 std::deque，conStack2（第 30 行）使用 std::vector，而 conStack3（第 33 行）使用 std::list。std::stack 以及后面的 std::queue 是所谓的容器适配器，因为它们使用现有容器并支持类似栈或类似队列的接口。

你可能会问，为什么我在单线程环境中使用 ConcurrentStackPush，以及为什么没有展示任何输出。我的回答是：只有一个成员函数 push 限制太大。ConcurrentStackPush 只应作为完整实现的起点。

### 13.0.1.2 完整实现

根据信息框中的栈，我的并发栈至少应支持成员函数 push、pop 和 top。

你可能认为，对之前的类型 ConcurrentStackPush 进行直接扩展就能完成任务。这个假设是错误的。

### 一个有缺陷的并发栈

```cpp
template<typename T, template <typename, typename> class Cont = std::deque>
class ConcurrentStackBroken {
public:
    void push(T val) {
        std::lock_guard<std::mutex> lockStack(mutexStack);
        myStack.push(std::move(val));
    }
    void pop() {
        std::lock_guard<std::mutex> lockStack(mutexStack);
        myStack.pop();
    }
    T& top() {
        std::lock_guard<std::mutex> lockStack(mutexStack);
        return myStack.top();
    }
    ConcurrentStackBroken() = default;
    ConcurrentStackBroken(const ConcurrentStackBroken&) = delete;
    ConcurrentStackBroken& operator= (const ConcurrentStackBroken&) = delete;
private:
    mutable std::mutex mutexStack;
    std::stack<T, Cont<T, std::allocator<T>>> myStack;
};
```

可能基于 conStack 拥有有效元素这一错误假设而按顺序发生。当然，这三个 std::async 都会交错执行，因此可能发生以下操作序列。操作 top 和 pop 不会交错，因为它们使用同一个互斥量。

### 一种可能的交错

```
conStack.top()   // associated promise to 'fut'
conStack.top()   // associated promise to 'fut2'
conStack.top()   // associated promise to 'fut3'
conStack.pop()   // associated promise to 'fut'      // (2)
conStack.pop()   // associated promise to 'fut2'     // (2)
conStack.pop()   // associated promise to 'fut3'     // (3)
```

构造出的操作序列是致命的。通过调用 (2)，SENTINEL 被移除，因此不变量被破坏。调用 (3) 具有未定义行为，因为对 std::stack 调用 pop 会触发内部容器上的 pop_back 调用。对空容器调用 pop_back 是未定义行为。

更改并发数据结构的接口通常是克服并发问题的一种可行方法。在本例中，我改变接口的粒度，并将成员函数 top 和 pop 合并为一个成员函数 topAndPop。当然，这种对成员函数 top 和 pop 的合并违反了单一职责原则*。

### 一个并发栈

```cpp
1    // concurrentStack.cpp
2
3    #include <future>
4    #include <limits>
5    #include <iostream>
6    #include <mutex>
7    #include <stack>
8    #include <stdexcept>
9    #include <utility>
10
11   template<typename T, template <typename, typename> class Cont = std::deque>
12   class ConcurrentStack {
13   public:
14       void push(T val) {
15           std::lock_guard<std::mutex> lockStack(mutexStack);
16           myStack.push(std::move(val));
17       }
18       T topAndPop() {
19           std::lock_guard<std::mutex> lockStack(mutexStack);
20           if ( myStack.empty() ) throw std::out_of_range("The stack is empty!");
21           auto val = myStack.top();
22           myStack.pop();
23           return val;
24       }
25       ConcurrentStack() = default;
26       ConcurrentStack(const ConcurrentStack&) = delete;
27       ConcurrentStack& operator = (const ConcurrentStack&) = delete;
28   private:
29       mutable std::mutex mutexStack;
30       std::stack<T, Cont<T, std::allocator<T>>> myStack;
31   };
32
33   int main() {
34
35       ConcurrentStack<int> conStack;
36
37       auto fut = std::async([&conStack] { conStack.push(2011); });
38       auto fut1 = std::async([&conStack] { conStack.push(2014); });
39       auto fut2 = std::async([&conStack] { conStack.push(2017); });
40
41       auto fut3 = std::async([&conStack] { return conStack.topAndPop(); });
42       auto fut4 = std::async([&conStack] { return conStack.topAndPop(); });
43       auto fut5 = std::async([&conStack] { return conStack.topAndPop(); });
44
45       fut.get(), fut1.get(), fut2.get();
46
47       std::cout << fut3.get() << '\n';
48       std::cout << fut4.get() << '\n';
49       std::cout << fut5.get() << '\n';
50
51   }
```

> *https://en.wikipedia.org/wiki/Single_responsibility_principle

成员函数 topAndPop（第 18 至 24 行）返回副本，而不是像之前的成员函数 top 那样返回引用。对空容器调用 pop 是未定义行为。如果栈为空，我更倾向于抛出 std::out_of_range 异常（第 20 行）。返回一个特殊的非值，或返回 std::optional¹，也是有效选项。复制该值有一个缺点。如果值类型的复制构造函数抛出诸如 std::bad_alloc² 的异常，该值就会丢失。

调用 fut.get()、fut1.get()、fut2.get()（第 45 行）可确保关联的 promise 运行。如果未指定启动策略，promise 可能会在调用者线程中惰性运行。惰性意味着，仅当 future 通过 get 或 wait 请求其结果时，promise 才会执行。在单独线程中启动这些 promise 也是有效选项：

¹https://en.cppreference.com/w/cpp/utility/optional
²https://en.cppreference.com/w/cpp/memory/new/bad_alloc

