```
```cpp
void waitingForWork(std::future<void>&& fut){

    std::cout << "Worker: Waiting for work." << '\n';
    fut.wait();
    doTheWork();
    std::cout << "Work done." << '\n';

}

void setDataReady(std::promise<void>&& prom){

    std::cout << "Sender: Data is ready." << '\n';
    prom.set_value();

}
```
```

# 9.2.4.1.2 Pull Principle

Instead of passively waiting for the state change, you can actively ask for it. This pull principle is not natively supported in C++ but can be, for example, implemented with atomics.

```
```cpp
std::vector<int> mySharedWork;
std::atomic<bool> dataReady(false);

void waitingForWork(){
    std::cout << "Waiting " << '\n';
    while (!dataReady.load()){
        std::this_thread::sleep_for(std::chrono::milliseconds(5));
    }
    mySharedWork[1] = 2;
    std::cout << "Work done " << '\n';
}

void setDataReady(){
    mySharedWork = {1, 0, 3};
    dataReady = true;
    std::cout << "Data prepared" << '\n';
}
```
```

# 9.2.4.2 Waiting with and without time boundary

A condition variable and a future have three member functions for waiting: wait, wait_for, and wait_until. The wait_for variant requires a time duration and the wait_until variant a time point. I skip