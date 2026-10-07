# 7.5 Atomic Operation and Model      CHAPTER 07 PARALLELISM AND CONCURRENCY

2. Release/consumption model: In this model, we begin to limit the order of operations between processes. If a thread needs to modify a value, but another thread has a dependency on that operation of the value, that is, the latter depends. Specifically, A has completed three writes to x, and B releases only on the third write operation, regardless of the first two writes of x, A when calling x.release() (ie use std::memory_order_release), the option std::memory_order_consume ensures that B observes when calling x.load()) Three writes to x. Let's look at an example:

```
// initialize as nullptr to prevent consumer load a dangling pointer
std::atomic<int*> ptr(nullptr);
int v;
std::thread producer([&]() {
    int* p = new int(42);
    ptr.store(p, std::memory_order_release);
});

std::thread consumer([&]() {
    int* p;
    while (!(p = ptr.load(std::memory_order_consume))) {
        std::cout << "x: " << *p << std::endl;
        std::cout << "y: " << v << std::endl;
    }
});

producer.join();
consumer.join();
```

3. Release/Acquire model: Under this model, we can further tighten the order of atomic operations between different threads, specifically specifying the timing between releasing std::memory_order_acquire and getting std::memory_order_acquire. All writes before the release operation are visible to any other thread, ie, happens-before.

As you can see, std::memory_order_release ensures that the write behavior does not occur before the release operation, which is a forward barrier, std::memory_order_acquire ensures that its previous write behavior does not occur after this acquisition operation, which is a backward barrier. For the std::memory_order_acq_rel option, it combines the characteristics of two and defines a memory barrier, so that the current thread's reading and writing of memory will not be rearranged before and after this operation.

Let's check out an example:

```
std::vector<int> v;
std::atomic<int> flag = {0};
std::thread release([&]() {
    v.push_back(42);
    flag.store(1, std::memory_order_release);
});
```