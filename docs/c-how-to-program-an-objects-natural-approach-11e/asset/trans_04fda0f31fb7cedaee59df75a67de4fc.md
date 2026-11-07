
- 当 `latch` 的计数变为 0 时，`latch` 会永久打开，解除对算法线程的阻塞，使其能够合并其工作线程的结果。

### 当网关永久打开时尝试等待

任意数量的线程都可以尝试等待给定的 `latch`。然而，一旦 `latch` 打开，其他尝试等待它的线程就会直接通过网关并继续执行。

### 演示闩锁

图 17.14 使用一个名为 `task` 的 lambda（第 22–34 行）来执行必须在 `main` 被允许继续执行之前完成的工作。正如本章通篇所做的那样，我们通过休眠来模拟工作。程序运行如下：

- 第 19 行创建计数为 3 的 `std::latch mainLatch`。任何等待 `mainLatch` 的线程都无法继续执行，直到三个线程到达 `mainLatch`。
- 第 40–46 行启动三个 `jthreads`——每个都执行 `task` lambda。
- 在 `main` 启动 `jthreads` 之后，第 49 行调用 `mainLatch` 的 `wait` 成员函数。如果 `mainLatch` 的计数大于 0，`main` 将在第 49 行等待，直到闩锁的计数达到 0。
- 当每个 `jthread` 的 `task` 调用到达第 32 行时，它会调用 `mainLatch` 的 `count_down` 成员函数来 `signal` 闩锁，从而递减其计数。尽管该任务在此程序中终止，但它本可以继续工作。关键在于，`main` 正在等待的工作应由每个线程在它 `signals` 闩锁之前完成。在输出中，请注意各线程以不同顺序向闩锁发送信号。
- 当 `mainLatch` 的计数达到 0 时，任何等待 `mainLatch` 的线程都会解除阻塞并继续执行。在此程序中，`main` 在第 51 行继续执行。
- 为了表明闩锁是一次性网关，第 53 行再次调用 `mainLatch` 的 `wait` 函数。由于 `mainLatch` 已经打开，`main` 会直接继续执行第 54 行，显示另一条消息，然后终止。

```cpp
1  // Fig. 17.14: LatchDemo.cpp
2  // Coordinate threads with a std::latch object.
3  #include <chrono>
4  #include <format>
5  #include <iostream>
6  #include <latch>
7  #include <random>
8  #include <string_view>
9  #include <thread>
10 #include <vector>
11
12 int main() {
13     // set up random-number generation
14     std::random_device rd;
15     std::default_random_engine engine{rd()};
16     std::uniform_int_distribution ints{2000, 3000};
17
18      // latch that 3 threads must signal before the main thread continues
19      std::latch mainLatch{3};
20
21      // lambda representing the task to execute
22      auto task{
23          [&](std::string_view name, std::chrono::milliseconds workTime) {
24              std::cout << std::format("Proceeding with {} work for {} ms.\n",
25                  name, workTime.count());
26
27              // simulate work by sleeping
28              std::this_thread::sleep_for(workTime);
29
30              // show that task arrived at mainLatch
31              std::cout << std::format("{} done; signals mainLatch.\n", name);
32              mainLatch.count_down();
33          }
34      };
35
36      std::vector<std::jthread> threads;  // stores the threads
37      std::cout << "Main starting three jthreads.\n";
38
39      // start three jthreads
40      for (int i{}; i < 3; ++i) {
41          // create jthread that calls task lambda,
42          // passing a task name and work time
43          threads.push_back(std::jthread(task,
44              std::format("Task {}", i),
45              std::chrono::milliseconds(ints(engine))));
46      }
47
48      std::cout << "\nMain waiting for jthreads to reach the latch.\n";
49      mainLatch.wait();
50
51      std::cout << "\nAll jthreads reached the latch. Main working.\n";
52      std::cout << "Showing that mainLatch is permanently open.\n";
53      mainLatch.wait(); // latch is already open
54      std::cout << "mainLatch is already open. Main continues.\n";
55  }
```

