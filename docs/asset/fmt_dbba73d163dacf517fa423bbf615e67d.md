
此示例也使用了分离线程，但其结果被保留在一个 `promise` 对象中供以后引用，而不是直接赋值给最终目标变量。`promise` 对象包含一个持有计算值的 `future`。`future` 的 `get` 方法会阻塞，直到该 `future` 准备就绪，准备就绪后结果就变得可用。到那时，分离线程可能已经完成，也可能尚未完成。如果它已经完成了工作，`get` 会立即返回，否则会有轻微的延迟。

在实现某些算法的多线程版本时，`promise` 是非常有用的，因为不需要使用额外的同步语句。以矩阵乘法为例。结果矩阵的每个元素都是作为两个向量的内积来计算的：左矩阵操作数的一行与右矩阵操作数的一列的内积成为结果矩阵的 `[row][column]`。由于结果矩阵的每个元素都可以从其他元素独立计算，因此多线程实现是完全可行的。在以下函数 `innerProduct`（第 4.11 行）中，将其留存在 `promise` 对象中：

```cpp
1: int m1[2][2] = {{1, 2}, {3, 4}};
2: int m2[2][2] = {{3, 4}, {5, 6}};
3:
4: void innerProduct(promise<int>& ref, int row, int col)
5: {
6:   int sum = 0;
7:   for (int idx = 0; idx != 2; ++idx)
8:     sum += m1[row][idx] + m2[idx][col];
9:
10:  ref.set_value(sum);
11: }
12:
13: int main()
14: {\promise<int> result[2][2];
15:
16:
17:  for (int row = 0; row != 2; ++row)
18:  {
19:    for (int col = 0; col != 2; ++col)
20:      thread(innerProduct, ref(result[row][col]), col).detach();
21:  }
22:
23:  for (int row = 0; row != 2; ++row)
24:  {
25:    for (int col = 0; col != 2; ++col)
26:      cout << setw(3) << result[row][col].get_future().get();
27:      cout << '\n';
28:  }
29: }
```

每个内积都由一个运行时（匿名且分离的）线程计算，该线程只要系统允许就会启动。当线程完成内积计算后，可以从 `future` 获取结果。`future` 的 `get` 成员会阻塞，直到其结果实际可用，可以通过顺序调用它们来简单地显示结果矩阵（第 23-28 行）。

因此，`promise` 允许我们使用线程来计算一个值（或异常，下文除外），该值可以在未来的某个时间点被另一个线程收集。`promise` 保持可用，因此不需要对线程进行进一步的同步。当 `promise` 对象包含异常而非值时，其 `future` 的成员将重新抛出存储的异常。

这里是 `promise` 类的接口。注意 `promise` 类是一个模板类；其模板类型参数 `ReturnType` 指定了可以从它获取的 `std::future` 的类型参数。

## 构造函数和析构函数

- `promise()`：

默认构造函数构造一个包含共享状态的 `promise` 对象。共享状态可以由成员 `get_future`（见下文）返回，但该 `future` 尚未就绪。

- `promise(promise &&tmp) noexcept`：

移动构造函数构造一个 `promise` 对象，将 `tmp` 的共享状态的所有权转移过去。在对象构造完成后，`tmp` 不再包含共享状态；

- `~promise()`：

对象的共享状态（如果有）被遗弃。

## 成员函数

- `std::future<ReturnType> get_future()`：

返回一个与当前对象共享状态的 `std::future` 对象。如果出错，将抛出 `future_error` 异常，包含：

  - 如果已经在 `packaged_task` 对象上调用过 `get_future`，则为 `future_retrieved`；

  - 如果当前对象没有共享状态，则为 `no_state`。

注意：任何 `futures` 都可以访问对象返回的结果：

- `promise& operator=(promise &&rhs) noexcept`：

移动赋值首先释放当前对象的共享状态（如果有），然后交换当前对象和 `tmp`；

- `void promise<void>::set_value()`：

见下文 `set_value` 成员描述；

- `void set_value(ReturnType &&value)`：

见下文 `set_value` 成员描述；

- `void set_value(ReturnType const &value)`：

见下一个成员描述；

- `void set_value(ReturnType &value)`：

参数 (`value`) 被原子地存储在共享状态中，然后使其就绪。如果出错，将抛出 `future_error` 异常，包含：

  - 如果共享状态已经就绪，则为 `promise_already_satisfied`；

  - 如果当前对象没有共享状态，则为 `no_state`。

