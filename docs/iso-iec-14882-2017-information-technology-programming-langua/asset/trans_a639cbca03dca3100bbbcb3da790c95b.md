

# ISO/IEC 14882:2017(E)

相同的互斥锁，观察到它不再被使用，在线程 A 似乎从其 `unlock` 调用返回之前，进行 `unlock`、`unlock` 并销毁。实现要求正确处理此类场景，只要线程在 `unlock` 调用返回后不再访问该互斥锁。这些情况发生在引用计数对象包含一个用于保护引用计数的互斥锁时。—— 尾注

+ 3 `mutex` 类应满足所有的互斥锁要求 (33.4.3)。它应该是一个标准布局类（第 12 own）。

> [ 注意：如果拥有 `mutex` 对象的线程对该对象调用 `lock()`，则程序可能会死锁。如果实现能够检测到死锁，可能会观察到 `resource_deadlock_would_occur` 错误条件。—— 尾注]

+ 5 如果销毁了任何线程拥有的 `mutex` 对象，或在拥有 `mutex` 对象时终止，则程序的行为是未定义的。

## 33.4.3.2 Class recursive_mutex

```cpp
namespace std {
    class recursive_mutex {
    public:
        recursive_mutex();
        ~recursive_mutex();

        recursive_mutex(const recursive_mutex&) = delete;
        recursive_mutex& operator=(const recursive_mutex&) = delete;

        void lock();
        bool try_lock() noexcept;
        void unlock();

        using native_handle_type = implementation_defined; // see 33.2.3
        native_handle_type native_handle(); // see 33.2.3
    };
}
```

+ 1 `recursive_mutex` 类提供了具有排斥所有权语义的 `recursive_mutex`。如果一个线程拥有 `recursive_mutex` 对象，尝试获取该对象的所有权将失败（对于 `try_lock()`）或阻塞（对于 `lock()`），直到该线程完全释放所有权。

+ 2 `recursive_mutex` 类应满足所有的互斥锁要求 (33.4.3)。它应该是一个标准布局类（第 12 ）。

+ 3 拥有 `recursive_mutex` 对象的线程可以通过对它调用 `lock()` 或 `try_lock()` 获取额外的所有权层级。单个线程可以获取多少层所有权是不指定的。如果一个线程已经获取了 `recursive_mutex` 对象的最高层所有权，则额外的 `lock()` 调用将失败，额外的 `unlock()` 调用将抛出 `system_error` 异常。线程应为通过 `lock()` 获取的每层所有权调用一次 `unlock()`，并且只有当所有层所有权都释放后，另一个线程才能获取所有权。

+ 4 如果满足以下条件，程序的行为是未定义的：

- (4.1) 它销毁了任何线程拥有的 `recursive_mutex` 对象
- (4.2) 线程在拥有 `recursive_mutex` 对象时终止。

## 33.4.3. Timed mutex types

+ 1 定时互斥锁类型是标准类型 `timed_mutex`、`recursive_timed_mutex` 和 `shared_timed_mutex`。它们应满足下列要求。在此描述中，`m` 表示互斥锁对象，`rel_time` 表示持续时间 `duration` (23.17.5) 的实例化对象，`abs_time` 表示 `time_point` (23.17.6) 的实例化对象。

+ 2 定时互斥锁类型应满足 `TimedLockable` 要求 (33.2.5.4)。

+ 3 表达式 `my.lock_for(rel_time)` 应当是格式良好的，并具有以下语义：

+ 4 如果 `m` 类型为 `timed_mutex` 或 `shared_timed_mutex`，则该调用不拥有互斥锁。

+ 5 影响：函数尝试在 `rel_time` 指定的相对超时 (33.2.4) 内获取互斥锁的所有权。如果 `rel_time` 指定的时间小于或等于 `rel_time.zero()`，则函数尝试在不阻塞的情况下获取所有权（如果通过调用 `try_lock()`）。只有当获取了互斥锁的所有权时，函数才会在 `rel_time` 的超时范围内返回。[注意：与 `try_lock()` 一样，不能保证在所有权可用时一定能获取，但预计实现会尽力为。—— 尾注]

+ 6 返回：`bool`。

+ 7 返回：如果获取了所有权则返回 `true`，否则返回 `false`。

+ 8 同步：如果 `try_lock()` 返回 `true`，则同一对象上的之前的 `unlock()` 操作与此操作同步 (4.7)。

表达式 `my.lock_until(abs_time)` 应当是格式良好的，并具有以下语义：

+ 11 如果 `m` 类型为 `timed_mutex` 或 `shared_timed_mutex`，如果 `abs_time` 已通过，则该调用不拥有互斥锁。

+ 12 影响：函数尝试获取互斥锁的所有权。如果它已经通过，函数尝试在不阻塞的情况下获取所有权（如果通过调用 `try_lock()`）。只有在获取了互斥锁的所有权时，函数才会在 `abs_time` 指定的绝对超时 (33.2.4) 之前返回。[注意：与 `try_lock()` 一样，不能保证在所有权可用时一定能获取，但预计实现会尽力为。—— 尾注]

+ 13 返回：`bool`。

+ 14 返回：如果获取了所有权则返回 `true`，否则返回 `false`。

+ 15 同步：如果 `try_lock()` 返回 `true`，则同一对象上的之前的 `unlock()` 操作与此操作同步 (4.7)。

+ 16 抛出：与超时相关的异常 (33.2.4)。

## 33.4.3.1 Class timed_mutex

```cpp
namespace std {
    class timed_mutex {
public:
    timed_mutex();
    ~timed_mutex();

    timed_mutex(const timed_mutex&) = delete;
    timed_mutex& operator=(const timed_mutex&) = delete;

    void lock(); // 阻塞
    
    template<class Rep, class Period>
    bool lock_for(const std::duration<Rep, Period>& rel_time); 

    template<class Clock, class Duration>
    bool lock_until(const std::chrono::time_point<Clock, Duration>& abs_time);

    bool try_lock(); // 非阻塞

    using native_handle_type = implementation_defined; // see 33.2.3
    native_handle_type native_handle(); // see 33.2.3
};
```

+ 1 `timed_mutex` 类提供了非递归的排斥所有权互斥锁。如果一个线程拥有 `timed_mutex`，另一个线程尝试获取该对象的所有权将失败（对于 `try_lock()`）或阻塞（对于 `lock()`），直到该线程释放所有权。

`timed_mutex` 类应满足所有的互斥锁要求 (33.4.3)。

+ 3 如果满足以下条件，程序的行为是未定义的：

- (3.1) 它销毁了任何线程拥有的 `timed_mutex`
- (3.2) 线程在拥有 `timed_mutex` 对象时对它调用了 `lock()`、`try_lock()`、`lock_for()` 或 `lock_until()`
- (3.3) 线程在拥有 `timed_mutex` 对象时终止。

