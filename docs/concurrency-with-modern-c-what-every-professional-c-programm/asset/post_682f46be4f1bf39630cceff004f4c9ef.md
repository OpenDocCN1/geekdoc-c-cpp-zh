
- `condVar.wait(lck)`: If the condition_variable condVar is waiting and gets a notification or a spurious wakeup the following steps happen.
  - The thread is unblocked and reacquires the lock on the mutex.
  - The thread checks the predicate.
  - If the call of the predicate evaluates to
    - `true`: the thread continues its work.
    - `false`: `condVar.wait()` unlocks the mutex and puts the thread in a waiting (blocking) state.

Even if the shared variable is atomic, it must be modified under the mutex to correctly publish the modification to the waiting thread.

## Use a mutex to protect the shared variable

Even if you make dataReady an atomic, it must be modified under the mutex; if not the modification to the waiting thread may be published but not correctly synchronized. This race condition may cause a deadlock. What does that mean: published, but not correctly synchronized. Let's have a closer look at the wait workflow and assume that dataReady is atomic and is modified, not protected by the mutex mutex_.

```cpp
1    std::unique_lock<std::mutex> lck(mutex_);
2    while (![]{ return dataReady.load(); }()) {
3        // time window
4        condVar.wait(lck);
5    }
```

Let me assume the notification is sent while the condition variable condVar is not waiting. This means the thread's execution is in the code snippet between line 2 and 4 (see the comment time window). The result is that the notification is lost. Afterward, the thread goes back waiting and presumably sleeps forever.

This wouldn't have happened if a mutex had protected 'dataReady'. Because of the synchronization with the mutex, the notification would only be sent if the condition variable and, therefore, the receiver thread is waiting.

In most of the use-cases, tasks are the less error-prone way to synchronize threads. I compare condition variables and tasks in the section Returning a Notification.

## 3.6 Cooperative Interruption (C++20)

The additional functionality of the cooperative interruption thread is based on the std::stop_source, std::stop_token, and the std::stop_callback classes. std::jthread and std::condition_variable_any support cooperative interruption by design.

First, why it is not a good idea to kill a thread?

### Killing a Thread is Dangerous

Killing a thread is dangerous because you don't know the state of the thread. Here are two possible malicious outcomes.

- The thread is only half-done with its job. Consequently, you don't know the state of its job and, hence, the state of your program. You end with undefined behavior, and all bets are off.
- The thread may be in a critical section and having locked a mutex. Killing a thread while it locks a mutex ends with a high probability in a deadlock.

The std::stop_source, std::stop_token, and the std::stop_callback classes allow a thread to asynchronously request an execution to stop or ask if an execution got a stop signal. The std::stop_token can be passed to an operation and afterward be used to actively poll the token for a stop request or to register a callback via std::stop_callback. The stop request is sent by a std::stop_source. This signal affects all associated std::stop_token. The three classes std::stop_source, std::stop_token, and the std::stop_callback share the ownership of an associated stop state.

In the next subsections, I provide more details about cooperative interruption.

### 3.6.1 std::stop_source

You can construct a std::stop_source in two ways:

Constructors of std::stop_source

```cpp
std::stop_source();
explicit std::stop_source(std::nostopstate_t) noexcept;
```

The default constructor (line 1) constructs a std::stop_source with a new stop state. The constructor taking std::nostopstate_t (line 2) constructs an empty std::stop_source without associated stop state.

The component std::stop_source src provides the following member functions for handling stop requests.

### Member functions of std::stop_source

| Member function | Description |
| --- | --- |
| std::stop_source src | The default constructor creates a stop source with an associated stop state. |
| std::stop_source src(nostopstate) | Creates a stop_source without associated stop state. |
| src.get_token() | If src.stop_possible(), returns a stop_token for the associated stop state. Otherwise, returns a default-constructed (empty) stop_token. |
| src.stop_possible() | true if src can be requested to stop. |
| src.stop_requested() | true if stop_possible() and request_stop() was called by one of the owners. |
| src.request_stop() | Calls a stop request if src.stop_possible() and !src.stop_requested(). Otherwise, the call has no effect. |

The call src.get_token() returns the stop token token. Thanks to token you can check if a stop request has been made or can be made by its associated stop source src. The stop token observes the stop source src.

src.stop_requested() returns true when src has an associated stop state and was asked to stop earlier.

src.stop_possible() returns false if there is no associated stop state or no stop source anymore and stop was never requested before.

The calls src.stop_possible(), src.stop_requested(), and src.request_stop() are thread-safe.

src.request_stop() of a stop source src is visible to all std::stop_token and registered callback of the same associated stop state. Also, any std::condition_variable_any waiting on the associated std::stop_token will be awakened. When a stop is requested, it cannot be withdrawn. src.request_stop() is successful and returns true if src has an associated stop state and it was not requested to stop before.

### 3.6.2 std::stop_token

std::stop_token is essentially a thread-safe "view" of the associated stop state. It is typically retrieved from a std::jthread or a std::stop_source src via src.get_token(). This causes them to share the same associated stop state as the std::jthread or std::stop_source.

Thanks to the std::stop_token, you can check for the associated std::stop_source if a stop request has been made.

The std::stop_token can also be passed to the constructor of std::stop_callback, or to the interruptible waiting functions of std::condition_variable_any.

![](img/d61a6c83410484053b8892275d2fcc4f_182_0.png)

Use of callbacks

The std::stop_callback constructor registers the callback function for the std::stop_token given by the associated std::stop_source. This callback function is either invoked in the thread invoking request_stop() or the thread constructing the std::stop_callback. If the request to stop happens prior to the registration of the std::stop_callback, the callback is invoked in the thread constructing the std::stop_callback. Otherwise, the callback is invoked in the thread invoking request_stop().

You can register more than one callback for one or more threads using the same std::stop_token. The C++ standard provides no guarantee about the order in which they are executed.

### Stop request arrives before the callback registration

```cpp
1   // invokeCallbacks.cpp
2
3   #include <chrono>
4   #include <iostream>
5   #include <thread>
6
7   using namespace std::literals;
8
9   void func(std::stop_token stopToken) {
10      std::this_thread::sleep_for(100ms);
11      for (int i = 0; i <= 9; ++i) {
12          std::stop_callback cb(stopToken, [i] { std::cout << i; });
13      }
14      std::cout << '\n';
15  }
16
17  int main() {
18
19      std::cout << '\n';
20
21      std::jthread thr1 = std::jthread(func);
22      std::jthread thr2 = std::jthread(func);
23      thr1.request_stop();
24      thr2.request_stop();
25
26      std::cout << '\n';
27
28 }
```

![](img/d61a6c83410484053b8892275d2fcc4f_183_0.png)

Stop request arrives before the callback registration

The previous program `invokeCallbacks.cpp` illustrates when the stop request arrives before the callback registration, and thus the child thread has to execute each handler during registration.

The following program, `invokeCallbacksLoop.cpp`, illustrates when the callback has been registered before the stop request.

### Stop request arrives after the callback registration

```cpp
1 // invokeCallbacksLoop.cpp
2
3 #include <chrono>
4 #include <functional>
5 #include <iostream>
6 #include <list>
7 #include <stop_token>
8 #include <thread>
9
10 using namespace std::literals;
11
```
