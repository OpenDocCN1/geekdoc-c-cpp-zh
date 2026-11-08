

![](img/c60a87adb7f61e2e82071d081bbb389a_503_0.png)

原始上传者为英文维基百科上的 AmosWolfe。 - 从 en.wikipedia 转移至 Commons。，CC BY 2.0.^33

C++20 支持 `std::binary_semaphore`，它是 `std::counting_semaphore<1>` 的别名。在这种情况下，最小的最大值是 1。`std::binary_semaphore` 可用于实现锁^34。

```cpp
using binary_semaphore = std::counting_semaphore<1>;
```

与 `std::mutex` 不同，`std::counting_semaphore` 不与线程绑定。这意味着信号量的获取和释放调用可以发生在不同线程上。下表展示了 `std::counting_semaphore` 的接口。

**`std::counting_semaphore sem` 的成员函数**

| 成员函数 | 描述 |
|---|---|
| `std::counting_semaphore sem(num)` | 创建一个计数器为 num 的信号量。cnt 必须是有符号整数。 |
| `sem.max() (static)` | 返回计数器的最大值。 |
| `sem.release(upd = 1)` | 将计数器增加 upd，随后解除正在获取信号量 sem 的线程的阻塞。 |
| `sem.acquire()` | 将计数器减 1，或阻塞直到计数器大于 0。 |
| `sem.try_acquire()` | 如果计数器大于 0，则尝试将计数器减 1。 |
| `sem.try_acquire_for(relTime)` | 如果计数器为 0，则尝试将计数器减 1，或最多阻塞 relTime。 |
| `sem.try_acquire_until(absTime)` | 如果计数器为 0，则尝试将计数器减 1，或最多阻塞到 absTime。 |

^33 https://commons.wikimedia.org/w/index.php?curid=1972304

^34 https://en.cppreference.com/w/cpp/named_req/BasicLockable

构造函数调用 `std::counting_semaphore<10> sem(5)` 创建一个信号量 `sem`，其最大值至少为 10，计数器为 5。调用 `sem.max()` 返回内部计数器的最大可能值。对于 `sem.release(upd = 1)` 中的 upd，必须满足以下关系：upd >= 0 且 upd + counter <= sem.max()。`sem.try_acquire_for(relTime)` 需要时间长度；成员函数 `sem.try_acquire_until(absTime)` 需要时间点。`sem.try_acquire`、`sem.try_acquire_for` 和 `sem.try_acquire_until` 这三个调用返回一个布尔值，表示调用是否成功。

信号量通常用于发送方-接收方工作流。例如，将信号量 `sem` 初始化为 0 会阻塞接收方的 `sem.acquire()` 调用，直到发送方调用 `sem.release()`。因此，接收方等待发送方的通知。使用信号量可以轻松实现线程的一次性同步。

**使用 `std::counting_semaphore` 进行线程同步**

```cpp
// threadSynchronizationSemaphore.cpp

#include <iostream>
#include <semaphore>
#include <thread>
#include <vector>

std::vector<int> myVec{};

std::counting_semaphore<1> prepareSignal(0);

void prepareWork() {

    myVec.insert(myVec.end(), {0, 1, 0, 3});
    std::cout << "Sender: Data prepared." << '\n';
    prepareSignal.release();
}

void completeWork() {
    std::cout << "Waiter: Waiting for data." << '\n';
    prepareSignal.acquire();
    myVec[2] = 2;
    std::cout << "Waiter: complete the work." << '\n';
    for (auto i: myVec) std::cout << i << " ";
    std::cout << '\n';

}

int main() {

    std::cout << '\n';

    std::thread t1(prepareWork);
    std::thread t2(completeWork);

    t1.join();
    t2.join();

    std::cout << '\n';

}
```

`std::counting_semaphore` `prepareSignal`（第 10 行）可以取值为 0 和 1。在这个具体示例中，它被初始化为 0（第 10 行）。这意味着，调用 `prepareSignal.release()` 会将值设为 1（第 16 行），并解除 `prepareSignal.acquire()` 调用（第 22 行）的阻塞。

![](img/c60a87adb7f61e2e82071d081bbb389a_506_0.png)

使用信号量进行线程同步

