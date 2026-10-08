

doubleComp4(vector<double>& v)
如果 v 足够大，它会产生很多任务

```cpp
{
    if (v.size()<10000)
        return accum(v.begin(),v.end(),0.0);

    auto v0 = &v[0];
    auto sz = v.size();

    auto f0 = async(accum,v0,v0+sz/4,0.0);
    auto f1 = async(accum,v0+sz/4,v0+sz/2,0.0);
    auto f2 = async(accum,v0+sz/2,v0+sz/3,0.0);
    auto f3 = async(accum,v0+sz/3,v,0.0);

    return f0.get()+f1.get()+f2.get()+f3.get();
}
```

基本上，`async()` 将函数的“调用部分”与“获取结果部分”分离开，并将两者都与任务的实际执行分开。使用 `async()`，你不需要考虑线程和锁。相反，你应该从可能异步计算结果的任务的角度来思考。这里有一个显而易见的局限性：不要为共享资源加载的任务考虑使用 `async()`。使用 `async()`，你甚至不知道将使用多少线程，因为 `async` 会根据它对调用时可用系统资源的了解来做出决断。例如，`async()` 可以在决定使用多少线程之前检查是否有空闲的内核（处理器）。

这种根据对计算成本相对于启动线程成本的猜测来做出判断（例如 `v.size()<10000`）是非常原始（prime，此处可能指原始/草率）的，且容易出错。然而，这里并不是正式讨论如何管理线程的地方。不要将其估计为不仅仅是一个简单且可能是错误的猜测。

通常没有必要并行化标准库算法（例如 `reduce(par_unseq,...))`），我通常在这方面做得更好（§17.3.1）。然而，这种技术是通用的。

请注意，`async()` 不仅仅是一种提高性能的并行计算机制。它也可以用于启动一个任务来获取用户信息，从而让“主程序”去处理其他事情 (§18.5.3)。

## 18.5.4 停止线程

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
同步和返回结果我能想到的最简单的：将结果放在原子变量 (18.3.2) 中并对其进行自旋。当然，我们可以扩展这个简单的示例来使用搜索线程，使返回结果更通用，并使用不同的元素类型。然而，这将模糊 `stop_source` 和 `stop_token` 的基本作用。

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

