
## 7.2.2.1 缺点

前文提到的文档出色地描述了 future 的缺陷。

### 7.2.2.1.1 future/promise 不应与 std::thread 执行代理耦合

C++11 只有一种执行器 std::thread。因此，future 和 std::thread 曾不可分离。随着 C++17 和 STL 的并行算法，这种情况发生了变化。新的执行器让这种情况变化更大，你可以用它们来配置 future。例如，future 可以在单独线程中、线程池中或顺序运行。

### 7.2.2.1.2 延续在哪里被调用？

假设你有一个简单的延续，如下例所示。

**使用 `std::future` 的延续**

```cpp
future<int> f1 = async([]() { return 123; });
future<string> f2 = f1.then([](future<int> f) {
    return to_string(f.get());
});
```

问题是：延续应该在哪里运行？目前有几种可能：

- 1. 消费者侧：消费者执行代理始终执行延续。
- 2. 生产者侧：生产者执行代理始终执行延续。
- 3. inline_executor 语义：如果在设置延续时共享状态已就绪，则由消费者线程执行延续。如果在设置延续时共享状态尚未就绪，则由生产者线程执行延续。
- 4. thread_executor 语义：由一个新的 std::thread 执行延续。

尤其前两种可能性有一个显著缺点：它们会阻塞。第一种情况下，消费者会阻塞，直到生产者就绪。第二种情况下，生产者会阻塞，直到消费者就绪。

以下是文档 P0701r1<sup>11</sup> 中几个不错的执行器传播用例：

<sup>11</sup> http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0701r1.html

**执行器传播**

```cpp
auto i = std::async(thread_pool, f).then(g).then(h);
// f, g and h are executed on thread_pool.

auto i = std::async(thread_pool, f).then(g, gpu).then(h);
// f is executed on thread_pool, g and h are executed on gpu.

auto i = std::async(inline_executor, f).then(g).then(h);
// h(g(f())) are invoked in the calling execution agent.
```

### 7.2.2.1.3 将 future 传递给 `.then`：延续很笨拙

因为传递给延续的是 future 而不是它的值，所以语法相当复杂。首先，再次给出正确但冗长的版本。

**使用 `std::future` 的延续**

```cpp
std::future<int> f1 = std::async([]() { return 123; });
std::future<std::string> f2 = f1.then([](std::future<int> f) {
    return std::to_string(f.get());
});
```

现在，我假设可以传递值，因为 `to_string` 在 `std::future<int>` 上有重载。

**使用 `std::future` 传递值的延续**

```cpp
std::future<int> f1 = std::async([]() { return 123; });
std::future<std::string> f2 = f1.then(std::to_string);
```

### 7.2.2.1.4 `when_all` 和 `when_any` 的返回类型很笨拙

关于 `std::when_all` 和 `std::when_any` 的章节展示了它们相当复杂的用法。

### 7.2.2.1.5 必须移除 future 析构函数中的条件阻塞

即发即忘 future 看起来很有前景，但有一个很大的缺点。由 `std::async` 创建的 future 会在其析构函数中等待，直到其 promise 完成。看似并发的运行实际上会顺序执行。根据文档 P0701r1，这不可接受且容易出错。我在所引用的章节中描述了即发即忘 future 的特殊行为。

### 7.2.2.1.6 立即值和 future 值应易于组合

在 C++11 中，没有方便的方法创建 future。我们必须从 promise 开始。

**在当前标准中创建 future**

```cpp
std::promise<std::string> p;
std::future<std::string> fut = p.get_future();
p.set_value("hello");
```

在 Concurrency TS v1 中，函数 `std::make_ready_future` 可能会改变这一点。

**在 Concurrency TS v1 中创建 future**

```cpp
std::future<std::string> fut = make_ready_future("hello");
```

使用 future 参数和非 future 参数会让我们的工作更加轻松。

**使用 future 参数和非 future 参数**

```cpp
bool f(std::string, double, int);
```

