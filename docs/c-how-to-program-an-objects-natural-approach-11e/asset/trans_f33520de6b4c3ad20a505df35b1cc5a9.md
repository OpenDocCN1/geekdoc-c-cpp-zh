
- 如果读者到达时某个写者正在写入，那么读者必须**等待**锁变为可用。此外，随后到达的任何其他写者都必须**等待**，直到当前正在等待的读者完成读取。如果允许源源不断的写者到达后写入，那么正在等待的读者将被**无限期推迟**。

再次，我们可以使用条件变量来管理这些情况——一个用于读者，另一个单独用于写者。

读者使用 **shared_locks**，但类 **condition_variable** 需要 **unique_locks**。因此，对于读者，请使用 `std::condition_variable_any` 对象来管理等待中的读者。**condition_variable_any** 的工作方式类似于 **condition_variable**，但支持其他锁类型。当写者完成写入时，它会通过调用 **condition_variable_any** 对象的 **notify_all** 函数来**通知所有**当前等待的读者：可以读取了。所有等待该 **condition_variable** 的读者线程随后将转换为就绪状态，并能够重新获取锁。

写者线程仍然可以使用 **unique_lock** 来独占访问共享的可变数据，因此我们可以用 **condition_variable** 来管理写入。当所有活动读者完成读取时，程序会调用 **condition_variable** 对象的 **notify_all** 函数。所有等待中的写者线程将进入就绪状态，并能够重新获取锁。但是，只有一个写者会重新获取锁并继续执行。

## 17.9 协作取消 jthreads

当多线程应用程序需要终止时，良好的做法是关闭仍在执行任务的线程，以便它们释放正在使用的资源。例如，它们可能需要关闭文件、数据库连接和网络连接。在 C++20 之前，没有标准机制让线程相互协作以优雅地终止。这是 **thread** 的另一个缺陷。

C++20 增加了协作取消来解决这个问题，使程序能够在线程该终止时通知它们。在线程中执行的任务可以监视此类通知，然后完成关键工作、释放资源并终止。

图 17.11 演示了使用 `<stop_token>` 头文件中的功能在线程之间进行协作取消。正如你将看到的，**jthread** 集成了这些功能。

```cpp
// Fig. 17.11: CooperativeCancelation.cpp
// Using a std::jthread's built-in stop_source
// to request that the std::jthread stop executing.
#include <chrono>
#include <format>
#include <iostream>
#include <mutex>
#include <random>
```

**图 17.11** | 使用 `std::jthread` 内置的 `stop_source` 请求 `std::jthread` 停止执行。（第 1 部分，共 3 部分。）

- 65. “`std::condition_variable`。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/thread/condition_variable_any
- 66. Anthony Williams，“C++20 及以后的并发”，2019 年 10 月 16 日。访问于 2023 年 4 月 18 日。https://www.youtube.com/watch?v=jozhw_B3D4U

```cpp
#include <sstream>
#include <stop_token>
#include <string>
#include <string_view>
#include <thread>

// get current thread's ID as a string
std::string id() {
    std::ostringstream out;
    out << std::this_thread::get_id();
    return out.str();
}

int main() {
    // each printTask iterates until a stop is requested by another thread
    auto printTask =
        [&](std::stop_token token, std::string name) {
            // set up random-number generation
            std::random_device rd;
            std::default_random_engine engine{rd()};
            std::uniform_int_distribution<> ints{500, 1000};

            // register a function to call when a stop is requested
            std::stop_callback callback{token, [&]() {
                std::cout << std::format(
                    "  {} told to stop by thread with id {}\n", name, id());
            }};

            while (!token.stop_requested()) { // run until stop requested
                auto sleepTime{std::chrono::milliseconds{ints(engine)}};

                std::cout << std::format(
                    "  {} (id: {}) going to sleep for {} ms\n",
                    name, id(), sleepTime.count());

                // put thread to sleep for sleepTime milliseconds
                std::this_thread::sleep_for(sleepTime);

                // show that task woke up
                std::cout << std::format("{} working.\n", name);
            }

            std::cout << std::format("{} terminating.\n", name);
        };

    std::cout << std::format("MAIN (id: {}) STARTING TASKS\n", id());

    // create two jthreads that each call printTask with a string argument
    std::jthread task1{printTask, "Task 1"};
    std::jthread task2{printTask, "Task 2"};
```

**图 17.11** | 使用 `std::jthread` 内置的 `stop_source` 请求 `std::jthread` 停止执行。（第 2 部分，共 3 部分。）

```cpp
// put main thread to sleep for 2 seconds
std::cout << "\nMAIN GOING TO SLEEP FOR 2 SECONDS\n\n";
std::this_thread::sleep_for(std::chrono::seconds{2});

std::cout << std::format("\nMAIN (id: {}) ENDS\n\n", id());
}
```

