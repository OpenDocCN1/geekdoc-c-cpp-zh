the deposit must be made before the withdrawal.

```
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex mu;
std::condition_variable cv;
size_t balance = 0; // shared resource

void deposit(size_t amt) {
    mu.lock();
    balance += amt;
    mu.unlock();
    cv.notify_one();
}

void withdraw(size_t amt) {
    std::unique_lock<std::mutex> ul(mu);
    cv.wait(ul, [] () { return balance > 0 ? true : false; });
    balance -= amt;
    ul.unlock();
}

int main() {
    std::thread t1(deposit, 500);
    std::thread t2(withdraw, 400);
    t1.join();
    t2.join();
    std::cout << "final balance: " << balance << std::endl;
    return 0;
}
```

Notice that use of the condition variable cv requires a unique_lock. In the withdraw function, we first try to lock the mutex mu. If we cannot lock the mutex, we keep on waiting. If the lock succeeds, we test the value of cv.wait().

The first parameter of cv.wait is the unique_lock mutex. The second parameter is a lambda that implements a predicate condition. If the condition evaluates to true,