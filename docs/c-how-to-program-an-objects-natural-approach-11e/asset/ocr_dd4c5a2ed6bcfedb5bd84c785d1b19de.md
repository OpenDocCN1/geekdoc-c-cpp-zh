```
```cpp
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
```

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
```

Fig. 17.14 | Coordinating threads with a std::latch object. (Part 2 of 3.)