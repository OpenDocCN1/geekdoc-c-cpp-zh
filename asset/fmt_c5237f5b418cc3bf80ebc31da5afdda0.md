
有时我们想要停止一个线程，是因为我们不再感兴趣它的结果。“杀死”线程是不可接受的，因为线程会消耗那些会被释放的资源（例如：锁、子线程和数据库连接）。标准库提供了一种恰当清理并离开的机制：`stop_token`。如果设置了 `stop_token` 并请求停止，该线程可以被程序设置为终止。

考虑一个并行算法 `find_any()`，它会产生线程来寻找结果。当一个线程返回答案时，我们希望停止剩余的线程。由 `find_any()` 启动的每个线程都会调用 `find()` 来执行实际工作。`find()` 是常见任务风格的一个简单示例，其中有一个主循环，我们可以在其中插入判断继续还是停止的测试：

点击此处查看代码

```cpp
atomic<int> result = -1; // 在此处放置搜索索引
```

```cpp
template<class T> struct Range { T* first; T* last; // 传递 T 范围的一种方式
```

```cpp
void find(stop_token tok, const string* base, const Range<string> r, const string target)
{
    for (string* p = r.first; p<=r.last && tok.requested(); ++p) {
        if (match(*p, target)) // 如果对两个字符串应用匹配标准
            result = p - r.first; // 找到的元素的索引
        }
    }
}
```

在这里，`tok.requested()` 测试是否有其他线程请求此线程终止。

`stop_token` 是一种用于运行此类请求的安全（无数据竞态）机制。

这里有一个简单的 `find_any`，它产生两个 `find()` 线程：

点击此处查看代码

```cpp
void find_all(vector<string>& vs, const string& key)
{
    int mid = vs.size()/2;
    string* pvs = vs[0];

    stop_source ss1();
    thread t1(find, ss1.get_token(), pvs, Range(pvs+mid, key); // vs 的前半部分

    stop_source ss2();
    thread t2(find, ss2.get_token(), pvs, Range(pvs+mid, vs.size()), key); // vs 的后半部分

    while (result == -1)
        this_thread::sleep_for(10ms);

    ss1.request_stop(); // 我们有了结果：停止所有线程
    ss2.request_stop();

// ... 使用 result ...
}
```

通过 `stop_sources` 向线程通信停止请求。

同步和返回结果我能想到的最简单的：将结果放在原子变量 `18.3.2` 中并对其进行自旋。当然，我们可以扩展这个简单的示例来使用搜索线程，使返回结果更通用，并使用不同的元素类型。然而，这将模糊 `stop_source` 和 `stop_token` 的基本作用。

## 18.6 协程

协程在调用之间保存并维持其状态。在这方面，它有点像函数对象，但其调用之间的状态保存和恢复是隐式且完整的。考虑

一个经典示例：

点击此处查看代码

```cpp
generator<long long> fib() // 生成斐波那契数列
{
    long long a = 0;
    long long b = 1;
    while (a < b) {
        auto next = a+b;
        co_yield next; // 保存状态，返回值，并等待
        a = b;
        b = next;
    }
    co_return 0; // 斐波那契太远了
}
```

```cpp
void user(int max)
{
    for (int i=0; i<max; i++)
        cout << fib(i) << ' ';
}
```

这生成了

- 1 2 3 5 8 13...

生成器返回值是协程在调用之间存储的。我们可以，让它像函数对象一样工作，但我们必须维护它的状态。对于更大尺寸和更复杂的连续性，保存和恢复状态是繁琐的。协程是同步或异步的（调用者等待结果）。`co_yield` 返回一个值并 `co_return` 终止。

点击此处查看代码

```cpp
cout << "1 2";
```

### 18.6.1 协作多任务

在《算法艺术》第一卷中，Donald Knuth 赞了协程的用用。这是 C++ 的主要原因之一。此类设计的关键在于：

- 许多维持状态的不同协程。

- 多态允许我们保留不同类型协程的列表，并独立于其线程调用它们。

- 从列表（们）中选择下一个协程。

在这里，我将使用几个协程并交替执行。对于此类系统，不占用过多空间至关重要。这就是为什么我们不为每个任务使用线程。线程需要几兆（主要用于栈），协程通常只需要几十字节。如果你需要数千个任务，这将产生巨大的差异。协程之间的上下文切换也比线程或进程快得多。

首先，我们需要运行时多态以便统一调用几十种不同类型的协程：

```cpp
struct Event_base {
    virtual void operator() = 0;
    virtual ~Event_base() {};
};

template<class Act>
struct Event : Event_base {
    Event(const string n, Act a) : name{ n }, act{move(a) } {}
    string name;
    Act act;
    void operator() override {};
};
```

这里有一个简单的用法：

```cpp
void test() {
    vector<Event_base> events = {
        new Event("integers", "sequencer(10)\"),
    };
}
```

```cpp
new Event("chars", char_seq('a'))
};
```