![](img/c60a87adb7f61e2e82071d081bbb389a_506_1.png)

### 提炼信息

- 信号量是一种同步机制，用于控制对共享资源的并发访问。
- C++20 中的计数信号量有一个计数器。获取信号量会减少计数器，释放信号量会增加计数器。如果某个线程在计数器为零时尝试获取信号量，该线程会阻塞，直到另一个线程通过释放信号量来增加计数器。

## 6.4 闩锁与屏障

![](img/c60a87adb7f61e2e82071d081bbb389a_507_0.png)

Cippi 在屏障处等待

闩锁和屏障是协调类型，可使一些线程阻塞，直到计数器变为零。在 C++20 中，我们有两种变体的闩锁和屏障：`std::latch` 和 `std::barrier`。并发调用 `std::latch` 或 `std::barrier` 的成员函数不会产生数据竞争。

首先，有两个问题：

1. 这两种协调线程的机制之间有什么区别？`std::latch` 只能使用一次，但 `std::barrier` 可以使用多次。`std::latch` 有助于由多个线程管理一个任务。`std::barrier` 有助于由多个线程管理重复任务。此外，`std::barrier` 使您能够在所谓的完成步骤中执行一个函数。完成步骤是计数器变为零时的状态。
2. 闩锁和屏障支持哪些在 C++11 和 C++14 中无法通过 future、线程或条件变量结合锁完成的用例？闩锁和屏障并未解决新的用例，但它们更易于使用。它们还更高效，因为它们在内部通常使用无锁机制。

### 6.4.1 `std::latch`

现在，让我们更仔细地看看 `std::latch` 的接口。

**`std::latch` 的成员函数**

| 成员函数 | 描述 |
|---|---|
| `std::latch latch(cnt)` | 创建一个计数器为 `cnt` 的 `std::latch`。`cnt` 必须是有符号整数。 |
| `lat.count_down(upd = 1)` | 以原子方式将计数器减少 `upd`，而不阻塞调用者。 |
| `lat.try_wait()` | 如果 counter == 0，则返回 true。 |
| `lat.wait()` | 如果 counter == 0，则立即返回。否则阻塞，直到 counter == 0。 |
| `lat.arrive_and_wait(upd = 1)` | 等价于 `count_down(upd); wait();`。 |
| `std::latch::max` | 返回实现所支持的计数器的最大值 |

upd 的默认值为 1。如果 upd 大于计数器或为负数，则行为未定义。顾名思义，调用 `lat.try_wait()` 实际上从不等待。

以下程序 `bossWorkers.cpp` 使用两个 `std::latch` 构建一个老板-工作者工作流。我使用函数 `synchronizedOut`（第 13 行）将输出同步到 `std::cout`。这种同步使工作流更易于跟踪。

**使用两个 `std::latch` 的老板-工作者工作流**

```cpp
// bossWorkers.cpp

#include <iostream>
#include <mutex>
#include <latch>
#include <thread>

std::latch workDone(6);
std::latch goHome(1);

std::mutex coutMutex;

void synchronizedOut(const std::string& s) {
    std::lock_guard<std::mutex> lo(coutMutex);
    std::cout << s;
}

class Worker {
public:
    Worker(std::string n): name(n) { }

    void operator()() {
        // notify the boss when work is done
        synchronizedOut(name + " : " + "Work done!\n");
        workDone.count_down();

        // waiting before going home
        goHome.wait();
        synchronizedOut(name + " : " + "Good bye!\n");
    }
private:
    std::string name;
};

int main() {

    std::cout << '\n';

    std::cout << "BOSS: START WORKING!" << '\n';

    Worker herb("Herb");
    std::thread herbWork(herb);

    Worker scott("Scott");
    std::thread scottWork(scott);

    Worker bjarne("Bjarne");
    std::thread bjarneWork(bjarne);

    Worker andrei("Andrei");
    std::thread andreiWork(andrei);

    Worker andrew("Andrew");
    std::thread andrewWork(andrew);

    Worker david("David");
    std::thread davidWork(david);

    workDone.wait();

    std::cout << '\n';

    goHome.count_down();

    std::cout << "BOSS: GO HOME!" << '\n';
}
```

