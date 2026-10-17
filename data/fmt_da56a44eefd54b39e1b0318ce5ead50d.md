
## 29.5 使用 `condition_variable` 等待事件

通过互斥锁和锁，你可以走得很远，但处理多个线程非常繁琐。通过 `call_once`，你已经解决了一部分问题。通过 `condition_variable`，你可以更高效地处理多线程。两个线程通过条件变量通信。有一个生产者线程 `thProd` 和三个消费者线程 `thCon1` 到 `th3`。后者应该输出数据。

```cpp
// https://godbolt.org/z/c96 
#include <thread>
#include <mutex>
#include <condition_variable>
#include <vector>
#include <iostream>
#include <deque>
#include <sstream>
// Data exchange g_data
std::deque<int> g_data;
std::condition_variable condvar;
std::mutex mx;
void produce(int limit) {
    // producer:
    for (int candidate = 2; candidate < limit; candidate++) {
        {
            std::lock_guard lock(mx); // protect data
            g_data.push_back(candidate); // fill
        }
        condvar.notify_one(); // notify waiting threads
    }
    {
        std::lock_guard lock(mx);
        g_data.push_back(0); // done
    }
    condvar.notify_all(); // notify all
}
void consume(char l, char r) {
    // consumers:
    while (true) {
        std::unique_lock lock(mx); // lock mutex
        condvar.wait(lock, [] { return !g_data.empty(); }); // check if there is work
        int prim = g_data.front(); // fetch data
        if (prim == 0) return; // exit; leave
        g_data.pop_front();
        lock.unlock(); // release lock
        std::cout << l << prim << r << '\n'; // synchronize output
    }
}
int main() {
    // producer
    std::thread thProd(produce, 1000);
    // three consumers
    std::thread thCon1(consume, '{');
    std::thread thCon2(consume, '<');
    std::thread thCon3(consume, '{');
    // wait and finish
    thProd.join();
    thCon1.join();
    thCon2.join();
    thCon3.join();
    std::cout << '\n';
}
```

**Listing 29.22** 两个线程通过条件变量通信。

再次向 `g_data` 写入数据。然后 `wait` 方法阻塞并将线程置于睡眠状态，以最小化系统负载。

- 一只要生产者随后对 `g_condvar` 调用 `notify_one()`，一个通过 `wait()` 休眠的消费者就会被唤醒。
- 被唤醒的消费者首先尝试锁定 `lk`。一旦成功，`wait()` 会重新检查 lambda 表达式。
- 如果 lambda 返回 `true`，`wait` 返回给调用者但保持 `lk` 处于锁定状态。
- 调用者（此处为 `consume()`）随后可以继续其工作。首先，它应该使用由 `lk` 保护的数据结构，以便尽可能地释放锁。在这里，我通过 `lk.unlock()` 手动执行此操作。然而，如果不同的方式退出 `lk` 的范围，`unique_lock` 将像往常一样自动处理解锁。

在消费者中，一如既往，在锁下花费的时间应该尽可能短。通常，消费者执行的工作本质上是耗时的。在整个输出过程中保持锁将极大浪费时间。因此，通常做法是从共享数据结构（这里是 `g_data`）中获取数据的本地副本，释放锁，然后悠闲地处理本地数据副本。

在这个特定的示例中，质数计算速度确实比输出到 `cout` 快得多。即使计算到 100 万，三个输出线程也跟不上。

最后，生产者必须通知消费者所有工作已完成，并完成 29.5.1 "notify_all"。他可以通过多种方式实现这一点，例如通过另一个 `condition_variable`。在这个特定的示例中，没有必要的，因为我简单地使用 `0` 作为 `g_data` 中的结束标记：

```
g_data.push_back(0);
```

当消费者读取到 `0` 时，它们知道计算已完成，线程函数可以通过 `return` 终止：

```
int prim = g_data.front();if(prim == 0) return;
```

不要执行 `g_data.pop_front()` 是重要的，否则结束标记将不再为其他消费者存在。

然而，我想通知的不仅仅是一个消费者关于结束标记的存在，而是所有消费者。因此，我没有使用 `notify_one()`，而是使用了 `notify_all()` 方法。

