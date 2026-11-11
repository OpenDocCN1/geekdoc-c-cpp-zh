
## 7.2.2.1 Disadvantages

The already mentioned document gives an excellent description of the deficiencies of the futures.

### 7.2.2.1.1 future/promise Should Not Be Coupled to std::thread Execution Agents

C++11 had only one executor std::thread. Consequently, futures and std::thread were inseparable. This changed with C++17 and the parallel algorithms of the STL. This changes even more with the new executors, which you can use to configure the future. For example, the future may run in a separate thread, in a thread pool, or sequentially.

### 7.2.2.1.2 Where Are the Continuations Invoked?

Imagine you have a simple continuation, such as in the following example.

**Continuations with `std::future`**

```cpp
future<int> f1 = async([]() { return 123; });
future<string> f2 = f1.then([](future<int> f) {
    return to_string(f.get());
});
```

The question is: Where should the continuation run? There are a few possibilities today:

- 1. Consumer Side: The consumer execution agent always executes the continuation.
- 2. Producer Side: The producer execution agent always executes the continuation.
- 3. inline_executor semantics: If the shared state is ready when the continuation is set, the consumer thread executes the continuation. If the shared state is not ready when the continuation is set, the producer thread executes the continuation.
- 4. thread_executor semantics: A new std::thread executes the continuation.

In particular, the first two possibilities have a significant drawback: they block. In the first case, the consumer blocks until the producer is ready. In the second case, the producer blocks, until the consumer is ready.

Here are a few nice use-cases of executor propagation from the document P0701r1¹¹:

<sup>11</sup> http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0701r1.html

**Executor propagation**

```cpp
auto i = std::async(thread_pool, f).then(g).then(h);
// f, g and h are executed on thread_pool.

auto i = std::async(thread_pool, f).then(g, gpu).then(h);
// f is executed on thread_pool, g and h are executed on gpu.

auto i = std::async(inline_executor, f).then(g).then(h);
// h(g(f())) are invoked in the calling execution agent.
```

### 7.2.2.1.3 Passing futures to `.then`: Continuations Are Unwieldy

Because the future is passed to the continuation and not its value, the syntax is quite complicated. First, once more, the correct but verbose version.

**Continuations with `std::future`**

```cpp
std::future<int> f1 = std::async([]() { return 123; });
std::future<std::string> f2 = f1.then([](std::future<int> f) {
    return std::to_string(f.get());
});
```

Now, I assume that I can pass the value because `to_string` is overloaded on `std::future<int>`.

**Continuations with `std::future` Passing the Value**

```cpp
std::future<int> f1 = std::async([]() { return 123; });
std::future<std::string> f2 = f1.then(std::to_string);
```

### 7.2.2.1.4 `when_all` and `when_any` Return Types Are Unwieldy

The chapter on `std::when_all` and `std::when_any` shows their quite complicated usage.

### 7.2.2.1.5 Conditional Blocking in futures Destructor Must Go

Fire and forget futures look very promising but have a big drawback. A future that is created by `std::async` waits on its destructor until its promise is done. What seems to be concurrent runs sequentially. According to document P0701r1, this is not acceptable and error-prone. I describe the peculiar behavior of Fire and Forget Futures in the referenced chapter.

### 7.2.2.1.6 Immediate Values and Future Values Should Be Easily Composable

In C++11, there is no convenient way to create a future. We have to start with a promise.

**Creating a future in the current standard**

```cpp
std::promise<std::string> p;
std::future<std::string> fut = p.get_future();
p.set_value("hello");
```

This may change with the function `std::make_ready_future` in the Concurrency TS v1.

**Creating a future in the Concurrency TS v1**

```cpp
std::future<std::string> fut = make_ready_future("hello");
```

Using future and non-future arguments would make our job even more comfortable.

**Using future and non-future arguments**

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

Neither the syntactic form d1 nor the syntactic form d2 is possible with the Concurrency TS v1.

## 7.2.2 Five New Concepts

There are five new concepts for futures and promises in proposal 1054R0<sup>19</sup>.

- **FutureContinuation**, invocable objects that are called with the value or exception of a future as an argument.
- **SemiFuture**, which can be bound to an executor, an operation that produces a `ContinuableFuture` (`f = sf.via(exec)`).
- **ContinuableFuture**, which refines SemiFuture and instances can have one `FutureContinuation` attached to them (`f.then(c)`), which is executed on the future’s associated executor when the future becomes ready.
- **SharedFuture**, which refines `ContinuableFuture` and instances can have multiple `FutureContinuations` attached to them.
- **Promise**, each associated with a future and makes the future ready with either a value or an exception.

The paper also provides the declaration of these new concepts.

<sup>19</sup> http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1054r0.html

**The five new concepts for futures and promises**

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

## An atomic block

```cpp
atomic {
    statement1;
    statement2;
    statement3;
}
```

### Atomicity

Either all or none of the statements in the block are performed.

### Consistency

The system is always in a consistent state. All transactions establish a total order.

### Isolation

Each transaction runs in total isolation from other transactions.

How do these properties apply? A transaction remembers its initial state and is performed without synchronization. If a conflict happens during its execution, the transaction is interrupted and restored to its initial state. This rollback causes the transaction to be executed again. If the transaction’s initial state still exists at the end of the transaction, the transaction is committed. Conflicts are typically detected with a tagged state reference.

A transaction is a kind of speculative action that is only committed if the initial state holds. In contrast to a mutex, it is an optimistic approach. A transaction is performed without synchronization. It is only published if no conflict occurs. A mutex is a pessimistic approach. First, the mutex ensures that no other thread can enter the critical region. Next, the thread enters the critical region if it is the exclusive owner of the mutex, and hence all other threads are blocked.

C++ supports transactional memory in two flavors: synchronized blocks and atomic blocks.

## 7.3.2 Synchronized and Atomic Blocks

So far I only wrote about transactions. Now I write about synchronized blocks and atomic blocks. Both can be encapsulated in each other. To be more specific synchronized blocks are not transactions because they can execute transaction-unsafe. An example for a transaction-unsafe code would be a code like the output to the console, which can not be undone. For this reason, synchronized blocks are often called relaxed blocks.

### 7.3.2.1 Synchronized Blocks

Synchronized blocks behave like a global lock that protects them. This means that all synchronized blocks follow a total order, and in particular all changes to a synchronized block are available in the next synchronized block. There is a synchronizes-with relation between the synchronized blocks because of the commit of the transaction synchronizes-with the next start of a transaction. Synchronized blocks can not cause a deadlock because they create a total order. While a classical
