
- 如果生产者暂时比消费者运行得更快，那么生产者可以把额外的值写入额外的缓冲区单元（如果有可用单元）。这使得生产者即使消费者尚未准备好取走当前正在生产的值，也能保持忙碌。
- 如果消费者暂时比生产者运行得更快，那么消费者可以从缓冲区读取额外的值（如果有）。这使得消费者即使生产者尚未准备好生产额外的值，也能保持忙碌。

即使使用循环缓冲区，生产者线程也可能填满缓冲区，从而迫使生产者等待消费者消费一个值以释放缓冲区中的一个元素。同样，如果缓冲区为空，消费者必须等待生产者生产另一个值。

如果生产者和消费者持续以显著不同的平均速度运行，那么即使是循环缓冲区也不合适：

- 如果消费者总是执行得更快，那么包含一个位置（或少量位置）的缓冲区就足够了。
- 如果生产者平均执行得更快，并且程序不要求生产者等待，那么只有具有“无限”数量位置的缓冲区才能吸收额外的生产。

**软件工程（SE）** 如果它们以大致相同的平均速度执行，循环缓冲区有助于平滑任一线程执行中偶尔加速或减速的影响，并减少等待时间，从而提高性能。

**性能（Perf）** 循环缓冲区的关键在于优化其大小，以在不浪费内存的前提下最小化线程等待时间。如果我们确定生产者经常生产的值比消费者能消费的值多出多达三个，就可以提供至少三个单元的缓冲区来处理额外的生产。缓冲区太小会导致线程等待更久。

## 实现循环缓冲区

图 17.9—17.10 演示了并发生产者和消费者线程通过同步访问循环缓冲区（图 17.9）。我们将循环缓冲区实现为一个包含三个 `int` 元素的数组。消费者仅在数组非空时消费一个值，生产者仅在数组未满时生产一个值。同样，此类临界区中使用的输出语句仅用于演示。

```cpp
1  // Fig. 17.9: CircularBuffer.h
2  // Synchronizing access to a shared three-element circular buffer.
3  #pragma once
4  #include <array>
5  #include <condition_variable>
6  #include <format>
7  #include <mutex>
8  #include <iostream>
9  #include <string>
10 #include <string_view>

using namespace std::string_literals;

class CircularBuffer {
public:
    // place value into m_buffer
    void put(int value) {
        // critical section that requires a lock to modify shared data
        {
            // lock on m_mutex to be able to write to m_buffer
            std::unique_lock dataLock{m_mutex};

            // if no empty locations, wait on condition variable m_cv
            if (m_occupiedCells == m_buffer.size()) {
                std::cout << "Buffer is full. Producer waits.\n\n";

                // wait on the condition variable; the lambda argument
                // ensures that if the thread gets the processor before
                // the m_buffer has open cells, the thread continues waiting
                m_cv.wait(dataLock,
                    [&]{ return m_occupiedCells < m_buffer.size();});
            }

            m_buffer[m_writeIndex] = value; // write to m_buffer
            ++m_occupiedCells; // one more m_buffer cell is occupied
            m_writeIndex = (m_writeIndex + 1) % m_buffer.size();
            displayState(std::format("Producer writes {}", value));
        } // dataLock's destructor releases the lock on m_mutex here

        m_cv.notify_one(); // notify threads waiting to read from m_buffer
    }

    // return value from m_buffer
    int get() {
        int readValue; // will temporarily hold the next value read

        // critical section that requires a lock to modify shared data
        {
            // lock on m_mutex to be able to write to m_buffer
            std::unique_lock dataLock{m_mutex};

            // if no data to read, place thread in waiting state
            if (m_occupiedCells == 0) {
                std::cout << "Buffer is empty. Consumer waits.\n\n";

                // wait on the condition variable; the lambda argument
                // ensures that if the thread gets the processor before
                // there is data in the m_buffer, the thread continues waiting
                m_cv.wait(dataLock, [&](){ return m_occupiedCells > 0;});
            }

            readValue = m_buffer[m_readIndex]; // read value from m_buffer
            m_readIndex = (m_readIndex + 1) % m_buffer.size();
            --m_occupiedCells; // one fewer m_buffer cells is occupied
            displayState(std::format("Consumer reads {}", readValue));
        } // dataLock's destructor releases the lock on m_mutex here

        m_cv.notify_one(); // notify threads waiting to write to m_buffer
        return readValue;
    }

    // display current operation and m_buffer state
    void displayState(std::string_view operation) const {
        std::string s;

        // add operation argument and number of occupied m_buffer cells
        s += std::format("{} (buffer cells occupied: {}) {:<15}",
            operation, m_occupiedCells, "buffer cells:");

        // add values in m_buffer
        for (int value : m_buffer) {
            s += std::format(" {:2d} ", value);
        }

        s += std::format("\n{:<15}", ""); // padding

        // add underlines
        for (int i{0}; i < m_buffer.size(); ++i) {
            s += "-----";
        }

        s += std::format("\n{:<15}", ""); // padding

        for (int i{0}; i < m_buffer.size(); ++i) {
            s += std::format("  {}{}  ",
                (i == m_writeIndex ? 'W' : '-'),
                (i == m_readIndex ? 'R' : '-'));
        }

        s += "\n\n";
        std::cout << s; // display the state string
    }

private:
    std::condition_variable m_cv;
    std::mutex m_mutex;

    std::array<int, 3> m_buffer{-1, -1, -1}; // shared m_buffer
    int m_occupiedCells{0}; // number of buffers used
    int m_writeIndex{0}; // index of next element to write to
    int m_readIndex{0}; // index of next element to read
};
```

