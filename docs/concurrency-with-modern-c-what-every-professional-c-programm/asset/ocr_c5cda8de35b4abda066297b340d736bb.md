Let me explain the rest with a graphic.

```
```cpp
void dataProducer() {
    mySharedWork[1, , ,];
    dataProduced.store(true, std::memory_order_release);
}

void deliveryBoy() {
    while(!dataProduced.load(std::memory_order_acquire)) ;
    dataConsumed.store(true, std::memory_order_release);
}

void dataConsumer() {
    while(!dataConsumed.load(std::memory_order_acquire)) ;
    mySharedWork[1] == 2;
}
```
```

Transitivity of the acquire-release semantic

The essential parts of the picture are the arrows.

+   * The **blue** arrows are the *sequenced-before* relations. This means that all operations in one thread are executed in source code order.
+   * The **red** arrows are the *synchronizes-with* relations. The reason is the acquire-release semantic of the atomic operations on the same atomic. The synchronization between the atomics, and therefore between the threads happen at specific points.
+   * *sequenced-before* establishes a *happens-before* and *synchronizes-with* a *inter-thread happens-before* relation.

The rest is pretty simple. The *happens-before* and *inter-thread happens-before* order of the instructions correspond to the arrows' direction from top to bottom. Finally, we guarantee that `mySharedWork[1] == 2` is executed last.

A release operation *synchronizes-with* an acquire operation on the same atomic variable, so we can easily synchronize threads, if ... . The typical misunderstanding is about the if.

# 2.4.3.2 The Typical Misunderstanding

What is my motivation for writing about the typical misunderstanding of the acquire-release semantic? Many of my readers and students have already fallen into this trap. Let's look at the straightforward case.

# 2.4.3.2.1 Waiting Included

Here is a simple program as a starting point.