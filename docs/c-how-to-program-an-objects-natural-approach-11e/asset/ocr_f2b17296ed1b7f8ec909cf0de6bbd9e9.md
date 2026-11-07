```
```cpp
 1  // Fig. 17.8: SharedBufferTest.cpp
 2  // Concurrent threads correctly manipulating a synchronized buffer.
 3  #include <chrono>
 4  #include <format>
 5  #include <iostream>
 6  #include <mutex>
 7  #include <random>
 8  #include <thread>
 9  #include "SynchronizedBuffer.h"
10
11 int main() {
12     // set up random-number generation
13     std::random_device rd;
14     std::default_random_engine engine(rd());
15     std::uniform_int_distribution ints{0, 3000};
16     std::mutex intsMutex;
17
18     // lambda for synchronized random sleep time generation
19     auto getSleepTime{
20         [&]() {
21             std::lock_guard lock{intsMutex};
22             return std::chrono::milliseconds{ints(engine)};
23         }
24     };
25
26     // create SynchronizedBuffer to store ints
27     SynchronizedBuffer buffer;
28
29     // lambda expression that produces the values 1-10 and sums them
30     auto produce{
31         [&buffer, &getSleepTime]() {
32             int sum{};
33
34             for (int count{1}; count <= 10; ++count) {
35                 // get random sleep time then sleep
36                 std::this_thread::sleep_for(getSleepTime());
37
38                 buffer.put(count); // set value in buffer
39                 sum += count; // add count to sum of values produced
40             }
41
42             std::cout << "Producer done producing\nTerminating Producer\n";
43         }
44     };
45
46     // lambda expression that consumes the values 1-10 and sums them
47     auto consume{
48         [&buffer, &getSleepTime]() {
49             int sum{};
50
```
```

Fig. 17.8 | Concurrent threads correctly manipulating a synchronized buffer. (Part 1 of 3.)