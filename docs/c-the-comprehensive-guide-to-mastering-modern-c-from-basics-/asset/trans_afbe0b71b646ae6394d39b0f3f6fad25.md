
你不希望一个线程在自己运行结束之前停止。例如，可能在线程正在从磁盘读取一个大文件时，点击了“取消”按钮。如果数据不再需要，线程继续读取文件到结束将是不理想的。

解决此方案是 `stop_token`，它已经内置在 `jthread` 中。在 `thread` 中目前还没有，所以你必须自己实现它。

`stop_token` 是一个从 `jthread` 获取的对象，你可以将其用作进入线程的通信通道。线程内部应该定期检查外部线程是否请求了提前终止。

```
// https://godbolt.org/z/6cod7Tae
struct BackgroundTask {
    void operator()(std::stop_token st) const { // 用于通信的 Token
        task1();
        if(st.stop_requested()) return;
        task2();
        if(st.stop_requested()) return;
        task3();
    }
}
int main() {
    BackgroundTask backgroundTask;
    std::jthread myThread{backgroundTask};
    myThread::sleep_for(std::chrono::milliseconds(100)); // 等待100ms
    myThread.request_stop(); // 请求线程停止
}
```

列表 29.2 使用 "stop_token"，外部世界与线程进行通信。

这里并没有输出所有三个任务的结果，而是只输出了第一个任务的结果。

当创建一个 `jthread` 时，该类总是会同时创建一个 `stop_source`。如果该方法具有该类型的参数，则 `stop_token` 会从这个 `stop_source` 作为参数传递给调用的函数。如果没有，则不。可以说，它是你实际线程函数的一个可选参数。

在这种情况下，线程函数通过 `st` 接收了它。在此期间，我们定期通过 `st.stop_requested()` 检查是否有人想让线程终止。如果是这样，我们就停止工作并进行妥善清理。这很重要！在 C++ 中，你无法通过标准手段从外部简单终止线程。这会破坏 RAII 概念，因为例如，析构函数将不再被调用。

从外部，你可以通过 `get_stop_source()` 获取 `stop_source` 对象，然后调用 `request_stop()`。或者像这个示例中一样直接在 `jthread` 上调用 `request_stop()` 的快捷方法。

`jthread` 非常方便，因为它可以灵活处理带有 `stop_token` 参数的线程函数，也可以处理不带参数的。然而，你应该注意，如果没有此类参数，你就无法检查线程是否应该终止。

为了简单起见，我在这一章中大部分省略了 `stop_token`。但在编写运行超过几毫秒的线程时，你应该始终包含它。

# 29.1.3 等待一个不想提前终止的线程

而是等待直到它完成。一旦你启动了一个线程，你需要执行以下操作之一：

- 等待线程完成
  你通过连接（`join`）线程来实现这一点。这在 `jthread` 的析构函数中会自动发生。

- 让线程独立运行
  你需要从新启动的线程中分离（`detach`）。

如果你在启动线程结束前没有做决定并使用了 `thread`，你的整个程序将终止。具体来说，这意味着如果新线程仍在运行但 `thread` 的析构函数被调用，它将调用 `std::terminate()`——并强制结束你的程序。

- 等待
`myThread.join()`

- 分离
`myThread.detach()`

所以，让我们使用 `thread` 代替 `jthread` 并让等待显式化：

```
// https://godbolt.org/z/Tzs93MzfK
std::thread myThread() {
  task1();
  task2();
  task3();
}
myThread.join(); // 等待线程完成
```

再次：如果线程变量的作用域退出且线程仍在运行，而你没有使用 `detach()`，你的程序将会崩溃。

`join()` 等待线程完成。

在这种情况下，`join()` 是唯一正确的解决方案。因为如果 `main` 程序终止，分离的线程也会被终止。所以如果你在这里使用 `detach()`，由于 `main` 在计算完成前不久退出了，你将看不到任何输出。在另一个函数中，你可以使用 `detach()`，因为可能还有更多的计算在进行。

