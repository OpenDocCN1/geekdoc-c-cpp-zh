
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

Stop request arrives after the callback registration

## 3.6.4 A General Mechanism to Send Signals

The pair `std::stop_source` and `std::stop_token` can be considered as a general mechanism to send a signal. By copying the `std::stop_token`, you can send the signal to any entity executing something.

In the following example, I use std::async, std::promise, std::thread, and std::jthread in various combinations.

### Sending a signal to various executing entities

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

- Finished: The call `stopSource.request_stop` has no effect. The callback is not executed.

Let’s see what happens when I join the threads `thr1` and `thr2` before the call `stopSource.request_stop` in the previous program `signalStopRequests.cpp`. Here are the lines 44 and 45 swapped with the lines 47 and 48.

### Sending the signal too late

```
44    thr1.join();
45    thr2.join();

47    stopSource.request_stop();
48    if (stopToken.stop_requested()) std::cout << "main: Stop requested\n";
```

The swap of the lines affects that only the main-thread reacts to the signal.

![](img/d61a6c83410484053b8892275d2fcc4f_187_0.png)

## 3.6.5 Additional Functionality of `std::jthread`

A `std::jthread` is a `std::thread` with the additional functionality of cooperative interruption. To support this functionality it has a `std::stop_source`.

The member functions of `std::jthread` `jthr` for stop-token handling

| Member Function | Description |
|---|---|
| `jthr.get_stop_source()` | Returns a `std::stop_source` object associated with the shared stop state. |
| `jthr.get_stop_token()` | Returns a `std::stop_token` object associated with the shared stop state. |
| `jthr.request_stop()` | Requests execution stop via the shared stop state. Returns true if the stop request was successful. |

The section `std::jthread` provides the details about cooperative interruption of a `std::jthread`.

## 3.6.6 New wait Overloads for the `condition_variable_any`

`std::condition_variable_any` is a generalization of `std::condition_variable`<sup>45</sup>. `std::condition_variable` requires a `std::unique_lock<std::mutex>`, but `std::condition_variable_any` can operate on any lock, supporting `lock()` and `unlock()`.

The three wait variations to `wait`, `wait_for`, and `wait_until` of the `std::condition_variable_any` get new overloads. They take a `std::stop_token`.

**Three new wait overloads**

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

These new overloads require a predicate. The presented versions ensure that the threads are notified if a stop request for the passed `std::stop_token stoken` is signaled. The functions return a boolean that indicates whether the predicate evaluates to true. This returned boolean is independent of whether a stop was requested or whether the timeout was triggered. The three overloads are equivalent to the following expressions:

> 45 https://en.cppreference.com/w/cpp/thread/condition_variable

### Equivalent expression for the three overloads

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

After the wait calls, you can check if a stop request happened.

### Handle interrupts with wait

```cpp
cv.wait(lock, stoken, predicate);
if (stoken.stop_requested()){
    // interrupt occurred
}
```

### Use of condition variable with a stop request

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

## 3.7 Semaphores (C++20)

Semaphores are a synchronization mechanism used to control concurrent access to a shared resource. A counting semaphore is a semaphore that has a counter that is bigger than zero. The constructor initializes the counter. Acquiring the semaphore decreases the counter, and releasing the semaphore increases the counter. If a thread tries to acquire the semaphore when the counter is zero, the thread will block until another thread increments the counter by releasing the semaphore.

### Edgar W. Dijkstra invented semaphores

The Dutch computer scientist Edgar W. Dijkstra<sup>15</sup> presented in 1965 the concept of a semaphore. A semaphore is a data structure with a queue and a counter. The counter is initialized to a value equal to or greater than zero. It supports the two operations wait and signal. Operation wait acquires the semaphore and decreases the counter. It blocks the thread from acquiring the semaphore if the counter is zero. Operation signal releases the semaphore and increases the counter. Blocked threads are added to the queue to avoid starvation<sup>17</sup>.

Originally, a semaphore was a railway signal.

![](img/d61a6c83410484053b8892275d2fcc4f_192_0.png)

Semaphore

The original uploader was AmosWolfe at English Wikipedia. - Transferred from en.wikipedia to Commons., CC BY 2.6.<sup>18</sup>

C++20 supports a `std::binary_semaphore`, which is an alias for a `std::counting_semaphore<1>`. In this

- 15. https://en.wikipedia.org/wiki/Edgar_W._Dijkstra
- 17. https://en.wikipedia.org/wiki/Starvation_(computer_science)
- 18. https://commons.wikimedia.org/w/index.php?curid=1972304
