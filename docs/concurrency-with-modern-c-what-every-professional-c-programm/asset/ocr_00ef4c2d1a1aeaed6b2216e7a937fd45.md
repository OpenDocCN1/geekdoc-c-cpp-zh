```
```cpp
{
    lock_guard<mutex> lockGuard(activationListMutex);
    activationList.push_back(move(pair));
}
return isPrimeFuture;
}

void run() {
    vector<jthread> allServers;
    // only one thread because the activation list is the bottleneck
    for (int n = 0; n < 1; ++n) {
        allServers.emplace_back([this] {
            while (!runNextTask());
        });
    }
}

private:

    bool runNextTask() {
        lock_guard<mutex> lockGuard(activationListMutex);
        auto empty = activationList.empty();
        if (!empty) {
            auto myTask = std::move(activationList.front());
            activationList.pop_front();
            myTask.first(myTask.second);
        }
        return empty;
    }

    deque<pair<packaged_task<pair<bool, int>(int)>, int >> activationList;
    mutex activationListMutex;
};

vector<int> getRandNumbers(int number) {
    random_device seed;
    mt19937 engine(seed());
    uniform_int_distribution<> dist(1000000, 1000000000);
    vector<int> numbers;
    for (long long i = 0; i < number; ++i) numbers.push_back(dist(engine));
    return numbers;
}

future<vector<future<pair<bool, int>>>> getFutures(ActiveObject& activeObject,
                                                    int numberPrimes) {
```
```