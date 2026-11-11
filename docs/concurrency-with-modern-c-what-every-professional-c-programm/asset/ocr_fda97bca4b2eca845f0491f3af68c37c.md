# ### 7.2.2.1 Disadvantages

The already mentioned document gives an excellent description of the deficiencies of the futures.

# #### 7.2.2.1.1 future/promise Should Not Be Coupled to std::thread Execution Agents

C++11 had only one executor std::thread. Consequently, futures and std::thread were inseparable. This changed with C++17 and the parallel algorithms of the STL. This changes even more with the new executors, which you can use to configure the future. For example, the future may run in a separate thread, in a thread pool, or sequentially.

# #### 7.2.2.1.2 Where are then Continuations are Invoked?

Imagine you have a simple continuation, such as in the following example.

**Continuations with std::future**

```
~~~cpp
future<int> f1 = async([]() { return 123; });
future<string> f2 = f1.then([](future<int> f) {
    return to_string(f.get());
});
~~~
```

The question is: Where should the continuation run? There are a few possibilities today:

+   1. Consumer Side: The consumer execution agent always executes the continuation.
+   2. Producer Side: The producer execution agent always executes the continuation.
+   3. inline_executor semantics: If the shared state is ready when the continuation is set, the consumer thread executes the continuation. If the shared state is not ready when the continuation is set, the producer thread executes the continuation.
+   4. thread_executor semantics: A new std::thread executes the continuation.

In particular, the first two possibilities have a significant drawback: they block. In the first case, the consumer blocks until the producer is ready. In the second case, the producer blocks, until the consumer is ready.

Here are a few nice use-cases of executor propagation from the document P0701r1¹¹:

11)http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0701r1.html