```
MAIN (id: 16352) STARTING TASKS

MAIN GOING TO SLEEP FOR 2 SECONDS

Task 1 (id: 14048) going to sleep for 708 ms
Task 2 (id: 10504) going to sleep for 995 ms
Task 1 working.
Task 1 (id: 14048) going to sleep for 940 ms
Task 2 working.
Task 2 (id: 10504) going to sleep for 926 ms
Task 1 working.
Task 1 (id: 14048) going to sleep for 875 ms
Task 2 working.
Task 2 (id: 10504) going to sleep for 519 ms

MAIN (id: 16352) ENDS

Task 2 told to stop by thread with id 16352
Task 2 working.
Task 2 terminating.
Task 1 told to stop by thread with id 16352
Task 1 working.
Task 1 terminating.
```

**图 17.11** | 使用 `std::jthread` 内置的 `stop_source` 请求 `std::jthread` 停止执行。（第 3 部分，共 3 部分。）

每个 `jthread` 在内部维护一个 `std::stop_source`，它有一个关联的 `std::stop_token`。`jthread` 的任务函数可以选择将此令牌作为其第一个参数接收。然后，任务函数可以定期调用该令牌的 `stop_requested` 成员函数，以确定任务是否应停止执行。当

- 另一个线程调用 `jthread` 的 `request_stop` 成员函数，或
- `jthread` 的析构函数在 `jthread` 离开作用域时调用 `request_stop`，

`stop_source` 会通知其关联的 `stop_token` 已请求停止。随后对 `stop_token` 的 `stop_requested` 成员函数的调用将返回 `true`。任务随后可以优雅地终止其执行。如果任务函数从不调用 `stop_requested`，则相应的 `jthread` 会继续执行——因此，这被称为协作取消。

在这个示例中，我们将让 `jthread` 的析构函数调用 `request_stop` 成员函数，使程序能够在 main 完成后不久终止。我们创建两个 `jthreads`（第 58–59 行），它们调用 `printTask` lambda（第 24–53 行）。每个 `jthread` 将其 `stop_token` 传递给该 lambda。lambda 中的第 37–49 行循环连续执行以下操作：

- 打印任务名称、线程 ID 和睡眠时间，
- 睡眠，然后
- 打印任务名称，并说明该 lambda 正在执行工作。

循环会一直执行，直到相应的 **jthread** 内部 **stop_source** 收到对其 **request_stop** 成员函数的调用。在这个程序中，该调用发生在 **jthreads** 在 main 结束时离开作用域时，由 **jthread** 的析构函数执行。

### 可选的 stop_callback

第 32–35 行还演示了可以注册一个可选函数，以便在请求**停止**时调用。`std::stop_callback<sup>67</sup>` 构造函数接收一个 **stop_token** 和一个无参数函数——在本例中是一个 lambda。该构造函数将该函数注册到给定的 **stop_token**。当 **stop_token** 收到已请求停止的通知时，它会在请求停止的线程（本例中为主线程）上调用由 **stop_callback** 注册的函数。可以为给定的 **stop_token** 创建任意数量的 **stop_callbacks**。它们函数的执行顺序未指定。我们的 lambda 只是显示一个字符串，以表明回调确实被调用，但这可用于在线程终止前执行清理操作。<sup>68</sup>

### 分析输出

在整个示例输出中，Task 1 和 Task 2 会睡眠并工作。一旦 main 结束，执行这些任务的 **jthreads** 离开作用域，它们的析构函数会调用每个 **jthread** 的 **request_stop** 成员函数，以通知任务应终止。在输出中 "MAIN (id: 16352) ENDS" 之后，你可以看到每个 **jthread** 何时收到其 **request_stop** 调用——我们的 **stop_callback** 会显示任务名称，随后是一条消息，其中包含告知任务停止的线程 ID（本例中为主线程）。<sup>69</sup> 在每种情况下，相应的任务随后完成其工作并终止。

## 17.10 使用 std::async 启动任务

图 17.12 演示了 **std::async**——一种在单独线程中启动任务的更高级方式。在这个示例中，我们将实现一个可能长时间运行的任务——判断一个大整数是否为素数，如果不是，则确定其质因数。

### 安全性、加密与超大整数的质因数分解

安全性是一个关键应用。质因数分解<sup>70,71,72</sup> 是 RSA 公钥密码算法的一个重要方面，该算法通常用于保护传输的数据

- 67. “std::stop_callback。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/thread/stop_callback.
- 68. Williams，“C++20 及以后的并发”。
- 69. 如果在构造 stop_callback 之前请求停止，则显示的线程 ID 将是构造 stop_callback 的线程的 ID（依据 https://en.cppreference.com/w/cpp/thread/stop_callback）。
- 70. “质因数分解”，2020 年 7 月 2 日。访问于 2023 年 4 月 18 日。https://www.cuemath.com/numbers/prime-factorization/.
- 71. Striver，“大数的质因数”，2021 年 5 月 28 日。https://www.geeksforgeeks.org/prime-factors-big-number/.
- 72. Etrud Shalit，“素数——为何如此令人兴奋？”，2018 年 9 月 7 日。访问于 2023 年 4 月 18 日。https://kids.frontiersin.org/articles/10.3389/frym.2018.00040.
