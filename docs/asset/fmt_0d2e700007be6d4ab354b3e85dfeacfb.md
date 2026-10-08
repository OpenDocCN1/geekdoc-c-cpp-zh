
## Header <shared_mutex> 摘要

## 30.4.1 互斥锁要求

本节提供了互斥的机制：互斥锁（`mutexes`）、锁（`locks`）和一次调用（`call once`）。这些机制使得无冲突程序 (1.10)可用。

## 30.4.1.1 一般

本节提供了互斥的机制：互斥锁（`mutexes`）、锁（`locks`）和一次调用（`call once`）。这些机制使得无冲突程序 (1.10)可用。

## 30.4.1.2 互斥锁类型

本节提供了互斥的机制：互斥锁（`mutexes`）、锁（`locks`）和一次调用（`call once`）。这些机制使得无冲突程序 (1.10)可用。

## 30.4.1.2.1 类 mutex 类

```cpp
namespace std {
    class mutex {
    public:
        constexpr mutex() noexcept;
        ~mutex();
        mutex(const mutex&) = delete;
        operator=(const mutex&) = delete;
        void lock();
        bool try_lock();
        void unlock();
        typedef implementation-defined native_handle_type; // See 30.2.3
        native_handle_type native_handle(); // See 30.2.3
    };
```

`mutex` 类提供了另一种具有排他所有权语义的非递归互斥锁。如果一个线程拥有一个 `mutex` 对象，另一个尝试获取该对象所有权的线程将失败（`try_lock()`）或阻塞（`lock()`），直到该线程通过调用 `unlock()`释放所有权。

> [注意：在线程 A 调用 `unlock()` 释放互斥锁后，另一个线程 B 可能在线程 A 似乎从其 `unlock` 调用返回之前，锁定同一个不再使用的互斥锁，对其调用 `unlock()` 并将其销毁。实现要求必须正确处理此类场景，因为线程 A 在 `unlock` 调用后不再访问该互斥锁。这些情况通常发生在使用引用计数对象保护资源时。]

`mutex` 类应满足所有要求 (30.4.1)。它应该是标准布局（第 9 章）。

> [注意：如果拥有 `mutex` 对象的线程对该对象调用 `lock()`，程序可能会发生死锁。如果实现能够检测到死锁，可能会观察到 `deadlock_would_occur` 错误状态。]

如果销毁了由任何线程拥有的 `mutex`，或者线程在持有该对象时终止，则程序的行为是未定义的。

## 30.4.1.2.2 类 recursive_mutex 类

```cpp
namespace std {
    class recursive_mutex {
    public:
        recursive_mutex();
        ~recursive_mutex();
        recursive_mutex(const recursive_mutex&) = delete;
        recursive_mutex& operator=(const recursive_mutex&) = delete;
        void lock();
        bool try_lock();
        void unlock();
        typedef implementation-defined native_handle_type; // See 30.2.3
        native_handle_type native_handle(); // See 30.2.3
    };
```

`recursive_mutex` 类提供了具有排他所有权语义的递归互斥锁。如果一个线程拥有一个 `recursive_mutex` 对象，另一个尝试获取该对象所有权的线程将失败（`try_lock()`）或阻塞（`lock()`），直到第一个线程释放所有权。

`recursive_mutex` 类应满足所有要求 (30.4.1)。它应该是标准布局（第 9 章）。

拥有 `recursive_mutex` 对象的线程可以通过对该对象调用 `lock()` 或 `try_lock()` 获取额外的所有权层级。单个线程可以获取多少层所有权是不未指定的。如果线程已经获取了 `recursive_mutex` 对象的最大所有权层级，额外的 `try_lock()` 调用将失败，额外的 `lock()` 调用将抛出 `system_error` 类型的异常。线程应为通过调用 `lock` 和 `try_lock` 获取的每一层所有权调用一次 `unlock()`。只有当所有层所有权都已释放后，另一个线程才能获取所有权。

在以下情况下，互斥锁的行为是未定义的：
- (1) 它销毁了任何线程拥有的 `recursive_mutex` 对象
- (2) 线程在持有 `recursive_mutex` 时终止

## 30.4.1.3 计时互斥锁类型

计时互斥锁类型是标准库类型：`timed_mutex`、`recursive_timed_mutex` 和 `std::shared_timed_mutex`。它们应满足下面列出的要求。在描述中，`mutex` 表示类型该类型的对象，`rel_time` 表示持续时间的实例 (30.12.5)，`abs_time` 表示 `time_point` 类型的对象 (30.12.6)。

计时互斥锁应满足 `Lockable` 要求 (30.2.5)。

如果调用线程不拥有该互斥锁，表达式 `m.try_lock_for(rel_time)` 应该是良法的。

