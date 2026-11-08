# Full-time and part-time workers

```
```cpp
// FullTimePartTimeWorkers.cpp

#include <iostream>
#include <barrier>
#include <mutex>
#include <string>
#include <thread>

std::barrier workDone(6);
std::mutex coutMutex;

void synchronizedOut(const std::string& s) {
    std::lock_guard<std::mutex> lg(coutMutex);
    std::cout << s;
}

class FullTimeWorker {
public:
    FullTimeWorker(std::string n): name(n) { }

    void operator()() {
        synchronizedOut(name + ": " + "Morning work done!\n");
        workDone.arrive_and_wait();  // Wait until morning work is done
        synchronizedOut(name + ": " + "Afternoon work done!\n");
        workDone.arrive_and_wait();  // Wait until afternoon work is done
    }

private:
    std::string name;
};

class PartTimeWorker {
public:
    PartTimeWorker(std::string n): name(n) { }

    void operator()() {
        synchronizedOut(name + ": " + "Morning work done!\n");
        workDone.arrive_and_drop();  // Wait until morning work is done
    }

private:
    std::string name;
};

int main() {
```
```