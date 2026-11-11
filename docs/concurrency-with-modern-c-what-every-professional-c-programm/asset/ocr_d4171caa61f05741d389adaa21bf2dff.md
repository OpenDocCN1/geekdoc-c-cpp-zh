If you call the constructor of std::unique_lock with std::defer_lock, the underlying mutex is not locked automatically. At this point (lines 16 and 21), the std::unique_lock is just the mutex owner. Thanks to the variadic template std::lock, the lock operation is performed in an atomic step (line 25).

In this example, std::unique_lock manages the lifetime of the resources and std::lock locks the associated mutex. You can do it the other way around. In the first step, the mutexes are locked. In the second std::unique_lock manages the lifetime of resources. Here is an example of the second approach.

```
```cpp
std::lock(a.mut, b.mut);
std::lock_guard<std::mutex> guard1(a.mut, std::adopt_lock);
std::lock_guard<std::mutex> guard2(b.mut, std::adopt_lock);
```
```

Both variants resolve the deadlock.

![](bbox=[0.27, 0.44, 0.74, 0.665])

Deadlock resolved with std::unique_lock