**图 17.9** | 同步访问共享的三元素循环缓冲区。

### 数据成员

第104—110行定义类的数据成员：

- 第104—105行定义 `std::condition_variable` `m_cv` 和 `std::mutex` `m_mutex`，用于同步对 `CircularBuffer` 其他数据成员的访问。
- 第107行创建并初始化三元素 `int` 数组 `m_buffer`，表示循环缓冲区。
- 变量 `m_occupiedCells`（第108行）统计包含可读数据的 `m_buffer` 元素数量。当 `m_occupiedCells` 为0时，循环缓冲区为空，消费者必须等待。当 `m_occupiedCells` 为3（缓冲区大小）时，循环缓冲区已满，生产者必须等待。
- 变量 `m_writeIndex`（第109行）指示生产者可以放置下一个值的位置。
- 变量 `m_readIndex`（第110行）指示消费者可以读取下一个值的位置。

数据成员 `m_buffer`、`m_occupiedCells`、`m_writeIndex` 和 `m_readIndex` 都属于类的共享可变数据，因此必须同步对这些变量的访问，以确保 `CircularBuffer` 是线程安全的。

### CircularBuffer 函数 put

`put` 函数（第17—41行）执行与图17.7相同的任务，但有几处修改。第24—32行检查 `CircularBuffer` 是否已满。如果已满，生产者必须等待，因此第25行表明生产者正在等待执行其任务。然后，第30—31行调用 `m_cv` 的 `wait` 函数，使生产者线程释放 `m_mutex` 的锁，并等待缓冲区中有空间写入新值。

当执行在第34行继续时，生产者将一个值放入循环缓冲区中 `m_writeIndex` 位置。第35行递增 `m_occupiedCells`，因为缓冲区包含一个消费者可以读取的值。然后第36行更新 `m_writeIndex`，供生产者下一次调用 put 使用。这一行是缓冲区循环性的关键。当 `m_writeIndex` 递增超过缓冲区末尾时，这一行将其重置为0。接下来，第37行调用 `displayState`（第73—102行）显示生产者写入的值、`m_occupiedCells` 计数、各单元内容以及当前的 `m_writeIndex` 和 `m_readIndex`。到达第38行的代码块末尾会释放 `m_mutex` 的锁。第40行在 `m_cv` 上调用 `notify_one`，将一个等待线程转换为就绪状态，以便正在等待的消费者线程（如果有）现在可以再次尝试从缓冲区读取值。

### CircularBuffer 函数 get

`get` 函数（第44—70行）执行与图17.7相同的任务，但有几处细微修改。第53—60行（图17.9）判断所有缓冲区单元是否为空，在这种情况下消费者必须等待。如果是，第54行更新输出以表明消费者正在等待执行其任务。然后第59行调用 `m_cv` 的 `wait` 函数，使消费者线程释放 `m_mutex` 的锁，并等待有可读取的数据。

当执行在第62行继续时，局部变量 `readValue` 被赋值为 `m_buffer` 中 `m_readIndex` 位置的值。然后第63行更新 `m_readIndex`，供下一次调用 `CircularBuffer` 函数 `get` 使用。这一行和第36行实现了缓冲区的循环-
