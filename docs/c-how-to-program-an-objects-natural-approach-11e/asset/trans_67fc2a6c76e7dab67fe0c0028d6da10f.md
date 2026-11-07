
循环性。第 64 行将 m_occupiedCells 递减，因为现在有一个空闲的缓冲区位置，生产者可以在其中放置一个值。第 65 行用正在被消费的值、occupiedCells 计数、各单元格的内容以及当前的 m_writeIndex 和 m_readIndex 更新输出。到达第 66 行时释放 m_mutex 的锁。第 68 行调用 m_cv 的 notify_one 函数，以允许正在等待的生产者线程醒来再次写入。然后第 69 行将消费的值返回给调用者。

## CircularBuffer 函数 displayState

函数 displayState（第 73–102 行）构建并输出一个包含应用程序状态的字符串。第 81–83 行将缓冲区各单元格的值添加到字符串中，对每个单元格的内容使用“:2d”格式说明符；如果是一位数字，则前面加一个空格。第 94–98 行分别用字母 W 和 R 将当前的 m_writeIndex 和 m_readIndex 添加到字符串中。注意，我们仅从临界区调用此函数，以确保线程安全。同样，我们不应在临界区中进行 I/O——我们这样做只是为了生成有用的输出用于演示目的。

## 测试类 CircularBuffer

图 17.10 包含启动应用程序的 main 函数。第 13 行创建一个名为 buffer 的 CircularBuffer 对象，第 14 行显示 buffer 的初始状态。第 17–37 行和第 40–60 行创建 produce 和 consume 这两个 lambda，并发生产者线程和消费者线程将执行它们。第 62–63 行创建调用 produce 和 consume 这两个 lambda 的 std::jthreads。当 main 结束时，std::jthreads 离开作用域，自动 join 这些线程。

```cpp
// Fig. 17.10: SharedBufferTest.cpp
// Concurrent threads manipulating a synchronized circular buffer.
#include <chrono>
#include <format>
#include <iostream>
#include <mutex>
#include <random>
#include <thread>
#include "CircularBuffer.h"

int main() {
    // create CircularBuffer to store ints and display initial state
    CircularBuffer buffer;
    buffer.displayState("Initial State");

    // lambda expression that produces the values 1-10 and sums them
    auto produce{
        [&buffer]() {
            // set up random-number generation
            std::random_device rd;
            std::default_random_engine engine{rd()};
            std::uniform_int_distribution<int> ints{0, 3000};

            int sum{0};

            for (int count{}; count <= 10; ++count) {
                // get random sleep time in this sleep
                std::chrono::milliseconds sleepTime{ints(engine)};
                std::this_thread::sleep_for(sleepTime);

                buffer.put(count); // set value in buffer
                sum += count; // add count to sum of values produced
            }

            std::cout << "Producer done producing\nTerminating Producer\n\n";
        }
    };

    // lambda expression that consumes the values 1-10 and sums them
    auto consume{
        [&buffer]() {
            // set up random-number generation
            std::random_device rd;
            std::default_random_engine engine{rd()};
            std::uniform_int_distribution<int> ints{0, 3000};

            int sum{};

            for (int count{}; count <= 10; ++count) {
                // get random sleep time in this sleep
                std::chrono::milliseconds sleepTime{ints(engine)};
                std::this_thread::sleep_for(sleepTime);

                sum += buffer.get(); // get buffer value and add to sum
            }

            std::cout << std::format("{} {}\n{}",
                "Consumer read values totaling", sum, "Terminating Consumer");
        }
    };

    std::jthread producer{produce}; // start producer thread
    std::jthread consumer{consume}; // start consumer thread
}
```