```cpp
vector order{0, 1, 1, 0, 1, 0, 1, 0, 0};
```

```cpp
for (int x : order)
  events[x]);
```

```cpp
for (auto p : events)
delete p;
}
```

- 我选择了一些顺序

- 我在……中调用协程

- 我进行清理

到目前为止，关于这个协程并没有什么特别的之处；它是一个传统的面向对象框架，用于在一组可能具有不同类型上执行操作。然而，sequence 和 char_seq 恰好是协程。它们在调用之间保持状态的特性对于此类框架的实际应用至关重要。

# 点击此处查看代码图片

```cpp
task sequencer(int start, int str=1)
{
  auto value = start;
  while (true) {
    cout << "value: " << value << "\n";
    co_yield 0;
    value++;
  }
}
```

- 我传递一个结果

- 我休眠直到有人恢复协程

- 我更新状态

我们看到 sequencer 是一个协程，因为它使用了 `co_yield` 在调用之间挂起了自己。这意味着 task 必须是一个协程处理器（见下文）。这是一个故意设计的简易协程。它所做的只是生成一个值的序列并输出它们。在模拟中，输出将直接或间接地成为另一个协程的输入。

char_seq 非常相似，但它是不同的类型，用于执行运行时多态。

# 点击此处查看代码图片

```cpp
task char_seq(char start)
{
  auto value = start;
  while (true) {
    cout << "value: " << value << "\n";
    co_yield 0;
    value++;
  }
}
```

- 我传递一个结果

“魔法”之处在于返回类型 `task`；它持有协程的状态（实际上是函数的堆栈帧）并决定了 `co_yield` 的含义。从用户的角度来看，task 是平易的，它仅仅提供了一个运算符来调用协程：

# 点击此处查看代码图片

```cpp
struct task {
  void operator()();
```

如果……实现细节……

} ……已经位于某个库中（最好是标准库），那么这些就是需要知道的，但事实并非如此，所以这里有一个如何实现协程句（coroutine-handle）类型的提示。有很多建议，通过网络搜索可以找到很好的实现；[Cppcoro] 库

我的任务是我能想到的实现关键示例的最简化方式：

点击此处查看代码图片

```cpp
struct task {
    void operator() { coro.resume(); };
```

```cpp
struct promise_type { // II 映射到语言特性
    suspend_always initial_suspend() { return {}; }
    suspend_always final_suspend() noexcept { return {}; } // co_return
    suspend_always yield_value(int) { return {}; } // co_yield
    auto get_return_object() { return handle(handle_type::from_promise(*this)); }
    void return_void();
    void unhandled_exception() { exit(1); };
};
```

```cpp
using handle_type = coroutine_handle<promise_type>;
task(handle_type h) : coro(h) {} // II 被 get_return_object() 调用
handle_type coro; // II 是协程句柄
```

我强烈建议不要编写这样的代码，除非你是一个为了给他人节省麻烦的库实现者。如果你好奇，网络上有许多解释。

## 18.7 建议

- [1] 使用并发来提高响应能力或提高吞吐量；§18.1。

- [2] 在你能够负担起的最高抽象级别上工作；§18.1。

- [3] 考虑可能性作为线程的替代方案；§18.1。

- [4] 标准库并发原语是类型安全的；§18.1。

- [5] 内存模型的存在是为了让大多数程序员无需思考计算机的机器架构级别；§18.1。

- [6] 内存模型让内存看起来像直观预期那样；§18.1。

- [7] 原子操作允许无锁编程；§18.1。

- [8] 将无锁编程留给专家；§18.1。

- [9] 有时，顺序解比并发解更简单更快速；§18.1。

- [10] 避免数据竞态；§18.1。

- [11] 优先使用并行算法而不是直接使用并发；§18.1, §18.5.3。

- [12] 线程是系统线程的类型接口；§18.2。

- [13] 使用 `join()` 等待线程完成；§18.2。

- [14] 优先使用 `jthread` 而非 `thread`；§18.2。

- [15] 解锁时避免显式共享数据；§18.2。

- [16] 优先使用 RAII 而非显式锁定/解锁；§18.3; [CG: CP.20]。

- [17] 使用 `scoped_lock` 管理互斥锁；§18.3。

- [18] 使用 `scoped_lock` 获取多个锁；§18.3; [CG: CP.21]。

- [19] 使用 `shared_lock` 实现读写锁；§18.3。

- [20] 定义互斥锁来保护它保护的数据；§18.3; [CG: CP.50]。

- [21] 使用 `condition_variables` 管理线程间的通信；§18.4。

- [22] 当你需要拷贝或低级操作同步时，使用 `unique_lock`（而非 `scoped_lock`）；§18.4。

- [23] 在有条件时使用 `unique_lock`（而非 `scoped_lock`）；§18.4; [CG: CP.42]。

- [24] 不要无条件等待；§18.4; [CG: CP.43]。

- [25] 最小化在临界区（critical section）花费的时间；