# 29.1.4 启动线程中的异常

你还需要考虑异常：如果在调用线程某处抛出了异常导致你的线程变量离开作用域，启动的线程尚未完成，整个程序将终止。因此，在远层之外处理异常可能会产生严重后果：

```
// https://godbolt.org/z/E49on6zn
#include <iostream>
#include <thread>
#include <vector>
#include <exception>
using std::cout; using std::endl;
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
void task1() { auto r = fib(40); cout << "fib(40)=" << r << endl; }

void main_program() {
  try {
    std::thread t{&task1};
    std::vector<int> data{0,1,2};
    data.at(666); // 触发 out_of_range
    t.join()); // 等待
  } catch(std::runtime_error &ex) {
    /* (...) */ // 在此处处理特定错误
    t.join();
    throw; // 在外部继续错误处理
  }
}

int main() {
    try {
        main_program();
    } catch(...) { // 到此为止是安全的
        std::cout << "An error has occurred\n"; // 你将看不到这个
    }
}
```

在没有线程的情况下，这段代码是可以工作的。`data.at(666)` 会抛出一个异常，但这是被允许的。抛出的 `out_of_range` 异常与 `catch` 中指定的 `runtime_error` 不匹配。因此异常离开了 `main_program` 并在 `catch(...)` 中被捕获。如果没有线程——会出现 "An error ..." 输出。

对于仍在运行的线程并非如此：异常发生时，其块退出，`thread` 的析构函数被调用。这导致了 `terminate()`，即立即终止程序。

如果在 `main` 程序中使用 `catch(...)` 已经捕获了所有可能的情况而不是 `catch(std::runtime_error ex)` 呢？遗憾的是，在处理异常时 `th` 的作用域已经退出。你需要确保 `th` 在 `catch` 内部仍然存在——例如：

```
// https://godbolt.org/z/T4c1GnjY
#include <iostream>
#include <thread>
#include <vector>
#include <exception>
using std::cout; using std::endl;

long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
void task() { auto r = fib(40); cout << "fib(40)=" << r << endl; }

void main_program() {
    std::thread t1(&task);
    try {
        std::vector<int> data(0,1,2);
        data.at(66); // 触发 out_of_range
    } catch(std::runtime_error& ex) { // 不匹配 out of range
        /* (...) */ // 在此处处理
        t1.join();
        throw; // 在外部继续抛出
    }
    t1.join(); // 在 OK 或特定异常后等待
}

int main() {
    try {
        main_program();
    } catch(...) {
        std::cout << "An error has occurred\n";
    }
}
```

`th` 实例的生命周期可能会出错。在示例中，我区分了两种类型的异常：使用 `std::runtime_error` 处理“我在这里需要做一些特定的事情”，以及其他所有……，我不本地预期这些，但知道或假设会在远层被处理——这就是为什么在重要的 `th.join()` 之后使用 `throw;` 重新抛出。

我尽可能晚调用 `join()`，因为该调用会等待直到线程中的计算完成（调用会阻塞）。如果我早早调用它（例如在启动后立即调用），我就无法获得并行执行。

使用 `jthread` 要简单得多！因为等待发生在析构函数本身，在发生异常时情况也是如此：

```
// https://godbolt.org/z/8TdTEGf3d
void mainProgram() {
    std::jthread th(&task1);
    std::vector data(0,1,2);
    data.at(666); // 触发 out_of_range
}
```

`main()` 函数保持不变。尽管来自 `data.at(666)` 的异常，`jthread` 仍会执行到结束，因为 `th` 的析构函数包含 `join()`。所以你首先看到 `fib(40)=102334155`，然后在控制台上出现 `An error has occurred`。

`jthread` 的析构函数做了两件事：

- 它在线程函数的 `stop_token` 上调用了 `request_stop()`。
- 它通过 `join()` 等待线程函数的结束。

这意味着当你的 `jthread` 变量（如 `th`）离开作用域时，它的析构函数会被调用。如果