```text
Main starting three jthreads.

Main waiting for jthreads to reach the latch.

Proceeding with Task 3 work for 2648 ms.
Proceeding with Task 2 work for 2705 ms.
Proceeding with Task 1 work for 2024 ms.
Task 1 done; signals mainLatch.
Task 3 done; signals mainLatch.
Task 2 done; signals mainLatch.

All jthreads reached the latch. Main working.
Showing that mainLatch is permanently open.
mainLatch is already open. Main continues.
```

```text
Main starting three jthreads.

Main waiting for jthreads to reach the latch.

Proceeding with Task 2 work for 2571 ms.
Proceeding with Task 1 work for 2462 ms.
Proceeding with Task 3 work for 2248 ms.
Task 3 done; signals mainLatch.
Task 1 done; signals mainLatch.
Task 2 done; signals mainLatch.

All jthreads reached the latch. Main working.
Showing that mainLatch is permanently open.
mainLatch is already open. Main continues.
```

**图 17.14** | 使用 `std::latch` 对象协调线程。

## 17.13.2 C++20 `std::barrier`

考虑对自动化汽车装配线中喷漆步骤的模拟。通常，多个计算机控制的机器人协同工作来执行给定步骤。假设由独立线程控制沿装配线移动的汽车以及两个机器人的操作。一旦对一辆汽车的工作完成，我们希望重置一切、推进装配线，并为下一辆汽车再次执行该工作。前面的场景非常适合 `std::barrier`¹⁰⁴（来自 `<barrier>` 头文件），它就像一个可复用的闩锁。通常，屏障用于循环中的重复任务。

104. C++ 标准，“线程支持库——协调类型——屏障。”访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/thread.barrier.

- 每个线程先工作，然后到达一个**屏障**并等待它打开。
- 当指定数量的线程到达该**屏障**时，会执行一个可选的完成函数。
- 该**屏障**会重置其计数，从而解除对线程的阻塞，使它们可以继续执行并重复此过程。

使用一个**屏障**（图 17.15），我们来模拟装配线对多辆汽车的喷漆步骤。我们还将手动使用 **stop_source** 和 **stop_token** 来协调装配线关闭时的线程取消。同样，我们将使用休眠来模拟工作。请注意，在输出中，机器人有时会以不同顺序完成对每辆汽车的“工作”。

```cpp
1  // Fig. 17.15: BarrierDemo.cpp
2  // Coordinating threads with a std::barrier object.
3  #include <barrier>
4  #include <chrono>
5  #include <format>
6  #include <iostream>
7  #include <random>
8  #include <string_view>
9  #include <thread>

int main() {
    // simulate moving car into painting position
    auto moveCarIntoPosition =
        [&]() {
            std::cout << "Moving next car into painting position.\n";
            std::this_thread::sleep_for(std::chrono::seconds(2));
            std::cout << "Car ready for painting.\n\n";
        };

    int carsToPaint{3};

    // stop_source used to notify robots assembly line is shutting down
    std::stop_source assemblyLineStopSource;

    // stop_token used by paintingRobotTask to determine when to shut down
    std::stop_token stopToken{assemblyLineStopSource.get_token()};

    // assembly line waits for two painting robots to reach this barrier
    std::barrier syncPoint{2, [&]() noexcept { // lambda called when robots finish
        static int count{}; // # of cars that have been painted
        std::cout << "Painting robots completed tasks\n\n";

        // check whether it's time to shut down the assembly line
        if (++count == carsToPaint) {
            std::cout << "Shutting down assembly line\n\n";
            assemblyLineStopSource.request_stop();
        }
        else {
            moveCarIntoPosition();
        }
    }};

    // lambda that simulates painting work
    auto paintingRobotTask =
        [&](std::string_view name) {
            // set up random-number generation
            std::random_device rd;
            std::default_random_engine engine{rd()};
            std::uniform_int_distribution<int> ints{2500, 5000};

            // check whether the assembly line is shutting down
            // and, if not, do the painting work
            while (!stopToken.stop_requested()) {
                auto workTime{std::chrono::milliseconds(ints(engine))};

                std::cout << std::format("{} painting for {} ms\n",
                    name, workTime.count());
                std::this_thread::sleep_for(workTime); // simulate work
            }
        };
```

**图 17.15** | 使用 `std::barrier` 对象协调线程。

