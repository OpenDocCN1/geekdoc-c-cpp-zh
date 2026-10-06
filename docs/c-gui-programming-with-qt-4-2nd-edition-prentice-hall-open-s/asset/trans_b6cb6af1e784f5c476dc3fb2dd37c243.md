
例如，每个字节都算作一个资源。在实际应用中，我们可能会操作更大的单元（例如，一次处理 64 或 256 字节），以减少使用信号量带来的开销。

```cpp
void Producer::run()
{
    for (int i = 0; i < DataSize; ++i) {
        freeSpace.acquire();
        buffer[i % BufferSize] = "ACGT"[uint(std::rand()) % 4];
        usedSpace.release();
    }
}
```

在生产者中，每次迭代都从获取一个“空闲”字节开始。如果缓冲区已满了消费者尚未读取的数据，则 `acquire()` 调用将阻塞，直到消费者开始消耗数据。一旦我们获取了该字节，就会向其填充一些随机数据（'A'、'C'、'G' 或 'T'），并将该字节释放为“已使用”状态，这样消费者就可以读取它。

```cpp
void Consumer::run()
{
    for (int i = 0; i < DataSize; ++i) {
        usedSpace.acquire();
        std::cerr << buffer[i % BufferSize];
        freeSpace.release();
    }
    std::cerr << std::endl;
}
```

在消费者中，我们从获取一个“已使用”字节开始。如果缓冲区中没有数据可读，则 `acquire()` 调用将阻塞，直到生产者产生了一些数据。一旦我们获取了该字节，就会将其打印并将该字节释放为“空闲”，使得生产者能够再次向其填充数据。

```cpp
int main()
{
    Producer producer;
    Consumer consumer;
    producer.start();
    consumer.start();
    producer.wait();
    consumer.wait();
    return 0;
}
```

最后，在 `main()` 函数中，我们启动生产者和消费者线程。然后，生产者将“空闲”空间转换为“已使用”空间，而消费者可以将其转换回“空闲”空间。

当我们运行程序时，它会向控制台写入 100000 个随机的 'A'、'C'、'G' 和 'T' 序列并终止。为了真正理解发生了什么，我们可以禁用输出写入，改为而每次消费者读取一个字节时写入 'P'。为了尽可能保持简单，我们可以使用较小的 `DataSize` 和 `BufferSize` 值。

例如，这里有一个 `DataSize` 为 10 且 `BufferSize` 为 4 的可能运行情况：PcPcPcPcPcPcPPcPPCC。在这种情况下，消费者在生产者生成字节后立即读取；两个线程以相同的速度执行。
另一种可能性是生产者在消费者开始读取之前就填满了缓冲区：PPPPPPPPPP。此外还有许多其他可能性。
当我们研究线程的行为并选择合适的调度策略时，信号量为特定系统的线程调度器留了余地。

解决生产者与消费者同步问题的另一种方法是使用 `WaitCondition`（等待条件）和 `Mutex`（互斥锁）。`WaitCondition` 允许在某些条件满足时唤醒其他线程。这比仅使用互斥锁提供了更精确的。为了展示它是如何工作的，我们将使用等待条件重新编写生产者-消费者示例。

```cpp
const int DataSize = 100000;
const int BufferSize = 4096;
char buffer[BufferSize];
```

```cpp
QWaitCondition bufferIsFull;
QWaitCondition bufferIsNotEmpty;
QMutex mutex;
int usedSpace = 0;
```

除了缓冲区，我们还声明了两个 `QWaitCondition`、一个 `QMutex` 以及一个存储缓冲区中“已使用”字节数量的变量。

```cpp
void Producer::run()
{
  for (int i = 0; i < DataSize; ++i) {
    mutex.lock();
    while (usedSpace == BufferSize) {
      bufferIsNotFull.wait(&mutex);
    }
    buffer[i % BufferSize] = "ACGT"[uint(std::rand()) % 4];
    usedSpace++;
    bufferIsNotEmpty.notifyOne();
    mutex.unlock();
  }
}

void Consumer::run()
{
  for (int i = 0; i < DataSize; ++i) {
    mutex.lock();
    while (usedSpace == 0) {
      bufferIsNotEmpty.wait(&mutex);
    }
    std::cerr << buffer[i % BufferSize];
    usedSpace--;
    bufferIsFull.notifyOne();
    mutex.unlock();
  }
}
```
