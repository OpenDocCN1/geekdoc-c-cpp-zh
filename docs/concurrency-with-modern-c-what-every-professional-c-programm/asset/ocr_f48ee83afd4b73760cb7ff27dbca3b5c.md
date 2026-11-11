# Loophole in the interface

```
```cpp
1  // lockDouble.cpp
2
3  #include <future>
4  #include <iostream>
5  #include <mutex>
6
7  class LockDouble {
8  public:
9      double get() const {
10         std::lock_guard<std::mutex> lockDoubGuard(lockDoubMutex);
11         return lockDoub;
12     }
13
14     void set(double val) {
15         std::lock_guard<std::mutex> lockDoubGuard(lockDoubMutex);
16         lockDoub = val;
17     }
18
19     template <typename Func>
20     void apply(Func func){
21         std::lock_guard<std::mutex> lockDoubGuard(lockDoubMutex);
22         func(lockDoub);
23     }
24
25
26  private:
27     double lockDoub{};
28     mutable std::mutex lockDoubMutex;
29
30  };
31
32  int main(){
33
34     LockDouble lck1;
35
36     auto fut1 = std::async([&lck1]{ lck1.set(20.11); });
37     auto fut2 = std::async([&lck1]{ std::cout << lck1.get() << '\n'; });
38
39     double* loophole = nullptr;
40     lck1.apply([&loophole](double d) mutable { loophole = &d; });
41     *loophole = 11.22;
42
43     auto fut3 = std::async([&lck1]{ std::cout << lck1.get() << '\n'; });
```
```