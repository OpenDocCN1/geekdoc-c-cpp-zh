# 7.3 Future

```
int v = 1;

void critical_section(int change_v) {
    static std::mutex mtx;
    std::unique_lock<std::mutex> lock(mtx);
    // do contention operations
    v = change_v;
    std::cout << v << std::endl;
    // release the lock
    unlock();

    // during this period,
    // others are allowed to acquire v

    // start another group of contention operations
    // lock again
    lock();
    v += 1;
    std::cout << v << std::endl;
}

int main() {
    std::thread t1(critical_section, 2), t2(critical_section, 3);
    t1.join();
    t2.join();
    return 0;
}
```

# 7.3 Future

The Future is represented by std::future, which provides a way to access the results of asynchronous operations. This sentence is very difficult to understand. In order to understand this feature, we need to understand the multi-threaded behavior before C++11.

Imagine if main thread A wants to open a new thread B to perform some of our expected tasks and return a result. At this time, thread A may be busy with other threads, and have no time to take into account the results of B. So naturally hope to get the result of thread B at a certain time.

Before the introduction of std::future in C++11, the usual practice is: Create a variable, start task B in thread A, start an event when it is ready, and save the result in a global variable. The main function A doing other things. When the result is needed, a thread is called to wait for the function to get the result of the execution.