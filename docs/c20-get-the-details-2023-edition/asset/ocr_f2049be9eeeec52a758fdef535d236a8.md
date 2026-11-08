A value of type `std::atomic_flag`⁴ is a kind of atomic boolean. It has a cleared and set state. For simplicity reasons, I call the clear state `false` and the set state `true`. The `clear()` member function enables you to set its value to `false`. With the `test_and_set()` member function, you can set the value to `true` and get the previous value. There is no member function to ask for the current value. This will change with C++20 because `std::atomic_flag` has a `test()` method.

Furthermore, `std::atomic_flag` can be used for thread synchronization via the member functions `notify_one()`, `notify_all()`, and `wait()`. With C++20, notifying and waiting are available on all partial and full specializations of `std::atomic` and `std::atomic_ref`. Specializations are available for bools, integrals, floats, and pointers.

# ### 3.4.2 Semaphores

Semaphores are a synchronization mechanism used to control concurrent access to a shared resource. A counting semaphore, such as the one which was added in C++20, is a special semaphore whose initial counter is bigger than zero. The counter is initialized in the constructor. Acquiring the semaphore decreases the counter, and releasing the semaphore increases the counter. If a thread tries to acquire the semaphore when the counter is zero, the thread blocks until another thread increments the counter by releasing the semaphore.

# ### 3.4.3 Latches and Barriers

Latches and barriers are straightforward thread synchronization mechanisms that enable some threads to block until a counter becomes zero. What are the differences between these two mechanisms to synchronize threads? You can use a `std::latch` only once, but you can use a `std::barrier` more than once. A `std::latch` is useful for managing one task by multiple threads; a `std::barrier` is useful for managing repeated tasks by multiple threads. Furthermore, a `std::barrier` can adjust the counter in each iteration.

The following is based on a code snippet from proposal N4204⁵. I fixed a few typos and reformatted it.

**Thread synchronization with a `std::latch`**

```
```
void DoWork(threadpool* pool) {

  std::latch completion_latch(NTASKS);
  for (int i = 0; i < NTASKS; ++i) {
    pool->add_task([&] {
      // perform work

      completion_latch.count_down();
    });
```
```

⁴ https://en.cppreference.com/w/cpp/atomic/atomic_flag

⁵ http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4204.html