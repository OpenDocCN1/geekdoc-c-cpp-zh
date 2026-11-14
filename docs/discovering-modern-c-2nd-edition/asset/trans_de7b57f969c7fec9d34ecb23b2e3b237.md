

max_check 的选择绝非明智之举。如果使用 max_check = sqrt(i) + 1，我们可以节省大量操作，但无论线程数量多少，计算都会立即完成（以人类感知而言）。要开始我们的实现，我们可以先了解硬件支持多少个线程：

单击此处查看代码图像

```
cout << thread::hardware_concurrency() << " threads available.\n";
```

我们的测试机器支持八个硬件线程（四个核心并启用超线程）。为了让机器忙碌几秒钟（但不是永远），我们选取了一个大约 10 亿的已知质数作为第一个测试值，以及随后的奇数：

单击此处查看代码图像

```
vector<long> vi;
long first_prime = 982451653;
for (long i = 0, v = first_prime; i < num_threads; ++i, v += 2)
vi.push_back(v);
```

为了不让 I/O 中断计算，我们为结果创建一个向量：

```
vector<char> results(num_threads);
```

请注意，我们的结果存储在 `vector<char>` 中，而不是 `vector<bool>`。后者在单个字节内共享多个值，我们不希望当两个线程同时修改同一个字节时出现奇怪的影响。鉴于此修改所需时间很短，这种情况发生的可能性极低。反过来，极少发生的错误很难调试，并且还存在这样的风险：在我们测试程序时不会出现，但当其他人（博士导师、付费客户、最喜欢的敌人……）尝试我们的程序时却会出现。

现在我们应该能够使用 `is_prime` 启动线程了。不完全是。`thread` 不允许从函数返回值。我们可以通过编写一个持有引用的函数对象，并在 `void operator()` 中执行 `is_prime` 的调用来绕过这一限制。这样的函数对象可以用 lambda 更简洁地实现：

单击此处查看代码图像

```
vector<thread> threads;
for (int i = 0; i < num_threads; ++i)
threads.push_back(std::thread([&vi, &results, i]()
{ results[i] = is_prime(vi[i]); }
}));
```

与其构造一个线程并将其（好吧，移动）复制到向量中，不如在向量内部直接构造线程：

单击此处查看代码图像

```
for (int i = 0; i < num_threads; ++i)
threads.emplace_back(
[&vi, &results, i]() { results[i] = is_prime(vi[i]); }
);
```

要使用结果，我们必须确保相应的线程已结束。`join` 方法会等待线程结束，并且只有在确认线程已安全终止后才返回：

单击此处查看代码图像

```
for (int i = 0; i < num_threads; ++i) {
threads[i].join();
cout << vi[i] << " is " << (results[i] ? "" : "not ")
<< "a prime number.\n";
}
```

这已经是并行的，我们可以就此收工了。然而，使用 `thread` 存在几个缺点：

- 我们需要一个额外的 lambda 来处理返回值；
- 我们有两个容器：一个用于线程，一个用于结果；
- 我们无法测试任务是否完成（而不阻塞调用者）；以及
- 我们无法处理异常。

在接下来的章节中，我们将展示实现并发计算的更好方法。

## 4.6.4 向调用者回传

对于正在运行的线程，一个更好的句柄是 `future`（位于 `<future>` 中）。它知道关联的线程是否仍在运行，并在终止后保存其结果。它的对应物是 `promise`。线程在此存储其结果或异常。

它们与一个函数对象一起封装在 `packaged_task` 中。这三个类都位于头文件 `<future>` 中。我们将通过实现一个（简化的）`packaged_task` 来演示它们如何协同工作：

单击此处查看代码图像

```
template <typename Ret, typename ...Args>
class ptask
{
    using fun = std::function<Ret(Args...)>;
public:
    explicit ptask(fun fn) : f(fn) {}
    // ...
private:
    fun f;
    mutable std::promise<Ret> p;
};
```

