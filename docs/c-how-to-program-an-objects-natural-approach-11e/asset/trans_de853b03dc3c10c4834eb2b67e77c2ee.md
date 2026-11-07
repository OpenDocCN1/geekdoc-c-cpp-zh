
- 协程 `sortCoroutine`（第 21–78 行）使用 **concurrencpp** 启动两个任务，每个任务对 vector 的一半进行排序。
- 函数 `main`（第 80–107 行）创建包含一亿个元素的 vector，并调用 `sortCoroutine` 对该 vector 进行排序。

为便于讨论，我们将该程序分成若干部分。程序之后，我们展示一个示例输出。

## #include 指令与函数 `id`

在图 18.3 中，第 3–11 行包含本程序使用的头文件，第 14–18 行定义函数 `id`。**concurrencpp** 库（第 3 行）提供本程序所需的协程支持功能。

```cpp
// fig18_03.cpp
// Implementing a coroutine with co_await and co_return.
#include <concurrencpp/concurrencpp.h>
#include <format>
#include <iostream>
#include <memory> // for shared_ptr
#include <random>
#include <sstream>
#include <string>
#include <thread>
#include <vector>

// get current thread's ID as a string
std::string id() {
    std::ostringstream out;
    out << std::this_thread::get_id();
    return out.str();
}
```

**图 18.3** | 使用 `co_await` 和 `co_return` 实现协程。

## 启动两个任务的 sortCoroutine

第 21–78 行定义 `sortCoroutine`，它接收以下参数

- 一个用于调度任务的 `std::shared_ptr<concurrencpp::thread_pool_executor>`，以及
- 一个待排序的 `vector<int>` 的引用。

```cpp
// coroutine that sorts a vector<int> using two tasks
concurrencpp::result<void> sortCoroutine(
    std::shared_ptr<concurrencpp::thread_pool_executor> executor,
    std::vector<int>& values) {

    std::cout << std::format("Thread {}: sortCoroutine started\n\n", id());

    // lambda that sorts a portion of a vector
    auto sortTask{
      [&](auto begin, auto end) {
        std::cout << std::format(
          "Thread {}: Sorting {} elements\n", id(), end - begin);
        std::sort(begin, end);
        std::cout << std::format("Thread {}: Finished sorting\n", id());
      }
    };

    // stores task results
    std::vector<concurrencpp::result<void>> results;

    size_t middle{values.size() / 2}; // middle element index

    std::cout << std::format(
      "Thread {}: sortCoroutine starting first half sortTask\n", id());

    // use a concurrencpp thread_pool_executor to schedule
    // a sortTask call that sorts the first half of values
    results.push_back(
      executor->submit(
        [&]() {sortTask(values.begin(), values.begin() + middle);}
      )
    );

    std::cout << std::format(
      "Thread {}: sortCoroutine starting second half sortTask\n", id());

    // use a concurrencpp thread_pool_executor to schedule
    // a sortTask call that sorts the second half of values
    results.push_back(
      executor->submit(
        [&]() {sortTask(values.begin() + middle, values.end());}
      )
    );

    // suspend coroutine while waiting for all sortTasks to complete
    std::cout << std::format("\nThread {}: {}\n", id(),
      "sortCoroutine co_awaiting sortTask completion");
    co_await concurrencpp::when_all(
      executor, results.begin(), results.end());

    // merge the two sorted sub-vectors
    std::cout << std::format(
      "\nThread {}: sortCoroutine merging results\n", id());
    std::inplace_merge(
      values.begin(), values.begin() + middle, values.end());

    std::cout << std::format("Thread {}: sortCoroutine done\n", id());
    co_return; // terminate coroutine and resume caller
}
```

**sortCoroutine** 的工作方式如下：