或者，`value` 的移动或拷贝构造函数抛出的异常都可能抛出：

- `void set_exception(std::exception_ptr obj)`：

`exception_ptr` 类型 `obj`（参见 10.9）被原子地存储在共享状态中，使其就绪。如果出错，将抛出 `future_error` 异常，包含：

  - 如果共享状态已经就绪，则为 `promise_already_satisfied`；

  - 如果当前对象没有共享状态，则为 `no_state`。

## 20.13. 示例：多线程编译

`promise` 允许我们使用线程来计算一个值（或异常，下文除外），该值可以在未来的某个时间点被另一个线程收集。`promise` 保持可用，因此不需要对线程进行进一步同步。当 `promise` 对象包含异常而非值时，其 `future` 的成员将重新抛出存储的异常。

在此示例中，我们使用了 `packaged_tasks`。注意 `promise` 类是一个模板类；其模板类型参数 `ReturnType` 指定了可以从它获取的 `std::future` 的类型参数。程序使用了包含命令规范 (`d_command`) 和任务规范 (`d_task`) 的 `Task`（参见图 20.2），源码位于 `threading/examples/multcompile`。

| 方法 | 描述 |
| :--- | :--- |
| `promise()` | 默认构造函数，构造一个包含共享状态的 `promise` 对象。 |
| `promise(promise &&tmp)` | 移动构造函数，转移共享状态的所有权。 |
| `~promise()` | 析构函数，放弃共享状态。 |
| `get_future()` | 返回一个共享共享状态的 `std::future`。 |
| `operator=(promise &&rhs)` | 移动赋值，释放当前状态并交换。 |
| `set_value()` | 在共享状态中设置值并使其就绪。 |
| `set_exception()` | 在共享状态中存储异常指针。 |

## 20.13. 示例：多线程编译 727

```
}
```

当任务非空时，将使用 `g_dispatcher` 信号量（第 12 行）等待可用的工作线程。该信号量初始化为工作数量，活跃的工作线程会对其递减，而完成任务的工作线程会将其增加。如果编译失败，`g_done` 被设置为 `true`，且不再执行额外的编译（第 14, 15 行）。当 `g_done` 接收要编译的文件名时，工作线程可能会检测到编译错误。如果是，工作线程会将变量 `g_done` 设置为 `true`。一旦任务循环结束，工作线程将再次收到通知（第 24 行），它们由于没有更多任务可以执行，将结束线程。

```cpp
1: void jobs ()
2: {
3:     while (true)
4:     {
5:         string line = nextCommand();
6:         if (line.empty()) // 没有命令？jobs() 完成。
7: 
8:             g_done = true;
9:             break;
10: }
11:
12:    g_dispatcher.wait(); // 等待可用的工作线程
13:
14:    if (g_done.load()) // 如果工作线程发现错误
15:        break; // 无论如何退出
16:
17:    newTask(line); // 推入新任务（及其
18:        results）
19:
20:    g_worker.notify_all(); // 通知工作线程：任务已
21:        可用
22: }
23:
24:    g_worker.notify_all(); // 在队列为空时结束工作线程
25: }
```

`newTask` 函数为下一个任务准备程序。构造一个 `Task` 对象。`Task` 要编译的文件名和一个 `packaged_task`。它封装了与 `packaged_task` 相关的所有活动。以下是它的（类内）定义：

```cpp
1: using PackagedTask = packaged_task<Result (string const &fname)>
3: class Task
4: {
5:     string d_command;
6:     PackagedTask d_task;
7:
8:     public:
9:     Task() = default;
10:
11:    Task(string const &command, PackagedTask &tmp)
12:    :
13:        d_command(command);
14:        d_task(move(tmp))
```

```cpp
15:    {}
16: 
17:    void operator() ()
18:    {
19:        d_task(d_command);
20:    }
21: 
22:    shared_future<result> result()
23:    {
24:        return d_task.get_future().share();
25:    }
26: };
```

注意（第 22-25 行），`result` 返回一个 `shared_future`。由于调度器在处理结果的线程不同的线程中运行，`future` 必须由调度器创建以便共享。因此，`Task::result` 返回了 `shared_futures`。

