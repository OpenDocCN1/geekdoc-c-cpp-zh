
我甚至不需要启动一个线程；默认情况下，`this_thread` 可以指代唯一的那个线程。
使用了 `duration_cast` 将时钟单位调整为我想要的纳秒。

通信外部事件的基本支持由 `<condition_variable>` 中的 `condition_variable` 提供的。`condition_variable` 是一种允许一个线程等待另一个线程的机制。具体来说，它允许一个线程等待某个条件（称为事件），该条件是其他线程完成工作的结果。

使用 `condition_variables` 支持许多种优雅且高效的共享形式，但可能会相当复杂。考虑一个线程通过队列传递消息进行通信的经典示例。为了简单起见，我将队列以及避免该队列竞态条件的机制声明为生产者和消费者的全局变量：

点击此处查看代码图片

```
class Message {
    // 要通信的对象
    //...
};

queue<Message> mqueue;
condition_variable mcond;
mutex mtx;
```

`queue`、`condition_variable` 和 `mutex` 类型由标准库提供。
`consumer()` 读取并处理 `Messages`：

点击此处查看代码图片

```
void consumer() {
    while(true) {
        unique_lock lock(mtx);
        mcond.wait(lock, [] { return !mqueue.empty(); }); // 获取 mtx
                                            // 释放 mtx 并等待；
                                            // 唤醒后重新获取 mtx
                                            // 除非 mqueue 不为空否则唤醒

        auto m = mqueue.front();
        mqueue.pop();
        lock.unlock();
        // 获取消息
        // 释放 mtx

        // ... 处理 m
    }
}
```

在这里，我显式地使用 `mutex` 上的 `unique_lock` 来保护对队列和 `condition_variable` 的操作。在 `condition_variable` 上等待会释放其锁，直到等待结束（或队列不为空），并重新获取锁。显式检查条件（此处是 `mqueue.empty()`）是为了防止唤醒时由于其他任务已经“获取”了导致条件不再成立。原因有两个：
- 我们需要将锁传递给 `condition_variable` 的 `wait()`。`scoped_lock` 不能被移动，但 `unique_lock` 可以。
- 我们在处理消息之前想要解锁 `mutex` 以保护条件。`unique_lock` 提供了如 `lock()` 和 `unlock()` 等用于低级同步的操作。

另一方面，`unique_lock` 只能处理单个 `mutex`。

相应的生产者看起来如下：

点击此处查看代码图片

```
void producer() {
  while(true) {
    Message m;
    // ... 填充消息
    scoped_lock lck(mutex);
    mqueue.push(m);
    mcond.notify_one();
  }
}
```

# 18.5 任务通信

标准库提供了一些设施，允许程序员在任务的概念层面（可能并发执行的工作）进行操作，而不是直接在任务层面：
- `future` 和 `promise` 用于从单独线程返回值
- `packaged_task` 用于启动任务并连接返回机制
- `async()` 以类似于调用函数的方式启动任务

这些设施可以在 `<future>` 中找到

# 18.5.1 future 和 promise

`future` 和 `promise` 的重要点在于它们允许在不显式使用锁 的情况下，在两个任务之间传递值；“系统”高效地实现了这种传递。基本思想是：当一个任务想要传递值时，它将值放入 `promise` 中。通过某种方式，该值出现在相应的 `future` 中（通常由任务的启动者读取）：

![](img/0bde25eba2737c5daca16fad65.png)

如果我们有一个 `future<X> fx`，可以从它获取类型为 `X` 的值：

点击此处查看代码图片

```
X = fx.get(); // 如果必要，等待值计算
```

如果值尚未到达，我们的线程将被阻塞直到它到达。如果值无法计算，`get()` 可能会从系统或 `promise` 抛出异常。

`promise` 的主要目的是提供“放入”操作（称为 `set_value()` 和 `set_exception()`），以匹配 `future` 的 `get()`。“future”和“promise”这些名字是历史性的；请不要怪它们。它们是另一个双关语来源。

如果你有一个 `promise` 并需要向 `future` 传递类型为 `X` 的结果，你可以做两件事之一：传递值或异常。例如：

点击此处查看代码图片

```
void f(promise<X>& px) // 任务：将结果放在 px 中
{
  // ...
  try {
    X res;
    // ... 计算值 res
    px.set_value(res);
  } catch (...) {
    // 无法计算 res
    px.set_exception(current_exception()); // 将异常传递给 future 线程
  }
}
```

`current_exception()` 指向捕获到的异常。为了处理通过 `future` 传递的异常，`get()` 的调用者必须准备在某处捕获它。

点击此处查看代码图片

```
void g(future<X>& fx) // 任务：从 fx 获取结果
{
  // ...
  try {
    X v = fx.get(); // 如果必要，等待值计算
    // ... 使用 v
  } catch (...) {
    // 有人无法计算 v
    // ... 处理错误
  }
}
```

如果错误不需要 `g()` 自身处理，代码将简化为：

点击此处查看代码图片

```cpp
void g(future<X>& fx) // 任务：从 fx 获取结果
{
  // ...
  X v = fx.get(); // 如果必要，等待值计算
  // ... 使用 v
}
```

现在，来自 `fx` 函数（`f()`）的异常隐式地传播给 `g()` 的调用者，正就像 `g()` 直接调用 `f()` 一样。

# 18.5.2 packaged_task

我们如何获取需要任务和相应 `promise` 的 `future`？提供 `packaged_task` 类型是为了简化与 `future` 连接的任务。例如，如 §18.5.1 所示的代码，我们可以使用两个任务通过标准库的 `accumulate()` 来累加 `vector<double>` 的每个元素：

点击此处查看代码图片

```
double accumulate(vector<double>::iterator end, vector<double>::double init)
{
    return accumulate("begin", &end, init);
}

double comp2(vector<double>& v)
{
    packaged_task pt0(accum); // 封装任务（即 accum）
    packaged_task pt1(accum);

    future<double> f0 (pt0.get_future()); // 获取 pt0 的 future
    future<double> f1 (pt1.get_future()); // 获取 pt1 的 future

    double* first = &v[0];
    thread t1 (move(pt0), first, first+v.size()/2,0); // 为 pt0 启动线程
    thread t2 (move(pt1), first+v.size()/2,first+v.size(),0); // 为 pt1 启动线程
    // ...

    return f0.get()+f1.get(); // 获取结果
```

`packaged_task` 类型是为了简化与 `future` 连接的任务。
