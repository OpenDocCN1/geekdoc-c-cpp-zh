+   - Sequential consistency: `memory_order_seq_cst`
+   - Acquire-release: `memory_order_consume`, `memory_order_acquire`, `memory_order_release`, and `memory_order_acq_rel`
+   - Relaxed: `memory_order_relaxed`

While the sequential consistency establishes a global order between threads, the acquire-release semantic establishes an ordering between reading and writing operations on the same atomic variable with different threads. The relaxed semantic only guarantees the modification order of some atomic m. Modification order means that all modifications on a particular atomic m occur in some particular total order. Consequently, a particular thread reads of an atomic object never see "older" values than those the thread has already observed.

The different memory models and their effects on atomic and non-atomic operations make the C++ memory model an exciting and challenging topic. Let us discuss the synchronization and ordering constraints of the sequential consistency, the acquire-release semantic, and the relaxed semantic.

# ## 2.4.2 Sequential Consistency

Let us dive deeper into sequential consistency. The key to sequential consistency is that all operations on all threads obey a universal clock. This global clock makes it quite intuitive to think about it.

The intuitiveness of the sequential consistency comes with a price. The downside is that the system has to synchronize threads.

The following program synchronizes the producer and the consumer thread with the help of sequential consistency.

**Producer-Consumer synchronization with sequential consistency**

```
    1 // producerConsumer.cpp
    2
    3 #include <atomic>
    4 #include <iostream>
    5 #include <string>
    6 #include <thread>
    7
    8 std::string work;
    9 std::atomic<bool> ready(false);
    10
    11 void consumer() {
    12   while (!ready.load()) {}
    13   std::cout << work << '\n';
    14 }
    15
    16 void producer() {
    17   work = "done";
```