
我使用 **notify_one()** 而不是 **notify_all()**，因为我只添加了一个元素，并希望让 put() 保持简单。考虑到可能存在多个消费者以及消费者落后于生产者的可能性，我或许需要重新考虑。

**get()** 要稍微复杂一些，因为只有在**互斥量**阻止访问或队列为空时，它才应该阻塞其**线程**：

```
template<typename T>
void Sync_queue::get(T& val)
{
unique_lock<mutex> lck(mtx);
cond.wait(lck,[this]{ return !q.empty(); });
val=q.front();
q.pop_front();
}
```

**get()** 的调用者将一直阻塞，直到 **Sync_queue** 非空。
我使用了 **unique_lock** 而不是普通的 **lock_guard**，因为 **lock_guard** 为简单性而优化，不提供解锁和重新锁定**互斥量**所需的操作。
我使用 **[this]** 使 lambda 能够访问 **Sync_queue** 对象（§11.4.3.3）。
我通过引用参数从 **get()** 返回值，而不是作为返回值，以确保具有可能抛异常的复制构造函数的元素类型不会引起麻烦。
这是常规技术（例如，STL **stack** 适配器提供 **pop()**，容器提供 **front()**）。编写一个直接返回值的通用 **get()** 是可能的，但出奇地棘手。例如，参见 **future<T>::get()**（§42.4.4）。
一个简单的生产者-消费者对可以非常简单：

```
Sync_queue<Message> mq;

void producer()
{
while (true) {
Message m; // ... fill m ... mq.put(m);
}
}
void consumer()
{
while (true) {
Message m; mq.get(m); // ... use m ...
}
}
thread t1 {producer};
thread t2 {consumer};
```

使用 **condition_variable** 可以省去消费者显式处理工作耗尽情况的麻烦。如果我们仅仅使用**互斥量**来控制对 **Sync_queue** 的访问，消费者将不得不反复醒来，在队列中查找工作，并在发现队列为空时决定该怎么做。

我将值复制进出用于保存队列元素的列表。元素类型的复制可能抛出异常，但若如此，Sync_queue 将保持不变，put() 或 get() 只会失败。

Sync_queue 本身并不是共享数据结构，因此我们不为它使用单独的互斥量；只有 put() 和 get()（更新队列头和尾，二者可能是同一个元素）需要防止数据竞争。

对于某些应用程序，简单的 Sync_queue 有一个致命缺陷：如果生产者停止添加值，消费者永远等待怎么办？如果消费者还有其他事情要做，不能长时间等待怎么办？通常有解决办法，但一种常见技术是给 get() 添加超时，即指定最大等待时间：

```
void consumer()
{
while (true) {
Message m;
mq.get(m,milliseconds{200});
// ... use m ...
}
}
```

为使此工作，我们需要向 Sync_queue 添加第二个 get()：

```
template<typename T>
void Sync_queue::get(T& val, steady_clock::duration d) {
unique_lock<mutex> lck(mtx);
bool not_empty = cond.wait_for(lck,d,[this]{ return !q.empty(); }); if (not_empty) {
val=q.front();
q.pop_front();
}
else
throw system_error{"Sync_queue: get() timeout"};
}
```

使用超时时，我们需要考虑等待后该做什么：我们拿到了数据还是仅仅超时了？实际上，我们并不真正关心超时，只关心谓词（在 lambda 中表达）是否为真，这就是 wait_for() 返回的内容。我选择通过抛出异常来报告带超时的 get() 失败。如果我认为超时是一种常见且“非异常”的事件，我就会返回一个 bool。

对 put() 大致等效的修改是等待消费者在长队列上取得进展，但不会等待太长时间：

```
template<typename T>
void Sync_queue::put(T val, steady_clock::duration d, int n)
{
```

```
unique_lock<mutex> lck(mtx);
bool not_full = cond.wait_for(lck,d,[this]{ return q.size()<n; });
if (not_full) {
q.push_back(val);
cond.notify_one();
}
else {
cond.notify_all();
throw system_error{"Sync_queue: put() timeout"};
}
```