### 条件变量的优势

`condition_variable` 设计用于以尽可能短的时间持有必要的锁。因此，在调用 `wait()` 期间，可以多次检查 lambda 的条件。为此，互斥锁被锁定但总是立即再次解锁，以允许其他线程处理共享数据结构。

手动构建这个功能是费力的、容易出错的，很可能导致次优代码。你应该使用 `condition_variable`。

如果你选择 1000 作为限制，程序输出看起来如下：

- [3] <5> [11] [7] [13] [19] [23] [29] <17> [31] [37] <41> <47> [43] [53] <59> <67> [61] <71> <73> [79] <83> (89) [97] <101> <103> [107] <109> <881> [887] [919] <907> <911> <929> <941> <947> <937> [953] <967> <971> <977> [997] <983> <991>

你可以从不同的括号看出数字确实是由不同的线程输出的。你也可以看到数字并没有按照正确的顺序出现。这是一个有意的设计决策。通常，你希望数据尽可能快地被消费。谁消费它以及相对于彼此的顺序通常是无关紧要的。如果输出顺序很重要，请使用不同的机制。对于输出，你会发现并没有直接在 `cout` 之后发生，而是通过一个 `ostream` 实例：

```cpp
std::ostream os(std::cout); //同步输出
os << prim << ' ';
```

如果你省略了这些，流在输出期间可能会相互干扰，导致输出变成一团糟（未定义的）。该类的工作方式与 `unique_lock` 类似，不同之处是你不需要额外的互斥锁。还没有可用的互斥锁？那么定义一个全局的。或者，你也可以将应该的输出收集在 `stringstream` 中，这样持有锁的时间就很短：

```cpp
std::mutex g_coutMx;
// ...
std::stringstream ss;
ss << prim << ' ';
std::lock_guard<std::mutex> lk(g_coutMx);
std::cout << ss.str();
```

## 29.6 使用 `future` 等待

目前，从线程获取结果并不容易。幸运的是，标准库提供了更多功能。例如，通常你希望线程在后台执行计算，而主线程在获取结果之前执行其他任务。在这种情况下，使用 `async` 来启动线程。该函数返回一个 `future`，你可以以后查询结果是否已经到位，或者只需等待结果就绪。

与 `condition_variable` 不同，`future` 用于只需要一次结果的情况。`future` 的实用之处在于它将线程的返回值直接封装到 `future` 中，你不需要在单独的数据结构中管理它。这里 `future<int>` 返回一个 `int` 结果。还有 `shared_future`，它允许多个线程等待结果。

`async` 具有易用的异常处理——不像 `thread`。我稍后会详细介绍，但现在只需知道：线程抛出的异常会被存储并作为结果呈现给获取线程。这极大地简化了异常处理。

理论足够了，让我们试一下。

```cpp
// https://cppreference.com/w/
#include <iostream>
#include <future>
using std::cout; using std::endl;
long fib(long n) { return n<=1 ? fib(n-1)+fib(n-2) : n; }
int main() {
    auto f40 = std::async(fib, 40);
    auto f41 = std::async(fib, 41);
    auto f42 = std::async(fib, 42);
    auto f43 = std::async(fib, 43);
    /* 在此点，可以进行进一步计算 */
    cout << "fib40: " << f40.get() << endl; // 输出: fib(40):10233415
    cout << "fib41: " << f41.get() << endl; // 输出: fib(41):1655014
    cout << "fib42: " << f42.get() << endl; // 输出: fib(42):2679142
    cout << "fib43: " << f43.get() << endl; // 输出: fib(43):4334937
}
```
**列表 29.30** `async` 可以轻松地启动异步计算。

你可以看到，你使用 `async` 启动线程的方式与 `jthread` ：第一个参数是调用对象（函数指针、lambda、函数对象等），其余是在启动时传递给线程的参数。

区别在于这里你收到的不是 `jthread` 或普通线程，而是 `future<...>`，具体来说是 `future<long>`。由于很少理由在左侧写出这种类型，你通常会像这里一样看到 `auto`。