> [注意：如果 `m` 是 `std::timed_mutex` 或 `std::shared_timed_mutex` 类型，则调用线程不拥有该互斥锁。函数尝试在 `rel_time` 指定的相对时间 (30.2.4) 内获取互斥锁的所有权。如果 `rel_time` 指定的时间小于或等于 `rel_time.zero()`，则函数尝试在不阻塞的情况下获取所有权（如同调用 `try_lock()`）。只有仅在获取了互斥锁对象的所有权时，才会返回 `rel_time` 指定的超时。[注意：与 `try_lock()` 一样，不保证所有权一定可用，但预计实现会尽力做到。]

返回类型：`bool`

返回：如果获取了所有权则返回 `true`，否则返回 `false`。

同步：如果 `try_lock_for()` 返回 `true`，则在该对象上之前的 `unlock()` 操作与其同步 (11.10)。

抛出：与超时相关的异常 (30.2.4)。

表达式 `m.try_lock_until(abs_time)` 应该是良法的且具有以下语义：调用线程不拥有该互斥锁。

> [注意：如果 `m` 是 `std::timed_mutex` 或 `std::shared_timed_mutex` 类型，则调用线程尝试获取互斥锁的所有权。如果 `abs_time` 已经过去，则函数尝试在不阻塞的情况下获取所有权（如同调用 `try_lock()`）。只有仅在获取了互斥锁对象的所有权时，函数会在 `abs_time` 指定的绝对超时 (30.2.4) 之前返回。[注意：与 `try_lock()` 一样，如果锁可用但不保证能获取所有权，但预计实现会尽力做到。]

返回类型：`bool`

返回：如果获取了所有权则返回 `true`，否则返回 `false`。

同步：如果 `try_lock_until()` 返回 `true`，则在该对象上之前的 `unlock()` 操作与其同步 (1.10)。

抛出：超时异常 (30.2.4)。

## 30.4.1.3.1 类 timed_mutex 类

```cpp
namespace std {
class timed_mutex {
public:
    timed_mutex();
    ~timed_mutex();
    timed_mutex(const timed_mutex&) = delete;
    timed_mutex& operator=(const timed_mutex&) = delete;
    void lock(); // blocking
    bool try_lock();
    template<class Rep, class Period>
    bool try_lock_for(const std::duration<Rep, Period>& rel_time);
    template<class Clock, typename Period>
    bool try_lock_until(const std::time_point<Clock, Period>& abs_time);
    void unlock();
    typedef implementation-defined native_handle_type;
    native_handle_type native_handle();
};
```

直到其他执行代理释放了调用线程，使得共享锁的数量减少到最大值以下。

### 3 表达式 `m.lock_shared()` 应当是良的并具有以下语义：

- 要求：调用线程不拥有该互斥锁的所有权。
- 影响：阻塞调用线程，直到为调用线程获取该互斥锁的所有权。如果抛出异常，则当前线程未获取共享锁。
- 后置条件：调用线程拥有该互斥锁的共享锁。
- 返回类型：`void`。
- 同步：之前在同一对象上进行的 `unlock()` 操作应与 (1.10) 操作同步。
- 抛出：当需要发生异常时抛出 `system_error` (30.2.2)。
- 错误条件：
    - `operation_not_permitted` — 如果线程没有执行该操作的权限。
    - `resource_deadlock_would_occur` — 如果实现检测到会导致死锁。
    - `device_or_resource_busy` — 如果已经锁定且无法进行阻塞。

### 表达式 `m.unlock()` 应当是良的并具有以下语义：
（注：此处 OCR 乱码，但上下文暗示了 unlock 的语义）

### 表达式 `m.unlock()` 应当是良的并具有以下语义：

- 要求：调用线程应持有对该互斥锁的锁。
- 影响：释放调用线程对互斥锁的锁。
- 返回类型：`void`。
- 同步：此操作与后续在同一对象上获取所有权的 (1.10) `lock()` 操作同步。
- 抛出：无。

### 表达式 `m.try_lock_shared()` 应当是良的并具有以下语义：

- 要求：调用线程不拥有该互斥锁的所有权。
- 影响：尝试在不阻塞的情况下为调用线程获取互斥锁的共享所有权。如果没有获取共享所有权，则没有影响且 `try_lock_shared()` 立即返回。如果锁未被任何其他线程持有，实现可能会无法获取锁。
- 返回类型：`bool`。
- 返回：如果获取了共享锁则返回 true，否则返回 false。
- 同步：如果 `try_lock_shared()` 返回 true，之前在同一对象上进行的 `unlock()` 操作与 (1.10) 同。
- 抛出：无。

### 表达式 `m.try_lock_shared_for(rel_time)` 应当是良的并具有以下语义：

- 要求：调用线程应在 `rel_time` 指定的相对超时(30.2.4) 内为调用线程锁定锁所有权。如果由 `rel_time` 指定的时间小于或等于 `rel_time.zero()`，则函数尝试在不阻塞的情况下获取所有权（如同通过调用 `try_lock_shared()`）。该函数仅当在 `rel_time` 指定的超时时间内返回，且前提是它已经获取了所有权；如果锁可用将获得所有权，但预计实现会努力这样做。 — 结语。如果抛出异常，则当前线程未获取共享锁。
- 返回类型：`bool`。
- 返回：如果获取了共享锁则返回 true，否则返回 false。
- 同步：如果 `try_lock_for()` 返回 true，之前在同一对象上进行的 `unlock()` 操作与 (1.10) 此操作同步。
- 抛出：超时相关的异常 (30.2.4)。

### 表达式 `m.try_lock_shared_until(abs_time)` 应当是良的并具有以下语义：

- 要求：调用线程不拥有该互斥锁的所有权。如果 `abs_time` 已经过去，函数尝试在不阻塞的情况下获取互斥锁的共享所有权（如同通过调用 `try_lock_shared()`）。该函数仅当已拥有该互斥锁对象的共享所有权时，才会返回 `abs_time` 指定的绝对超时(30.2.4)。[注：使用 `try_lock()`，不能保证在锁可用时一定获取所有权，但预计实现会努力这样做。 — 结语]如果抛出异常，则当前线程未获取共享锁。
- 返回类型：`void`。
- 返回：如果获取了共享锁则返回 true，否则返回 false。（注：此处原文逻辑与返回类型可能存在冲突，已按原文翻译）
- 同步：如果 `try_lock_shared_until()` 返回 true，之前在同一对象上进行的 `unlock()` 操作与 (1.10) 此操作同步。
- 抛出：超时相关的异常 (30.2.4)。

## 30.4.1.4. 类 shared_timed_mutex

```cpp
namespace std {
class shared_timed_mutex {
public:
    shared_timed_mutex();
    ~shared_timed_mutex();
    shared_timed_mutex(const shared_timed_mutex&) = delete;
    shared_timed_mutex& operator=(const shared_timed_mutex&) = delete;
    // 独斥所有权
    void lock();
    bool try_lock();
    template<class Rep, class Period>
    bool try_lock_for(const chrono::duration<Rep, Period>& rel_time);
    template<class Clock, class Duration>
    bool try_lock_until(const chrono::time_point<Clock, Duration>& abs_time);
    void unlock();
    // 共享所有权
    void lock_shared(); // 阻塞
    bool try_lock_shared();
    template<class Rep, class Period>
    bool lock_shared_for(const chrono::duration<Rep, Period>& rel_time);
    template<class Clock, class Duration>
    void lock_shared_until(const chrono::time_point<Clock, Duration>& abs_time);
};
```

1. `shared_timed_mutex` 非递归互斥锁。
2. `shared_timed_mutex` 满足 `SharedMutex` 需求 (30.4.1)。它是 `BasicLockable` 类 (30.2.5)。
3. 在以下情况下 `shared_timed_mutex` 的行为是未定义的：
    - (1) 销毁 `shared_timed_mutex` 对象，
    - (2) 线程尝试获取所有权，或
    - (3) 线程在持有 `shared_timed_mutex` 时终止。

1. `lock_guard` 在生命周期内管理可锁对象的所有权，在正常和异常情况下均如此。

## 30.4.2.1. 类 lock_guard

```cpp
namespace std {
template <class Mutex>
class lock_guard {
public:
    Mutex mutex_type;
    lock_guard(Mutex& m);
    lock_guard(Mutex& m, std::lock_t);
    lock_guard();
    lock_guard(const lock_guard&) = delete;
    lock_guard& operator=(const lock_guard&) = delete;
private:
    Mutex& m;
};
}
```

1. `lock_guard` 在生命周期内管理可锁对象的所有权 (30.8)。提供的互斥锁必须满足 `BasicLockable` 需求。
2. `lock_guard(Mutex& m)`：
    - 如果 `Mutex` 不是递归互斥锁，则调用线程不拥有互斥锁。
    - 影响：调用 `m.lock()`。
    - 后置条件：`m == &`。
3. `lock_guard(Mutex& m, std::lock_t)`：
    - 调用线程拥有互斥锁 `m`。
    - 后置条件：`m == &`。
4. `~lock_guard()`：
    - 影响：调用 `m.unlock()`。

## 30.4.2.2. 模板类 unique_lock

（注：原文文本在此处中断，未提供后续具体内容）

# ©ISO/IEC N4296

```cpp
template <class Rep, class Period>
```
