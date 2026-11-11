

![](img/d61a6c83410484053b8892275d2fcc4f_199_0.png)

使用两个 `std::latch` 的老板-工人工作流程

当你思考这个工作流程时，可能会注意到没有老板也能完成。如下所示。

### 使用 `std::latch` 的工作者工作流程

```cpp
 1  // workers.cpp
 2
 3  #include <iostream>
 4  #include <latch>
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
19      void operator()() {
20          synchronizedOut(name + ": " + "Work done!\n");
21          workDone.arrive_and_wait(); // wait until all work is done
22          synchronizedOut(name + ": " + "See you tomorrow!\n");
23      }
24
25  private:
26      std::string name;
27  };
28
29  int main() {
30
31      std::cout << '\n';
32
33      Worker herb("  Herb");
34      std::thread herbWork(herb);
35
36      Worker scott("    Scott");
37      std::thread scottWork(scott);
38
39      Worker bjarne("      Bjarne");
40      std::thread bjarneWork(bjarne);
41
42      Worker andrei("        Andrei");
43      std::thread andreiWork(andrei);
44
45      Worker andrew("          Andrew");
46      std::thread andrewWork(andrew);
47
48      Worker david("            David");
49      std::thread davidWork(david);
50
51      herbWork.join();
52      scottWork.join();
53      bjarneWork.join();
54      andreiWork.join();
55      andrewWork.join();
56      davidWork.join();
57
58  }
```

这个简化的工作流程无需过多解释。调用 `workDone.arrive_and_wait()`（第 22 行）等价于调用 `count_down(upd); wait();`。这意味着工作者可以自行协调，不再需要老板，正如前一个程序 `bossWorkers.cpp` 中的情况。

![](img/d61a6c83410484053b8892275d2fcc4f_201_0.png)

`std::barrier` 与 `std::latch` 相似。

### 3.8.2 `std::barrier`

`std::latch` 和 `std::barrier` 之间有两个区别。首先，`std::barrier` 可以使用多次；其次，你可以为下一阶段调整计数器。计数器在 `std::barrier bar` 的构造函数中设置。调用 `bar.arrive()`、`bar.arrive_and_wait()` 和 `bar.arrive_and_drop()` 会递减当前阶段的计数器。此外，`bar.arrive_and_drop()` 还会递减下一阶段的计数器。当当前阶段结束、计数器变为零后，所谓的“完成步骤”（completion step）立即开始。在此完成步骤中，会调用一个可调用对象。`std::barrier` 在其构造函数中获取这个可调用对象。

完成步骤会执行以下步骤：

- 1. 所有线程都被阻塞。
- 2. 任意一个线程被解除阻塞并执行可调用对象。该可调用对象不得抛出异常，且必须是 `noexcept`。
- 3. 如果完成步骤已结束，所有线程都会被解除阻塞。

### `std::barrier` 的成员函数

| 成员函数 | 描述 |
| --- | --- |
| `std::barrier bar{cnt}` | 创建一个计数器为 `cnt` 的 `std::barrier`。 |
| `std::barrier bar{cnt, call}` | 创建一个计数器为 `cnt` 且带可调用对象 `call` 的 `std::barrier`。 |
| `bar.arrive(upd)` | 以原子方式将计数器递减 `upd`。 |
| `bar.wait()` | 在同步点阻塞，直到完成步骤结束。 |
| `bar.arrive_and_wait()` | 等价于 `wait(arrive())`。 |
| `bar.arrive_and_drop()` | 将当前阶段和后续阶段的计数器各减一。 |
| `std::barrier::max` | 实现支持的最大值。 |

调用 `bar.arrive_and_drop()` 本质上意味着下一阶段的计数器减一。

程序 `FullTimePartTimeWorkers.cpp` 在第二阶段将工作者数量减半。

### 全职与兼职工作者

```cpp
// FullTimePartTimeWorkers.cpp

#include <iostream>
#include <barrier>
#include <mutex>
#include <string>
#include <thread>

std::barrier workDone(6);
std::mutex coutMutex;

void synchronizedOut(const std::string& s) noexcept {
  std::lock_guard<std::mutex> lo(coutMutex);
  std::cout << s;
}

class FullTimeWorker {
public:
  FullTimeWorker(std::string n): name(n) { };

  void operator() () {
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
  PartTimeWorker(std::string n): name(n) { };

  void operator() () {
    synchronizedOut(name + ": " + "Morning work done!\n");
    workDone.arrive_and_drop();  // Wait until morning work is done
  }
private:
  std::string name;
};

int main() {

  std::cout << '\n';

  FullTimeWorker herb("  Herb");
  std::thread herbWork(herb);

  FullTimeWorker scott("  Scott");
  std::thread scottWork(scott);

  FullTimeWorker bjarne("  Bjarne");
  std::thread bjarneWork(bjarne);

  PartTimeWorker andrei("  Andrei");
  std::thread andreiWork(andrei);

  PartTimeWorker andrew("  Andrew");
  std::thread andrewWork(andrew);

  PartTimeWorker david("  David");
  std::thread davidWork(david);

  herbWork.join();
  scottWork.join();
```

## 3.9 任务

除了线程之外，C++ 还提供了任务（task）来异步执行工作。任务需要 `<future>` 头文件。任务以工作包为参数，由两个关联的组件组成：promise 和 future。两者通过数据通道连接。promise 执行工作包并将结果放入数据通道；关联的 future 获取结果。两个通信端点可以运行在独立的线程中。特别之处在于，关联的 future 可以获取结果；因此，promise 计算结果与关联 future 查询结果相互独立。

![](img/d61a6c83410484053b8892275d2fcc4f_205_0.png)

### 将任务视为通信端点之间的数据通道

任务的行为类似于通信端点之间的数据通道。数据通道的一个端点称为 promise，另一个端点称为 future。这些端点可以存在于相同或不同的线程中。promise 将结果放入数据通道，future 稍后获取。

![](img/d61a6c83410484053b8892275d2fcc4f_205_1.png)

任务作为通信端点之间的数据通道

### 3.9.1 任务与线程

任务与线程截然不同。

### 3.9.2.2 即发即忘

即发即忘的 future 是一种特殊的 future。它们就在原地执行，因为其 future 未绑定到任何变量。对于即发即忘的 future，promise 必须运行在单独的线程中才能立即开始工作，这是通过 `std::launch::async` 策略实现的。

让我们比较一个普通 future 和一个即发即忘的 future。

```cpp
auto fut= std::async([]{ return 2011; });
std::cout << fut.get() << '\n';

std::async(std::launch::async,
           []{ std::cout << "fire and forget" << '\n'; });
```

即发即忘的 future 看起来很有吸引力，但有一个很大的缺点：由 `std::async` 创建的 future 会在其析构函数中等待，直到其 promise 完成。在这种情况下，等待与阻塞没有太大区别。future 在其析构函数中会阻塞程序的执行进度。当你使用即发即忘的 future 时，这一点会更加明显：看似并发的操作实际上是顺序执行的。

### 即发即忘的 future

```cpp
// fireAndForgetFutures.cpp

#include <chrono>
#include <future>
#include <iostream>
#include <thread>

int main(){

    std::cout << '\n';

    std::async(std::launch::async, []{
        std::this_thread::sleep_for(std::chrono::seconds(2));
        std::cout << "first thread" << '\n';
    });

    std::async(std::launch::async, []{
        std::this_thread::sleep_for(std::chrono::seconds(1));
        std::cout << "second thread" << '\n';
    });

    std::cout << "main thread" << '\n';

    std::cout << '\n';
```

