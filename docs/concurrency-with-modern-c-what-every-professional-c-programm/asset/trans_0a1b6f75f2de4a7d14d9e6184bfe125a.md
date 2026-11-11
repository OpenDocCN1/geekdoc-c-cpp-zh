
```cpp
using handler_t = std::function<void()>;
using callback_t = std::stop_callback<handler_t>;

void func(std::stop_token stopToken) {
    std::list<callback_t> callbacks;
    for (int i = 0; i < 9; ++i) {
        callbacks.emplace_back(stopToken, [i] { std::cout << i; });
    }
    std::this_thread::sleep_for(100ms);
    std::cout << '\n';
}

int main() {
    std::cout << '\n';

    std::jthread thr1 = std::jthread(func);
    std::jthread thr2 = std::jthread(func);
    std::this_thread::sleep_for(50ms);
    thr1.request_stop();
    thr2.request_stop();

    std::cout << '\n';
}
```

![](img/d61a6c83410484053b8892275d2fcc4f_184_0.png)

停止请求在回调注册之后到达

## 3.6.4 发送信号的通用机制

`std::stop_source` 和 `std::stop_token` 这一对可以被视为发送信号的通用机制。通过复制 `std::stop_token`，你可以将信号发送给任何正在执行某些操作的实体。

在下面的示例中，我以各种组合使用 std::async、std::promise、std::thread 和 std::jthread。

### 向各种执行实体发送信号

```cpp
// signalStopRequests.cpp

#include <iostream>
#include <thread>
#include <future>

using namespace std::literals;

void function1(std::stop_token stopToken, const std::string& str){
    std::this_thread::sleep_for(1s);
    if (stopToken.stop_requested()) std::cout << str << ": Stop requested\n";
}

void function2(std::promise<void> prom,
               std::stop_token stopToken, const std::string& str) {
    std::this_thread::sleep_for(1s);
    std::stop_callback callBack(stopToken, [&str] {
        std::cout << str << ": Stop requested\n";
    });
    prom.set_value();
}

int main() {

    std::cout << '\n';

    std::stop_source stopSource;

    std::stop_token stopToken = std::stop_token(stopSource.get_token());

    std::thread thr1 = std::thread(function1, stopToken, "std::thread");

    std::jthread jthr = std::jthread(function1, "std::jthread");

    auto fut1 = std::async([stopToken] {
        std::this_thread::sleep_for(1s);
        if (stopToken.stop_requested()) std::cout << "std::async: Stop requested\n";
    });

    std::promise<void> prom;
    auto fut2 = prom.get_future();
```

- 已完成：调用 `stopSource.request_stop` 无效。回调不会执行。

让我们看看在上一个程序 `signalStopRequests.cpp` 中，在调用 `stopSource.request_stop` 之前先 join 线程 `thr1` 和 `thr2` 会发生什么。这里第 44 和 45 行与第 47 和 48 行交换了。

### 过晚发送信号

```
44    thr1.join();
45    thr2.join();

47    stopSource.request_stop();
48    if (stopToken.stop_requested()) std::cout << "main: Stop requested\n";
```

行的交换导致只有主线程对信号作出反应。

![](img/d61a6c83410484053b8892275d2fcc4f_187_0.png)

## 3.6.5 `std::jthread` 的附加功能

`std::jthread` 是一个具有协作式中断附加功能的 `std::thread`。为了支持此功能，它拥有一个 `std::stop_source`。

`std::jthread` 对象 `jthr` 用于停止令牌处理的成员函数

| 成员函数 | 描述 |
|---|---|
| `jthr.get_stop_source()` | 返回与共享停止状态关联的 `std::stop_source` 对象。 |
| `jthr.get_stop_token()` | 返回与共享停止状态关联的 `std::stop_token` 对象。 |
| `jthr.request_stop()` | 通过共享停止状态请求停止执行。如果停止请求成功，则返回 true。 |

`std::jthread` 一节提供了关于 `std::jthread` 协作式中断的详细信息。

## 3.6.6 `condition_variable_any` 的新等待重载

`std::condition_variable_any` 是 `std::condition_variable`<sup>45</sup> 的泛化。`std::condition_variable` 需要 `std::unique_lock<std::mutex>`，但 `std::condition_variable_any` 可以作用于任何锁，支持 `lock()` 和 `unlock()`。

`std::condition_variable_any` 的 `wait`、`wait_for` 和 `wait_until` 三种等待变体获得了新的重载。它们接受一个 `std::stop_token`。

