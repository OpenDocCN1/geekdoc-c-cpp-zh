
事实上，`async` 会自动为你在这两个选项中选择一个。如果你想确保计算以某种特定的方式执行，可以在额外参数中将其指定为规则。标准库将其称为“启动策略”（launch policy）。

`std::launch` 类型恰好有两种启动策略：

-  launch::async
  为后台计算启动一个独立的线程。

-  launch::deferred
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

-  wait()
  等待直到结果就绪。

-  wait_for(std::chrono::duration)
  等待直到结果就绪或持续时间结束。

-  wait_for(std::chrono::time_point)
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

# 列表 29.33 使用 "async" 等待特定时间。

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

所以它检查了六次，结果还没出来。在第七次时，结果出现了。随后的 `get()` 立即交付了结果。

## 无限等待或等待特定时间

如果你在标准库的线程区域使用如 `wait()` 等函数阻塞，并且可以无限等待函数返回，那么总会有函数允许你限制等待时间。在 `future::wait()` 的情况下，这些是 `wait_for` 和 `wait_until`。在互斥锁（mutexes）中，有一个 `timed_mutex` 类，拥有 `try_lock_for` 和 `try_lock_until` 方法。使用 `unique_lock` 时，你将持续时间（duration）或时间点（time_point）作为额外的构造函数参数传递。

在互斥锁和锁中使用持续时间的示例可见列表 29.34。在那里，来自 `timed_mutex` 的 `try_lock_for` 接收一个持续时间作为参数。

```cpp
// https://gdbbolt.org/z/xz8hj9oP
#include <chrono>
#include <future>
#include <mutex>
#include <vector>
#include <iostream>

std::mutex mtx;
long fibX(long n) { return n < 2 ? 1L : fibX(n-1) + fibX(n-2); }
long fibCall(long n) {
    using namespace std::chrono; // Suffixes
    if(mtx.try_lock_for(1000ms)) {
        auto res = fibX(n);
        mtx.unlock();
        return res;
    } else {
        return 0L;
    }
}

int main() {
    std::vector<std::future<long>> fs;
    for(long n=1; n<42; ++n) {
        fs.emplace_back(std::async(std::launch::async, fibCall, n));
    }
    for(auto &f : fs) {
        std::cout << f.get() << " ";
    }
    std::cout << std::endl;
}
```

# 列表 29.34 使用 “timed_mutex” 等待锁

`fibX` 函数被用来模拟“耗费长时间”，且参数 `n` 越大，耗时越长。假设 `fibX` 不具备多线程能力：不允许两个线程同时进入它。

`fibCall` 安全地调用 `fibX` 也可以并行调用。通过 `try_lock_for(1000ms)`，`fibX` 的调用受到保护不受两个线程同时进入。然而，它最多等待一秒。如果时间更长，`fibCall` 将返回 0 而不是结果。

输出看起来类似于：
```