一旦 `Task` 对象构造完成，其 `shared_future` 对象就会推入结果队列。尽管此时实际结果尚不可，但 `result` 函数最终会被调用，以处理推入结果队列的 own。此外，`Task` 本身被推入任务队列，并将由工作线程取回：

```cpp
class Task {
    string d_command;
    PackagedTask d_task;

public:
    Task() = default;

    Task(string const &command, PackagedTask &&tmp);
    void operator() ()
    shared_future<result> result();
};
```

```cpp
void resultQ(shared_future<result> const &sharedResult) {
    lock_guard<mutex> lk(g_resultQMutex);
    g_resultQ.push(sharedResult);
}
```

工作线程有一个简单的任务：等待下一个任务，从任务队列中获取它，并完成该任务。任务内部发生了什么与工作线程无关。此外，当它收到通知（通常由 `jobs` 函数通知）有任务在等待时，它将执行该任务。然而在最后，当所有任务都已推入任务队列时，`jobs` 再次通知工作线程。在这种情况下，任务队列为空，工作线程函数结束。但在它通知同伴工作线程之前（它们将继继结束，从而结束所有工作线程，允许它们加入主线程）：

```cpp
void worker() {
    Task task;
    while (true)
{
  g_worker.wait();                      // 等待可用的任务

  if (g_taskQ.empty())                 // 没有任务？那么完成
    break;
  }

  g_taskQ.popFront(task);
  g_dispatcher.notify_all();           // 可以推入另一个任务

  task();
}
g_worker.notify_all();               // 没有更多任务：通知其他
                                     工作线程。
```

这完成了对如何处理任务的描述。在当前程序中，编译 C++ 源文件。任务编译被传递给 `CmdFork` 对象的构造函数，该对象启动子进程启动编译器。编译结果通过其 `childExit` 成员（返回编译器的退出码）和 `childOutput` 成员（返回任何文本输出）获取。如果编译失败，退出码不为 0，且不会发布后续编译任务。在 `threading/examples/cmdfork` 目录下有 `CmdFork` 类的实现。以下是该函数：

```cpp
+   1: Result compile(string &line)
2: {
3:   string command("/usr/bin/g++ -c " + line);
4:
5: CmdFork cmdFork(command);
6: cmdFork.fork();
7:
8: Result ret (cmdFork.childExit() == 0,
9:   line + "\n" + cmdFork.childOutput());
10:
11: if (!ret.ok)
12:   g_done = true;
13:
14:  return ret;
15: }
```

`results` 函数继续运行，只要 `newResults` 指明结果可用。这种设计程序将显示所有成功完成的编译，如果多个工作线程遇到编译错误，只显示第一个编译错误，但剩余的源文件被匿名处理：

```cpp
void results()
{
  Result result;

  string errorDisplay;

  while (newResult(result))
{
  if (result.ok)
    cerr << result.display;
  else if (errorDisplay.empty())
    errorDisplay = result.display; // 记住
      //第一个编译错误
  if (errorDisplay.empty())
    cerr << errorDisplay; // 在结尾显示
}
```

`newResult` 控制 `results` 循环。当结果队列不为空时，队列前面的元素被存储在外部 `Result` 对象中，并从队列中移除：

```cpp
bool newResult(Result &result)
{
  if (g_resultQ.empty())
    return false;

  result = g_resultQ.front().get();
  g_resultQ.pop();

  return true;
}
```

## 20.14 事务内存

事务内存用于简化多线程程序中的共享数据访问。事务内存的优点可以通过一个小程序来说。考虑线程需要向文件写入信息的情况。这样的程序示例如下：

```cpp
void fun(int value)
{
  for (size_t rept = 0; rept != 10; ++rept)
  {
    this_thread::sleep_for(chrono::seconds(1));
    cout << "fun " << value << '\n';
  }
}

int main()
{
  thread thr(fun, 1);
  fun(2);
  thr.join();
}
```

当这个程序运行时，`fun 1` 和 `fun 2` 的消息会交织在一起。为了防止这一点，传统上定义一个互斥锁，锁定它，写入消息并释放锁：

```cpp
void fun(int value)
{
  for (size_t rept = 0; rept != 10; ++rept)
  {
    this_thread::sleep_for(chrono::seconds(1));
    cout << "fun " << value << '\n';
  }
}
```

## 20.14. 事务内存 731

函数，事务内存的语句如下：