```text
Initial State (buffer cells occupied: 0)
buffer cells:   -1  -1  -1
                --- --- ---
                    W

Buffer is empty. Consumer waits.

Producer writes 1 (buffer cells occupied: 1)
buffer cells:    1  -1  -1
                --- --- ---
                  R   W

Consumer reads 1 (buffer cells occupied: 0)
buffer cells:   1   -1   -1
                ---  ---  ---
                 WR

Buffer is empty. Consumer waits.

Producer writes 2 (buffer cells occupied: 1)
buffer cells:   1    2   -1
                ---  ---  ---
                 R    W

Consumer reads 2 (buffer cells occupied: 0)
buffer cells:   1    2   -1
                ---  ---  ---
                      WR

Buffer is empty. Consumer waits.

Producer writes 3 (buffer cells occupied: 1)
buffer cells:   1    2    3
                ---  ---  ---
                 W         R

Consumer reads 3 (buffer cells occupied: 0)
buffer cells:   1    2    3
                ---  ---  ---
                      WR

Producer writes 4 (buffer cells occupied: 1)
buffer cells:   4    2    3
                ---  ---  ---
                 R    W

Producer writes 5 (buffer cells occupied: 2)
buffer cells:   4    5    3
                ---  ---  ---
                 R         W

Consumer reads 4 (buffer cells occupied: 1)
buffer cells:   4    5    3
                ---  ---  ---
                      R    W

Consumer reads 5 (buffer cells occupied: 0)
buffer cells:   4    5    3
                ---  ---  ---
                      WR

Producer writes 6 (buffer cells occupied: 1)
buffer cells:   4    5    6
                ---  ---  ---
                 W         R

Producer writes 7 (buffer cells occupied: 2)
buffer cells:    7    5    6
                 ---  ---  ---
                        W    R

Producer writes 8 (buffer cells occupied: 3)
buffer cells:    7    8    6
                 ---  ---  ---
                            WR

Buffer is full. Producer waits.

Consumer reads 6 (buffer cells occupied: 2)
buffer cells:    7    8    6
                 ---  ---  ---
                   R        W

Producer writes 9 (buffer cells occupied: 3)
buffer cells:    7    8    9
                 ---  ---  ---
                        WR

Buffer is full. Producer waits.

Consumer reads 7 (buffer cells occupied: 2)
buffer cells:    7    8    9
                 ---  ---  ---
                   W    R

Producer writes 10 (buffer cells occupied: 3)
buffer cells:    10   8    9
                 ---  ---  ---
                            WR

Producer done producing
Terminating Producer

Consumer reads 8 (buffer cells occupied: 2)
buffer cells:    10   8    9
                 ---  ---  ---
                        W    R

Consumer reads 9 (buffer cells occupied: 1)
buffer cells:    10   8    9
                 ---  ---  ---
                        R    W

Consumer reads 10 (buffer cells occupied: 0)
buffer cells:    10   8    9
                 ---  ---  ---
                            WR

Consumer read values totaling 55
Terminating Consumer
```

**图 17.10** | 并发线程操作一个同步的循环缓冲区。

### 分析输出

当生产者写入一个值或消费者读取一个值时，程序会输出一条消息，指示所执行的操作、`m_buffer` 的内容以及 `m_writeIndex`（`"W"`）和 `m_readIndex`（`"R"`）的位置。在示例输出中，消费者立即等待，因为它在生产者执行之前就尝试消费。接下来，生产者写入 `1`。随后缓冲区在第一个单元格中包含 `1`，在另外两个单元格中包含 `-1`（我们为输出目的使用的默认值）。写索引现在位于第二个单元格，而读索引仍位于第一个单元格。接下来，消费者读取 `1`。缓冲区包含相同的值，但读索引现在位于第二个单元格。然后消费者尝试再次读取，但缓冲区为空，消费者必须等待。消费者在读取 `2` 后也会等待。在输出的后面，生产者两次填满缓冲区，并随后每次都等待。

## 17.8 读者与写者

我们的生产者-消费者示例使用单个生产者和单个消费者——这在许多使用线程共享可变数据的应用程序中很常见。有些系统需要多个读取数据的消费者线程（称为读者）和多个写入数据的生产者线程（称为写者）。这被称为读者与写者问题。

例如，在航空订票系统中，读者可能远多于写者。在客户实际购买某趟航班上的某个座位之前，会对可用航班信息数据库进行许多查询。关键观察是，如果有多个读者，它们**可以同时读取**，而不会出现线程安全问题，因为它们不修改数据。写者仍然需要独占访问修改数据的临界区——不能有其他写者，也不能有读者。

支持多个读者和写者的 C++ 特性是 `std::shared_mutex`、`std::shared_lock` 和 `std::condition_variable_any`。一个 `std::shared_mutex`<sup>63</sup>（来自 `<mutex>` 头文件）允许一个写者或多个读者拥有其锁：

- 如果锁可用，写者通过 `lock_guard` 或 `unique_lock` 获取它。否则，写者被**阻塞**，必须等待锁变为可用。当写者持有 `shared_mutex` 的锁时，其他任何线程都不能获取该锁。
- 如果锁可用，读者通过 `std::shared_lock`<sup>64</sup>（来自 `<mutex>` 头文件）获取它；否则，读者被阻塞，必须等待锁变为可用。当读者持有 `shared_mutex` 的锁时，只有其他读者可以获取该锁。

正如在我们同步的生产者-消费者示例中那样，我们必须确保读者和写者只在轮到它们时执行任务：

- 如果写者到达时有读者正在读取，写者必须等待锁变为可用。此外，随后到达的任何其他读者都必须等待当前正在写入的写者执行完毕并通知它们写入已完成。如果允许源源不断到达的读者进行读取，等待的写者将被**无限期推迟**。

63. `std::shared_mutex`。访问日期：2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/thread/shared_mutex。
64. `std::shared_lock`。访问日期：2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/thread/shared_lock。