**三种新的等待重载**

```cpp
template <class Predicate>
bool wait(Lock& lock,
          stop_token stoken,
          Predicate pred);

template <class Rep, class Period, class Predicate>
bool wait_for(Lock& lock,
              stop_token stoken,
              const chrono::duration<Rep, Period>& rel_time,
              Predicate pred);

template <class Clock, class Duration, class Predicate>
bool wait_until(Lock& lock,
                stop_token stoken,
                const chrono::time_point<Clock, Duration>& abs_time,
                Predicate pred);
```

这些新重载需要一个谓词。所展示的版本确保如果传入的 `std::stop_token stoken` 的停止请求被发出信号，线程会被通知。函数返回一个布尔值，指示谓词是否求值为 true。返回的布尔值与是否请求停止或是否触发超时无关。三个重载等价于以下表达式：

> 45 https://en.cppreference.com/w/cpp/thread/condition_variable

### 三个重载的等价表达式

```cpp
// wait in lines 1 - 4
while (!token.stop_requested()) {
    if (pred()) return true;
    wait(lock);
}
return pred();

// wait_for in lines 6 - 10
return wait_until(lock,
                  std::chrono::steady_clock::now() + rel_time,
                  std::move(pred)
                  );

// wait_until in lines 12 - 16
while (!token.stop_requested()) {
    if (pred()) return true;
    if (wait_until(lock, timeout_time) == std::cv_status::timeout) return pred();
}
return pred();
```

在等待调用之后，你可以检查是否发生了停止请求。

### 使用 wait 处理中断

```cpp
cv.wait(lock, stoken, predicate);
if (stoken.stop_requested()){
    // interrupt occurred
}
```

### 带停止请求使用条件变量

```cpp
// conditionalVariableAny.cpp

#include <condition_variable>
#include <thread>
#include <iostream>
#include <chrono>
#include <mutex>
#include <thread>

using namespace std::literals;

std::mutex mut;
std::condition_variable_any condVar;

bool dataReady;

void receiver(std::stop_token stopToken) {

    std::cout << "Waiting" << '\n';

    std::unique_lock<std::mutex> lck(mut);
    bool ret = condVar.wait(lck, stopToken, []{ return dataReady; });
    if (ret) {
        std::cout << "Notification received: " << '\n';
    }
    else {
        std::cout << "Stop request received" << '\n';
    }
}

void sender() {

    std::this_thread::sleep_for(5ms);
    {
        std::lock_guard<std::mutex> lck(mut);
        dataReady = true;
        std::cout << "Send notification" << '\n';
    }
    condVar.notify_one();

}

int main(){

    std::cout << '\n';

    std::jthread t1(receiver);
    std::jthread t2(sender);

    t1.request_stop();

    t1.join();
    t2.join();

    std::cout << '\n';
}
```

## 3.7 信号量（C++20）

信号量是一种用于控制对共享资源并发访问的同步机制。计数信号量是计数器大于零的信号量。构造函数初始化计数器。获取信号量会减少计数器，释放信号量会增加计数器。如果线程在计数器为零时尝试获取信号量，该线程将阻塞，直到另一个线程通过释放信号量来增加计数器。

### Edgar W. Dijkstra 发明了信号量

荷兰计算机科学家 Edgar W. Dijkstra<sup>15</sup> 于 1965 年提出了信号量的概念。信号量是一种带有队列和计数器的数据结构。计数器初始化为等于或大于零的值。它支持 wait 和 signal 两种操作。操作 wait 获取信号量并减少计数器。如果计数器为零，它会阻塞线程获取信号量。操作 signal 释放信号量并增加计数器。被阻塞的线程被加入队列以避免饥饿<sup>17</sup>。

最初，信号量是一种铁路信号。

![](img/d61a6c83410484053b8892275d2fcc4f_192_0.png)

信号量

原始上传者为英文维基百科的 AmosWolfe。- 从 en.wikipedia 转移至 Commons，CC BY 2.6。<sup>18</sup>

C++20 支持 `std::binary_semaphore`，它是 `std::counting_semaphore<1>` 的别名。在本文中

- 15. https://en.wikipedia.org/wiki/Edgar_W._Dijkstra
- 17. https://en.wikipedia.org/wiki/Starvation_(computer_science)
- 18. https://commons.wikimedia.org/w/index.php?curid=1972304

