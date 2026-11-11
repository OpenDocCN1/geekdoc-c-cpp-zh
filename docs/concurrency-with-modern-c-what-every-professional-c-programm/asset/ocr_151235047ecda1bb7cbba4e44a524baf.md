![](bbox=[0.265, 0.12, 0.731, 0.499])

A boss-worker workflow using two std::latch

When you think about this workflow, you may notice that it can be done without a boss. Here it is.

# A worker's workflow using a std::latch

```
```cpp
 1  // workers.cpp
 2
 3  #include <iostream>
 4  #include <barrier>
 5  #include <mutex>
 6  #include <thread>
 7
 8  std::latch workDone(6);
 9  std::mutex coutMutex;
10
11  void synchronizedOut(const std::string& s) {
12      std::lock_guard<std::mutex> lo(coutMutex);
13      std::cout << s;
14  }
15
16  class Worker {
17  public:
18      Worker(std::string n): name(n) { };
```
```