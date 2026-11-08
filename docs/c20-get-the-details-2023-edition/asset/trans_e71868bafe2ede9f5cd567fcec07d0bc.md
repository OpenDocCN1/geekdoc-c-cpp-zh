

### 使用条件变量进行线程同步

```cpp
std::thread t1(prepareWork);
std::thread t2(completeWork);

t1.join();
t2.join();

std::cout << '\n';

}
```

该程序有两个子线程：t1 和 t2。它们分别在第 40 行和第 41 行获得各自的任务负载 prepareWork 和 completeWork。函数 prepareWork（第 14 行）通知工作准备已完成：`condVar.notify_one()`。线程 t2 在持有锁的情况下等待通知：`condVar.wait(lock, [] { return not myVec.empty(); });`。等待线程始终执行相同的步骤。被唤醒时，它在持有锁的情况下检查谓词（`[] { return not myVec.empty(); }`）。如果谓词不成立，它就让自己重新休眠。如果谓词成立，它继续执行工作。在具体工作流中，发送线程将初始值放入 `std::vector`（第 18 行），接收线程完成这些值（第 29 行）。

```text
rainer@seminar:-> threadSynchronizationConditionVariables

Waiter: Waiting for data.
Sender: Data prepared.
Waiter: Complete the work.
0 1 2 3

rainer@seminar:-> threadSynchronizationConditionVariables

Sender: Data prepared.
Waiter: Waiting for data.
Waiter: Complete the work.
0 1 2 3

rainer@seminar:-> threadSynchronizationConditionVariables

Waiter: Waiting for data.
Sender: Data prepared.
Waiter: Complete the work.
0 1 2 3

rainer@seminar:-> threadSynchronizationConditionVariables

Sender: Data prepared.
Waiter: Waiting for data.
Waiter: Complete the work.
0 1 2 3

rainer@seminar:->
```

### 使用条件变量进行线程同步

条件变量有许多固有问题。例如，接收方可能在没有通知的情况下被唤醒，或者可能丢失通知。第一个问题称为虚假唤醒，第二个问题称为丢失唤醒。谓词可以防止这两个缺陷。如果发送方在接收方进入等待状态之前发送通知，并且没有使用谓词，通知就可能丢失。因此，接收方会等待一件永远不会发生的事情。这就是死锁。当你研究程序的输出时，你会看到，如果我不使用谓词，每隔一次运行就会导致死锁。当然，也可以在不使用谓词的情况下使用条件变量。

如果你想了解发送方-接收方工作流的细节以及条件变量的陷阱，请阅读我的文章“C++ Core Guidelines：注意条件变量的陷阱”。

22) https://www.modernescpp.com/index.php/c-core-guidelines-be-aware-of-the-traps-of-condition-variables

让我使用 future/promise 对实现相同的工作流。

### 6.2.3.3.2 Future 与 Promise

一个 promise 可以向其关联的 future 发送一个值、一个异常或一个通知。以下是使用 promise 和 future 的相应工作流。

使用 promise/future 对进行线程同步

```cpp
// threadSynchronizationPromiseFuture.cpp

#include <iostream>
#include <future>
#include <thread>
#include <vector>

std::vector<int> myVec{};

void prepareWork(std::promise<void> prom) {

    myVec.insert(myVec.end(), {0, 1, 0, 3});
    std::cout << "Sender: Data prepared." << '\n';
    prom.set_value();

}

void completeWork(std::future<void> fut){

    std::cout << "Waiter: Waiting for data." << '\n';
    fut.wait();
    myVec[2] = 2;
    std::cout << "Waiter: Complete the work." << '\n';
    for (auto i : myVec) std::cout << i << " ";
    std::cout << '\n';

}

int main() {

    std::cout << '\n';

    std::promise<void> sendNotification;
    auto waitForNotification = sendNotification.get_future();

    std::thread t1(prepareWork, std::move(sendNotification));
    std::thread t2(completeWork, std::move(waitForNotification));

    t1.join();
    t2.join();

    std::cout << '\n';

}
```

当你研究工作流时，你会认识到同步被简化为其本质部分：`prom.set_value()`（第 14 行）和 `fut.wait()`（第 21 行）。我跳过这次运行的截图，因为它与之前使用条件变量的运行基本相同。

以下是关于 promise 和 future 的更多信息，它们通常简称为任务<sup>29</sup>。

<sup>29</sup> https://www.modernescpp.com/index.php/tag/tasks