对于 put()，返回 bool 以鼓励生产者始终显式处理两种情况的做法似乎比 get() 更有吸引力。然而，为避免讨论如何最好地处理溢出，我再次选择通过抛出异常来指示失败。

我选择在队列满时调用 notify_all()。也许某个消费者需要一点推动才能继续。notify_all() 和 notify_one() 之间的选择取决于应用程序的行为，并不总是显而易见的。只通知一个线程会串行化对队列的访问，因此在有多个潜在消费者时可能会使吞吐量最小化。另一方面，通知所有等待线程可能会唤醒多个线程，造成互斥量上的竞争，并可能导致线程反复醒来却发现队列为空（已被其他线程清空）。我回归旧法则：不要相信直觉，要测量。

## 42.3.4.1 condition_variable_any

condition_variable 针对 unique_lock<mutex> 进行了优化。condition_variable_any 在功能上等价于 condition_variable，但可以为它的操作使用任何可锁定对象：

condition_variable_any（§iso.30.5.2）
lck 可以是任何具有所需操作的可锁定对象
... 与 condition_variable 类似 ...

## 42.4 基于任务的并发

到目前为止，本章的重点是运行并发任务的机制：重点是线程、避免竞争条件和线程同步。对于许多并发任务，我发现这种对机制的关注偏离了指定并发任务这一真正任务（原文如此！）。本节重点是指定一种简单的任务：给定参数做一件事并产生一个结果的任务。
为支持这种基于任务的并发模型，标准库提供了：

```
packaged_task<F> promise<T>
future<T>
shared_future<T> x=async(policy,f,args) x=async(f,args)
```

任务支持（§iso.30.6.1）

将类型为 **F** 的可调用对象封装为一个任务来运行。一种可将一个 **T** 类型结果放入其中的对象类型。一种可从中移动出一个 **T** 类型结果的对象类型。一个 **future**，可以从中多次读取 **T** 类型的结果。根据 **policy** 启动 **f(args)**。使用默认策略启动：

```
`x=async(launch::async|launch::deferred,f,args)`
```

这些设施的呈现方式暴露了许多通常无需打扰应用程序编写者的细节。请牢记任务模型本质上的简单性。大多数更复杂的细节是为了支持罕见用途，例如隐藏对更加混乱的线程和锁层次的使用。

标准库的任务支持只是支持基于任务的并发的一个例子。通常，我们希望提供大量小任务，让“系统”操心如何将它们的执行映射到硬件资源，以及如何让它们远离数据竞争、虚假唤醒、过度等待等问题。

这些设施的重要性在于它们对程序员而言的简单性。在顺序程序中，我们通常这样写：

```
`res = task(args); // prefer matask given arguments and get the result`
```

并发版本变为：

```
```cpp
auto handle = async(task,args); // ... do something else ...
res = handle.get()

// prefer matask given arguments

// get the result
```
```

有时候，当我们考虑替代方案、细节、性能和权衡时，我们会忽视简单性的价值。默认情况下，使用最简单的技术，并将更复杂的解决方案留给你知道确实值得的地方。

### 42.4.1 **future 与 promise**

如§5.3.5所述，任务之间的通信由一对 **future/promise** 处理。一个任务将结果放入 **promise**，需要结果的任务从相应的 **future** 中检索结果：

![](img/a47cb5c880e9c78ea4f904f538cf91c8_1217_0.png)

图中的“值”在技术上被称为*共享状态*（§iso.30.6.4）。除了返回值或异常外，它还包含两个**线程**安全交换信息所需的信息。共享状态至少必须能够保存：

+   - 适当类型的*值*或异常。对于“返回 void”的 **future**，该值为空。
+   - 一个*就绪位*，用于指示值或异常是否已准备好供 **future** 提取。
+   - 当 `get()` 被调用时，对于由 **async()** 以启动策略 **deferred**（§42.4.6）启动的任务，要执行的任务。