- 第 25 行显示一条消息，其中包含 **sortCoroutine** 正在运行的线程 ID，并表明 **sortCoroutine** 已启动。该线程 ID 证实 **sortCoroutine** 与 main 在同一线程中运行。
- **sortCoroutine** 将启动两个 **concurrencpp** 任务，这些任务执行 lambda **sortTask**（第 28–35 行）。该 lambda 接收表示待排序公共范围起始和结束的随机访问迭代器。第 30–31 行显示一条消息，其中包含对 **sortTask** 的特定调用所在的线程 ID 及其正在排序的元素数量。第 32 行调用 `std::sort` 算法对 vector 的指定部分进行排序。排序完成后，第 33 行显示一条消息，其中包含线程 ID，并表明该任务的排序已完成。
- **sortTask** 不返回值，因此每个 **thread_pool_executor** 的 **submit** 函数将为每个任务返回一个 **concurrencpp::result<void>**。我们将这些结果存储在 vector `results` 中（定义于第 38 行）。
- 第 40 行确定 vector 的中间元素，我们将用它把 vector 分成两半。
- 第 42–43 行显示一条消息，指出正在执行的线程 ID，并表明我们正在启动针对 vector 前半部分的 **sortTask**。然后，第 47–51 行使用 **thread_pool_executor** 的 **submit** 函数创建一个任务，该任务调用 **sortTask** 对范围 values.begin() 到中间 values 元素（但不包括该中间元素）中的元素进行排序。我们将 **submit** 返回的 **result** 对象存储在 `results` vector 中。第 53–62 行重复这些步骤，以启动第二个任务，对从中间元素到 vector 末尾的 vector 元素进行排序。
- 第 65–66 行显示一条消息，其中包含 **sortCoroutine** 正在运行的线程 ID，并表明我们正在 **co_awaiting** **sortTask** 的结果。第 67–68 行使用 **concurrencpp** 的 **when_all** 函数来 **co_await** 所有 sortTask 的结果。我们稍后将更详细地讨论这一行。
- 第 71–72 行显示一条消息，其中包含 **sortCoroutine** 正在运行的线程 ID，并表明我们正在合并结果。然后，第 73–74 行使用标准库算法 `inplace_merge` 合并 vector 的两个已排序半部分。
- 最后，第 76 行显示 **sortCoroutine** 当前正在执行的线程的线程 ID，并表明 **sortCoroutine** 已完成。然后，第 77 行使用 C++20 的 **co_return** 语句终止协程并将控制权返回给 main。由于 **sortCoroutine** 不返回值，**concurrencpp** 向协程的调用者返回一个 **concurrencpp::result<void>**。你将看到 main 使用该对象的 **get** 函数等待协程执行完毕。

## 将 when_all 与 C++20 的 co_await 表达式配合使用

我们可能在 C++23 或更高版本中见到的协程工具函数是 **when_all**，它使程序能够等待一组任务完成。函数 **when_all** 接收以下参数

- 第 100 行调用 `result` 对象的 `get` 方法，阻塞 main 继续执行，直到 `sortCoroutine` 的异步任务执行完毕。
- 一旦发生这种情况，第 102–103 行显示一条消息，表明 main 正在确认 values 已排序。然后，第 104 行以 values 为参数调用 `std::ranges::is_sorted`。如果其参数已排序，该算法返回 `true`；否则，返回 `false`。最后，第 105–106 行显示一条消息，表明该 vector 是否已排序。

## 示例输出

让我们详细讨论示例输出。在输出下方，我们为便于讨论将其分成若干部分。

```text
Thread 17276: main creating vector of random ints
Thread 17276: main starting sortCoroutine
Thread 17276: sortCoroutine started

Thread 17276: sortCoroutine starting first half sortTask
Thread 17276: sortCoroutine starting second half sortTask

Thread 17276: sortCoroutine co_awaiting sortTask completion

Thread 17276: main resumed. Waiting for sortCoroutine to complete.
Thread 17144: Sorting 50000000 elements
Thread 6252: Sorting 50000000 elements
Thread 6252: Finished sorting
Thread 17144: Finished sorting

Thread 6252: sortCoroutine merging results
Thread 6252: sortCoroutine done

Thread 17276: main confirming that vector is sorted
Thread 17276: values is sorted
```

首先，main 显示其线程 ID，并创建随机整数 vector：

```text
Thread 17276: main creating vector of random ints
```

接下来，main 显示其线程 ID 并调用 sortCoroutine：

```text
Thread 17276: main starting sortCoroutine
```

然后，sortCoroutine 显示其线程 ID，并表明它已启动：

```text
Thread 17276: sortCoroutine started
```

注意，sortCoroutine 在 main 的线程中执行，因此显示相同的线程 ID。

接下来，sortCoroutine 启动两个任务来对 vector 进行排序：

```text
Thread 17276: sortCoroutine starting first half sortTask
Thread 17276: sortCoroutine starting second half sortTask
```

此时，sortCoroutine 通过 co_await 等待任务完成：

```text
Thread 17276: sortCoroutine co_awaiting sortTask completion
```

如果 sortTask 尚未完成，sortCoroutine 会暂停执行并将控制权返回给 main。我们特意创建了一个很大的 vector，使排序不会立即完成。这使我们能够展示：当协程暂停执行时，main 会继续执行：

```text
Thread 17276: main resumed. Waiting for sortCoroutine to complete.
```
