![](bbox=[0.225, 0.107, 0.775, 0.414])

A `std::barrier` is similar to a `std::latch`.

# ### 3.8.2 `std::barrier`

There are two differences between a `std::latch` and a `std::barrier`. First, you can use a `std::barrier` more than once, and second, you can adjust the counter for the next phase. The counter is set in the constructor of `std::barrier bar`. Calling `bar.arrive()`, `bar.arrive_and_wait()`, and `bar.arrive_and_drop()` decrements the counter in the current phase. Additionally, `bar.arrive_and_drop()` decrements the counter for the next phase. Immediately after the current phase is finished and the counter becomes zero, the so-called completion step starts. In this completion step, a callable is invoked. The `std::barrier` gets its callable in its constructor.

The completion step performs the following steps:

+   1. All threads are blocked.
+   2. An arbitrary thread is unblocked and executes the callable. The callable must not throw and has to be noexcept.
+   3. If the completion step is done, all threads are unblocked.