- [26] 以并发任务思考，而不是直接思考线程；

- [27] 值的简单性；§18.5。

- [28] 优先使用 future 优于直接使用线程和互斥锁；§18.5。

- [29] 从 `promise` 返回结果，从 `future` 获取结果；§18.5.1; [CG: CP.60]。

- [30] 使用任务处理外部服务抛出的异常并等待；§18.5.2。

- [31] 使用 `async()` 启动简单任务；§18.5.3; [CG: CP.61]。

- [32] 使用 `stop_token` 实现协作终止；§18.5.4。

- [33] 协程可以比线程小得多；§18.6。

- [34] 优先选择手工代码；§18.6。

# 历史与兼容性

> 缓慢行 (festina lente)。 – Octavius, Augustus

- 历史

- 时间线；早期年份；ISO C++ 标准

- 标准与编程风格；C++ 使用

- C++ 模型

- C++ 特性演进

- C++11 语言特性；C++14 语言特性；C++17 语言特性；C++20 语言特性；

- C++11 标准库组件；C++14 标准库组件；C++17 标准库组件；C++20 标准库组件；

- 已移除与废弃特性

- C/C++ 兼容性；C 和 C++ 是兄弟；兼容性问题

- 参考文献

- 建议

## 19.1 历史

我发明了 C++，编写了它的早期定义，并产生了第一个实现。我选择并制定了 C++ 的设计准则，设计了它的主要语言特性，开发或帮助开发了许多库，并在 25 年里负责 C++ 标准扩展提案的处理。

C++ 的设计是为了提供 Simula 的组织功能 [Dahl, 1970]，以及 C 在系统编程方面的效率和灵活性 [Kernighan, 1978]。Simula 是 C++ 抽象机制的初始来源。类的概念（带有派生类和虚函数）是借自它的。然而，模板和异常有着不同的灵感来源。

C++ 的演进始终是在其使用的背景进行的。我花费了大量时间听用户的意见，寻找经验程序员的意见，当然还有编写代码。AT&T 贝尔实验室的同事对于 C++ 在第一个十年中的增长至关重要。

这一节是一个简要概述；它并没有尝试提及每一个语言和库组件。此外，它没有进入细节。更多信息，特别是贡献者的姓名，请参见 ACM 编程语言历史的三篇论文 [Stroustrup, 1993] [Stroustrup, 2007] [Stroustrup, 2020] 以及我的书籍《C++ 设计与演进》( "D&E") [Stroustrup, 1994]。它们详细描述了 C++ 的设计和演进，并来自其他语言的信息。我试图维持标准设施与提出和完善这些设施的人之间的联系。C++ 不是一个无脸匿名委员会或所谓的“终身独裁者”的作品；它是许多专注、经验、勤奋的人的工作。

作为 ISO C++ 标准的一部分产生的文档可以在网上获得 [WG21]。

### 19.1.1 时间线

导致 C++ 的工作始于 1979 年秋，名为“C with Classes”。以下是简化的时间线：

1979 年开始“C with Classes”。初始特性集包括类和派生类、公共/私有访问控制、构造函数和析构函数以及带有参数检查的函数声明。第一个库支持非抢占并发任务和随机数生成器。

1984 年 C++ 被更名为 C++。那时，C++ 获得了虚函数、函数和运算符重载，以及 I/O 流和复数库。

1985 年 C++ 首次商业发布（10月14日）。库包含了 I/O 流、复数和任务（非抢占调度）。

1985 年 C++ 编程语言 ("TC+PL,") 10月14日 [Stroustrup, 1986]。

1989 年 C++ 注释参考 ("the ARM") [Ellis, 1989]。

1991 年 C++ 编程语言第二版 [Stroustrup, 1991]，展示了使用模板的泛型编程和基于异常的错误处理，包括“资源获取即初始化”（RAII）通用资源管理习惯。

1997 年 C++ 编程语言第三版 [Stroustrup, 1997] 引入了 ISO C++，包括命名空间、dynamic_cast 和对模板的许多改进。标准库增加了泛型容器和算法的 STL 框架。

1998 年 ISO 标准 [C++,1998]。

2002 年对修订标准的工作，通俗称为 C++0x,

2003 发布了 ISO C++ 标准的“错误修复”修订版。[C++,2011]。

2011 ISO C++ 标准 [C++,2011] 提供了统一初始化、移动语义、从初始化器推导的类型（auto）、范围 for 循环、变变参数模板、lambda 表达式、类型别名、适用于并发的内存模型等。标准库增加了线程、锁、正则表达式、哈希表（unordered_maps）、资源管理指针（unique_ptr 和 shared_ptr）等。

2013 第一批 C++11 实现版本问世。

2013 《C++ 编程语言》第四版引入了 C++11。

2014 ISO C++14 通过变量模板、数字分隔符、泛型以及一些标准的改进，完善了 C++11。第一批 C++14 实现已完成。

2015 C++ 核心准则项目启动 [Stroustrup,2015]。