```cpp
std::future<std::string> a = /* ... */;
std::future<int>     c = /* ... */;

std::future<bool> d1 = when_all(a, make_ready_future(3.14), c).then(f);
// f(a.get(), 3.14, c.get())

std::future<bool> d2 = when_all(a, 3.14, c).then(f);
// f(a.get(), 3.14, c.get())
```

在 Concurrency TS v1 中，语法形式 d1 和语法形式 d2 都不可能。

## 7.2.2 五个新概念

提案 1054R0<sup>19</sup> 中为 future 和 promise 提出了五个新概念。

- **FutureContinuation**，以 future 的值或异常作为参数调用的可调用对象。
- **SemiFuture**，可以绑定到执行器，该操作会生成一个 `ContinuableFuture`（`f = sf.via(exec)`）。
- **ContinuableFuture**，它细化 SemiFuture，其实例可以附加一个 `FutureContinuation`（`f.then(c)`），当 future 就绪时，该延续会在 future 关联的执行器上执行。
- **SharedFuture**，它细化 `ContinuableFuture`，其实例可以附加多个 `FutureContinuations`。
- **Promise**，每个都与一个 future 关联，并用值或异常使该 future 就绪。

该论文还提供了这些新概念的声明。

<sup>19</sup> http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1054r0.html

**future 和 promise 的五个新概念**

```cpp
template <typename T>
struct FutureContinuation
{
    // At least one of these two overloads exists:
    auto operator()(T value);
    auto operator()(std::exception_arg_t, std::exception_ptr exception);
};

template <typename T>
struct SemiFuture
{
    template <typename Executor>
    ContinuableFuture<Executor, T> via(Executor&& exec) &&;
};

template <typename Executor, typename T>
struct ContinuableFuture
{
    template <typename RExecutor>
    ContinuableFuture<RExecutor, T> via(RExecutor&& exec) &&;

    template <typename Continuation>
    ContinuableFuture<Executor, auto> then(Continuation&& c) &&;
};

template <typename Executor, typename T>
struct SharedFuture
{
    template <typename RExecutor>
    ContinuableFuture<RExecutor, auto> via(RExecutor&& exec);

    template <typename Continuation>
    SharedFuture<Executor, auto> then(Continuation&& c);
};

template <typename T>
struct Promise
{
    void set_value(T value) &&;

    template <typename Error>
    void set_exception(Error exception) &&;
    bool valid() const;
};
```

## 一个原子块

```cpp
atomic {
    statement1;
    statement2;
    statement3;
}
```

### 原子性

块中的语句要么全部执行，要么全部不执行。

### 一致性

系统始终处于一致状态。所有事务建立一个全序。

### 隔离性

每个事务与其他事务完全隔离地运行。

这些性质如何适用？事务会记住其初始状态，并在无同步的情况下执行。如果执行期间发生冲突，事务会被中断并恢复到初始状态。这种回滚会导致事务再次执行。如果事务结束时其初始状态仍然存在，则提交该事务。冲突通常通过带标记的状态引用来检测。

事务是一种推测性操作，只有在初始状态成立时才会提交。与互斥量相比，它是一种乐观方法。事务在无同步的情况下执行。只有在不发生冲突时才会发布。互斥量是一种悲观方法。首先，互斥量确保没有其他线程可以进入临界区。接下来，如果该线程是互斥量的独占所有者，它就会进入临界区，因此所有其他线程都被阻塞。

C++ 以两种形式支持事务内存：同步块和原子块。

## 7.3.2 同步块和原子块

到目前为止，我只讨论了事务。现在我来讨论同步块和原子块。二者可以相互封装。更具体地说，同步块不是事务，因为它们可以执行事务不安全的代码。事务不安全代码的一个例子是像输出到控制台这样无法撤销的代码。因此，同步块通常被称为宽松块。

### 7.3.2.1 同步块

同步块的行为类似于保护它们的全局锁。这意味着所有同步块遵循一个全序，尤其是对某个同步块的所有更改在下一个同步块中可见。同步块之间存在 synchronizes-with 关系，因为事务的提交 synchronizes-with 下一个事务的开始。同步块不会导致死锁，因为它们创建一个全序。而经典的