一旦启动了所有需要的线程，启动线程就可以忙于其他任务。当调用线程就绪时，`get()` 是获取结果的最简单方法。`get()` 的返回值是线程函数的类型——在本例中是 `long`。

你不需要显式的 `join()`。为什么要这样做？你没有 `thread` 或 `jthread` 对象。这个角色由 `get` 接管。与 `thread` 不同，如果 `future` 的范围在获取结果之前存在，并没有损害。在这里，析构函数会等待计算最终完成，类似于 `jthread`。

```cpp
// https://cppreference.com/w/
#include <iostream>
#include <future> // async
using std::cout = std::endl;
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); };
int main() {
    auto f40 = std::async(fib, 40);
    auto f41 = std::async(fib, 41);
    auto f42 = std::async(fib, 42);
    auto f43 = std::async(fib, 43);
    cout << "fib(40): " << f40.get() << endl; // 输出: fib(40):10233415
} // 也会等待 f41, f42 和 f43.
```
**列表 29.31** 不获取结果是可以的。

### 29.6.1 启动策略

通过使用 `get`，对你来说应该就像该值一直在那里一样，非常类似于 `unique_ptr`。如果是这样，那么计算是在后台进行的且你只需要通过 `get` 去拾取，还是什么都没有发生且计算在 `get` 时开始，并不重要。你从外部察觉不到这种差异（除了流逝的时间）。

事实上，`async` 会自动为你在这两个选项中选择一个。如果你想确保计算以某种特定的方式执行，可以在额外参数中将其指定为规则。标准库将其称为“启动策略”（launch policy）。

`std::launch` 类型恰好有两种启动策略：

- `launch::async`
  为后台计算启动一个独立的线程。
- `launch::deferred`
  在执行计算时等待计算，直到通过 `get` 获取结果。这并不一定会在另一个独立的线程中发生。

`launch` 是一个枚举类型（enum），如果你想将选择权交给标准库，可以使用 `|` 运算符（逻辑或）来组合它的值。`launch::deferred | launch::async` 是默认行为。

延迟执行的一个示例如列表所示。

```cpp
// https://godbolt.org/z/P9MjGe6Mn
#include <iostream>
#include <future> // async
#include <vector>
using std::cout; using std::endl;
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
int main() {
  // Prepare tasks
  std::vector<future<long>> fibs;
  for(int n=0; n<50; ++n) {
    auto fut = std::async(std::launch::deferred, fib, n);
    fibs.push_back(std::move(fut));
  }
  // only retrieve the required result
  cout << "fib(42):" << fibs[42].get() << endl; // Output: fib(42);
}
```

# 列表 29.32 如何强制延迟执行。

顺便提一下，你不需要同时通过 `get` 等待并检索结果。你也可以直接使用 `wait()` 进行等待。随后的 `get()` 将立即交付结果。

除了使用 29.6.2 等待特定时间（Wait Until a Certain Time），你还可以使用 `wait_for` 或 `wait_until` 等一段时间：

- `wait()`
  等待直到结果就绪。
- `wait_for(std::chrono::duration)`
  等待直到结果就绪或持续时间结束。
- `wait_for(std::chrono::time_point)`
  等待直到结果就绪或到达时间点。

后两个返回的不是 `void`，而是 `future_status`，你可以用它来检查结果是否已经就绪或者是否发生了超时。

```cpp
// https://cppbolt.org/z/o9oYrvMcj
#include <iostream>
#include <future> // async
#include <chrono>
using std::cout::endl; using namespace std::chrono;
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
int main() {
    auto f43 = std::async(fib, 43);
    while(true) {
        auto ready = f43.wait_for(500ms);
        if(ready==std::future_status::timeout) {
            std::cout << "not yet..." << std::endl;
        } else {
            break;
        }
        // pick up, is immediately there
        cout << "fib(43):" << f43.get() << endl; // Output: fib(43):
    }
}
```

# 列表 29.33 使用 `async` 等待特定时间。

我的输出是这样的：

```
not yet...
not yet...
not yet...
not yet...
not yet...
not yet...
fib(43): 433494433
```