### 6.2.3.3 `std::atomic_flag`

现在，我直接从 C++11 跳到 C++20。

使用 `std::atomic_flag` 进行线程同步

```cpp
// threadSynchronizationAtomicFlag.cpp

#include <atomic>
#include <iostream>
#include <thread>
#include <vector>

std::vector<int> myVec{};

std::atomic_flag atomicFlag{};

void prepareWork() {

    myVec.insert(myVec.end(), {0, 1, 0, 3});
    std::cout << "Sender: Data prepared." << '\n';
    atomicFlag.test_and_set();
    atomicFlag.notify_one();

}

void completeWork() {

    std::cout << "Waiter: Waiting for data." << '\n';
    atomicFlag.wait(false);
    myVec[2] = 2;
    std::cout << "Waiter: Complete the work." << '\n';
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

准备工作线程（第 16 行）将 atomicFlag 设置为 true 并发送通知。完成工作的线程正在等待通知。只有当 atomicFlag 等于 true 时，它才会解除阻塞。

以下是使用 Microsoft 编译器运行该程序的几次结果。

![](img/c60a87adb7f61e2e82071d081bbb389a_498_0.png)

使用 `std::atomic_flag` 进行线程同步

## 6.2.4 `std::atomic` 扩展

在 C++20 中，`std::atomic`<sup>30</sup> 像 `std::atomic_ref` 一样，可以用 float、double 和 long double 等浮点类型实例化。此外，`std::atomic_flag` 和 `std::atomic` 可以通过成员函数 `notify_one`、`notify_all` 和 `wait` 用于线程同步。通知和等待功能适用于 `std::atomic` 的所有部分特化和完全特化（bool、整数、浮点和指针）以及 `std::atomic_ref`。

得益于 atomic\<bool\>，之前的程序 `threadSynchronizationAtomicFlag.cpp` 可以直接重新实现。

<sup>30</sup> https://en.cppreference.com/w/cpp/atomic/atomic

### 使用 `std::atomic<bool>` 进行线程同步

```cpp
// threadSynchronizationAtomicBool.cpp

#include <atomic>
#include <iostream>
#include <thread>
#include <vector>

std::vector<int> myVec{};

std::atomic<bool> atomicBool(false);

void prepareWork() {

    myVec.insert(myVec.end(), {0, 1, 0, 3});
    std::cout << "Sender: Data prepared." << '\n';
    atomicBool.store(true);
    atomicBool.notify_one();

}

void completeWork() {

    std::cout << "Waiter: Waiting for data." << '\n';
    atomicBool.wait(false);
    myVec[2] = 2;
    std::cout << "Waiter: Complete the work." << '\n';
    for (auto i : myVec) std::cout << i << " ";
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

调用 `atomicBool.wait(false)` 会在 `atomicBool == false` 成立时阻塞。因此，调用 `atomicBool.store(true)`（第 16 行）会将 `atomicBool` 设置为 true 并发送通知。

和之前一样，以下是使用 Microsoft 编译器运行的四次结果。

![](img/c60a87adb7f61e2e82071d081bbb389a_500_0.png)

## 6.3 信号量

![](img/c60a87adb7f61e2e82071d081bbb389a_502_0.png)

Cippi 指挥火车

信号量是一种同步机制，用于控制对共享资源的并发访问。计数信号量是一种特殊信号量，其计数器大于零。计数器在构造函数中初始化。获取信号量会使计数器递减，释放信号量会使计数器递增。如果线程在计数器为零时尝试获取信号量，该线程将阻塞，直到另一个线程通过释放信号量使计数器递增。

![](img/c60a87adb7f61e2e82071d081bbb389a_502_1.png)

### Edsger W. Dijkstra 发明了信号量

荷兰计算机科学家 Edsger W. Dijkstra<sup>31</sup> 于 1965 年提出了信号量的概念。信号量是一种带有队列和计数器的数据结构。计数器被初始化为大于或等于零的值。它支持 wait 和 signal 两个操作。wait 操作获取信号量并使计数器递减。如果计数器为零，它会阻塞线程获取信号量。signal 操作释放信号量并使计数器递增。被阻塞的线程会被加入队列，以避免饥饿<sup>32</sup>。

最初，信号量是一种铁路信号。

<sup>31</sup> https://en.wikipedia.org/wiki/Edsger_W._Dijkstra
<sup>32</sup> https://en.wikipedia.org/wiki/Starvation_(computer_science)