我们的类 `ptask` 使用我们将并行运行的函数的返回类型和参数类型进行参数化。为此，我们使用 `std::function`：一种用于存储多种函数对象的实用工具（更多内容见第 4.4.7 节）。我们的 `promise` 被声明为 `mutable`，以便我们可以在 `const` 方法中更改它。这个方法当然就是调用运算符：

单击此处查看代码图像

```
void operator() (Args&& ...args) const
{
    try {
        p.set_value_at_thread_exit(f(std::forward<Args>
        (args)...));
    } catch(...) {
        p.set_exception_at_thread_exit(std::current_exception());
    }
}
```

该运算符将所有参数转发给包含的函数 `f`。`f` 的结果存储在 `promise p` 中。除非抛出异常；那样的话，异常会存储在 `promise` 中。剩下的就是 `future`。它由我们的 `promise` 提供：

![](img/5682e787fc967e93d7e33e8bac5f58a0_424_0.png)

```
std::future<Ret> get_future() const { return p.get_future(); }
}
```

每个 `future` 都与一个 `promise` 关联。工作线程（被调用者）在 `promise` 中设置一个值或异常，调用者从关联的 `future` 中获取它。

与其保留一个线程和一个结果对象，不如只需要一个 `future` 或其容器：

![](img/5682e787fc967e93d7e33e8bac5f58a0_424_1.png)

```
vector<future<bool>> futures;
for (long i = 0; i < num_threads; ++i) {
    ptask<bool, long> pt_is_prime;
    futures.push_back(pt.get_future());
    thread t(move(pt), vi[i]);
    t.detach();
}
```

首先我们创建一个 `ptask` 并将其保存在容器中。这是我们保留的唯一东西。现在我们可以使用这个 `ptask` 启动一个新线程并分离该线程。这意味着另一个线程现在独立运行，并在退出时释放其资源。我们不再拥有它，线程对象也没用了。相反，我们为每个线程拥有一个 `future` 句柄，可以用它来获取结果：

![](img/5682e787fc967e93d7e33e8bac5f58a0_424_2.png)

```
for (long i = 0; i < num_threads; ++i)
    cout << vi[i] << (futures[i].get() ? " is " : " is not ")
         << "a prime number.\n";
```

此函数会等待任务完成，然后返回结果。

## 4.6.5 异步调用

=> c++11/async_example.cpp

倒数第二个代码片段中我们填充 `future` 向量的循环体，正是 `async` 所做的事情。因此，我们可以简单地使用以下方式启动并分离线程：

![](img/5682e787fc967e93d7e33e8bac5f58a0_424_3.png)

```
vector<future<bool>> vf;
for (long v : vi)
    vf.emplace_back(async(is_prime, v));
```

最后，我们不再处理线程和 `packaged_task`。我们所拥有的只是一个返回 `future` 的函数调用。

实际上，我们的 `async` 调用与前面的实现并不完全相同。在这种情况下——不提供启动策略——系统可能会推迟执行。为了确保在 `async` 调用时立即生成线程，我们必须通过策略来要求这一点：

```
async(launch::async, is_prime, v);
```

使用以下策略应用惰性求值：

```
async(launch::deferred, is_prime, v);
```

然后，只有当线程等待 `future` 来完成关联线程时，函数才会被求值。当我们使用 `get` 请求 `future` 的结果时，我们也会等待线程终止。为了让系统在两种策略之间选择，我们可以使用按位或允许两者：

单击此处查看代码图像

```
async(launch::async | launch::deferred, is_prime, v);
```

当我们省略策略时，这就是我们得到的结果。

最后，我们还想处理异常。如果我们问自己，对于哪些大数我们一眼就能看出它们不是质数，我们会意识到，它们是那些以偶数位或 5 结尾的数（当然，2 和 5 是质数，但它们不大）。从这一观察中我们得出结论，测试以 5 结尾的数是个 `exception-ally`（异常地）愚蠢的主意：

单击此处查看代码图像

```
bool is_prime(long i)
{
    if (i % 10 == 5 && i != 5)
        throw trivial_nonprime{};
    // remainder as before
}
```

我们现在遍历结果的循环应捕获这些异常：

