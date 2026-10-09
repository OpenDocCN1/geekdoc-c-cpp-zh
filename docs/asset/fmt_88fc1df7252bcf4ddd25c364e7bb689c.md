
- 类 `shared_mutex` 提供了一个具有共享所有权的非递归互斥锁。
- 类 `shared_mutex` 满足所有共享互斥锁的要求 (`32.5.4.4`)。它是一个布局类 (`11.2`)。
- 如果发生以下情况，程序的行为是未定义的：
    - `(3.1)` 它销毁了任何线程拥有的 `shared_mutex` 对象，
    - `(3.2)` 一个线程尝试递归地获取 `shared_mutex` 的任何所有权，
    - `(3.3)` 一个线程在持有 `shared_mutex` 的所有权时终止。
- `shared_mutex` 可以是 `shared_timed_mutex` 的别名。

## 32.5.4.5 共享定时互斥锁类型

### 32.5.4.5.1 通用

标准库类型 `type_timed_mutex` 是一种共享定时互斥锁类型。共享定时互斥锁满足定时互斥锁类型 (`32.5.4.3`)、`共享互斥锁类型` (`32.5.4.4`) 的要求，并额外满足下面列出的要求。在此描述中，共享定时互斥锁类型的对象 `rel_type` 表示 `time_point` (`27.5`) 的实例化对象，`abs_time` 表示 `time_point` (`27.5`) 的实例化对象。

表达式 `m.lock_shared_for(rel_time)` 返回并具有以下语义：

- 前提条件：调用线程不拥有该互斥锁的所有权。
- 影响：尝试在 `rel_time` 指定的相对时间 (`32.2.4`) 内为线程获取锁所有权。如果时间 `rel_time` 小于或等于 `rel_time.zero()`，函数将返回超时且不阻塞（就像 `try_lock_shared()` 仅在拥有互斥锁共享所有权时才返回 `true` 一样）。

> [注意1：对于 `try_lock()`，如果锁可用但不保证能获得所有权，但实现预计将尽力这样做。结束注]

如果抛出异常，则未为当前线程获取锁。

- 返回类型：`bool`。
- 返回：如果获取了锁则返回 `true`，否则返回 `false`。
- 同步：如果 `try_lock_shared_for()` 返回 `true`，则之前的 `unlock()` 操作在同一对象上与描述中的 (`6.9.2`)同步。
- 抛出：与超时相关的异常 (`32.2.4`)。

表达式 `m.try_lock_shared_until(abs_time)` 是合法的并具有以下语义：

- 前提条件：调用线程不拥有该互斥锁的所有权。
- 影响：函数尝试获取互斥锁的共享所有权。如果 `abs_time` 已经过去，函数尝试在不阻塞的情况下获取共享所有权（如果通过调用 `try_lock_shared()`）。只有当它拥有互斥锁对象的共享所有权时，函数才像通过 `abs_time` 一样返回绝对超时 (`32.2.4`)。

> [注意：对于 `try_lock()`，如果锁可用但不保证能获得所有权，但实现预计将尽力这样做。结束注]

如果抛出异常，则未为当前线程获取共享锁。

- 返回：`bool`
- 返回：如果获取了共享锁则返回 `true`，否则返回 `false`。
- 同步：如果 `try_lock_shared_until()` 返回 `true`，则在同一对象上的之前的 `unlock()` 操作与此操作同步 (`6.9.2`)。
- 抛出：与超时相关的异常 (`32.2.4`)。

## 32.5.4.5 类 `shared_timed_mutex`

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
    void unlock();
    template<class Rep, class Period>
    bool lock_for(const chrono::duration<Rep, Period>& rel_time);
    template<class Clock, class Duration>
    bool lock_until(const chrono::time_point<Clock, Duration>& abs_time);
    // 共享所有权
    void lock_shared();
    bool try_lock_shared();
    void unlock_shared();
    template<class Rep, class Period>
    bool try_lock_shared_for(const chrono::duration<Rep, Period>& rel_time);
    template<class Clock, class Duration>
    bool try_lock_shared_until(const chrono::time_point<Clock, Duration>& abs_time);
};
}
```

- `shared_timed_mutex` 提供了一个具有共享所有权的非递归互斥锁。
- `shared_timed_mutex` 满足所有定时互斥锁的要求 (`32.5.4.3`)。
- 如果发生以下情况，程序的行为是未定义的：
    - `(3.1)` 它销毁了任何线程拥有的 `shared_timed_mutex` 对象，
    - `(3.2)` 一个线程尝试递归地获取 `shared_timed_mutex` 的任何所有权，
    - `(3.3)` 一个线程在持有 `shared_timed_mutex` 的所有权时终止。

## 32.5.5 Locks

### 32.5.5.1 通用

一个引用可互斥锁对象的类型，它在离开作用域时管理所有权，以异常安全的方式释放可互斥锁。该对象在构造期间管理所有权，行为是 (`6.7.3`)。该对象在作用域结束时释放可互斥锁，具有所有权。

> 注意 1：为了释放可互斥锁，构造函数在异常情况下可能不会管理所有权。结束注

某些构造函数在构造期间期间不管理所有权。

```cpp
namespace std {
    struct defer_lock { };
    struct try_lock { };
    struct adopt_lock { };
}
```

### 32.5.5.2 `lock_guard`

```cpp
namespace std {
    template<class Mutex>
    class lock_guard {
    public:
        using mutex_type = Mutex;
        explicit lock_guard(mutex_type& m);
        lock_guard(mutex_type& m, std_lock_t);
        ~lock_guard();
        lock_guard(const lock_guard&) = delete;
        lock_guard& operator=(const lock_guard&) = delete;
    private:
        mutex_type& pm;
    };
}
```

- `lock_guard` 实例在作用域内管理可互斥锁的所有权。`lock_guard` 在其整个生命周期内管理可互斥锁 (`6.7.3`)。提供的互斥锁满足 `BasicLockable` 要求 (`32.2.5.2`)。
- `explicit lock_guard(mutex_type& m);`
- 前提条件：如果 `mutex_type` 不是递归的，调用线程不拥有相应的互斥锁元素 `m`。
- 影响：初始化 `pm`。调用 `lock()`。
- `lock_guard(mutex_type& m, std_lock_t);`
- 前提条件：调用线程拥有互斥锁 `m`。
- 影响：初始化 `pm`。
- `~lock_guard();`
- 影响：像通过 `pm` 一样调用 `unlock()`。

### 32.5.5.3 模板类 `scoped_lock`

```cpp
namespace std {
    template<class... MutexTypes>
    class scoped_lock {
    public:
        using mutex = MutexTypes; 
        explicit scoped_lock(MutexTypes&... m);
        explicit scoped_lock(adopt_lock_t, MutexTypes&... m);
        ~scoped_lock();
        scoped_lock(const scoped_lock&) = delete;
        scoped_lock& operator=(const scoped_lock&) = delete;
    private:
        std::tuple<MutexTypes&...> m;
    };
}
```

- `scoped_lock` 实例在作用域内管理可互斥锁的所有权。`scoped_lock` 在其整个生命周期内管理可互斥锁 (`6.7.3`)。如果 `sizeof...(MutexTypes)` 为 `1`，提供的互斥锁满足 `BasicLockable` 要求 (`32.2.5.2`)。否则，每个互斥锁类型必须满足 `Lockable` 要求 (`32.2.5.3`)。
- `explicit scoped_lock(MutexTypes&... m);`
- 前提条件：如果某个 `Mutex` 类型不是递归的，调用线程不拥有对应的互斥锁元素 `m`。
- 影响：初始化 `tie(m...)`。如果 `sizeof...(Types)` 为 `0`，则无影响。否则如果 `sizeof...(MutexTypes)` 为 `1`，调用 `lock(m)... lock(m...)`。
- `explicit scoped_lock(adopt_lock_t, MutexTypes&... m);`
- 前提条件：调用线程拥有 `m` 中所有的互斥锁。
- 影响：初始化 `tie(m...)`。
- `~scoped_lock();`
- 影响：对于所有 `i` 在 `[0, sizeof...(MutexTypes)]`，调用 `get(pm).unlock()`。

# ISO/IEC 14882:2020(E)

```cpp
unique_lock(const unique_lock&) = delete;
unique_lock operator=(const unique_lock&) = delete;
```

```cpp
unique_lock(unique_lock& u) noexcept;
unique_lock& operator=(unique_lock& u);
```

```cpp
// 32.5.4.3, locking
void lock();
bool lock();
```

```cpp
template<class Rep, class Period>
bool try_lock(const chrono::duration<Rep, Period>& rel_time);
template<class Clock, class Duration>
bool try_lock_until(const chrono::time_point<Clock, Duration>& abs_time);
```

```cpp
void unlock();
```

```cpp
// 32.5.5.4, modifiers
void swap(unique_lock& u) noexcept;
mutex_type* release() noexcept;
```

```cpp
// 32.5.5.5, observers
bool owns_lock() const noexcept;
explicit operator bool() const noexcept;
mutex_type* mutex() const noexcept;
```

```cpp
private:
mutex_type* m_; // 仅用于说明
bool owns_; // 仅用于说明
};
```

```cpp
template<class Mutex>
void swap(unique_lock<Mutex>& x, unique_lock<Mutex>& y) noexcept;
```

`unique_lock` 类型的对象在作用范围内控制可锁对象（lockable object）的所有权。可锁对象的所有权可以在构造时或构造后获取，并可以转移或赋值给另一个 `unique_lock`。`unique_lock` 类型的对象不可移动的。如果包含的指针不为空且由 `pm` 指向的锁在 `unique_lock` 对象的剩余寿命内（`6.3.7`）不再存在，则行为是未定义的。提供的互斥必须满足 `Cpp1Lockable` 要求（`32.2.5.3`）。

> [注意] `unique_lock` 满足 `Cpp1Lockable` 要求（`32.2.5.3`），`unique_lock` 也满足 `Cpp1Lockable` 要求；如果互斥满足 `Cpp1TimedLockable` 要求（`32.2.5.4`），则 `unique_lock` 也满足 `Cpp1TimedLockable` 要求。结束注

## 32.5.5.4.2 构造函数、析构函数和赋值 [thread.lock.unique.com]

```cpp
unique_lock() noexcept;
```

- 后置条件：`pm == 0` 且 `owns == false`。

`explicit unique_lock(mutex_type& m);`

- 前置条件：如果 `mutex_type` 不是递归互斥，则调用线程拥有该互斥。
- 效果：调用 `m.lock()`。
- 后置条件：`pm == addressof(m)` 且 `owns == true`。

```cpp
unique_lock(mutex_type& m, defer_lock_t) noexcept;
```

- 后置条件：`pm == addressof(m)` 且 `owns == false`。

```cpp
unique_lock(mutex_type& m, try_lock_t);
```

- 前置条件：提供的互斥满足 `Cpp1Lockable` 要求（`32.2.5.3`）。如果 `mutex_type` 不是递归互斥，则调用线程拥有该互斥。
- 效果：调用 `m.try_lock()`。
- 后置条件：`pm == addressof(m)` 且 `owns == res`，其中 `res` 是 `m.try_lock()` 的返回值。

```cpp
unique_lock(mutex_type& m, adopt_lock_t);
```

- 前置条件：调用线程拥有该互斥。
- 后置条件：`pm == addressof(m)` 且 `owns == true`。
- 异常：无。

```cpp
template<class Class, class Duration>
unique_lock(mutex_type& m, const chrono::time_point<Clock, Duration> abs_time);
```

- 前置条件：如果 `mutex_type` 不是递归互斥，则调用线程拥有该互斥。提供的互斥满足 `Cpp17Lockable` 要求（`32.2.5.4`）。
- 效果：调用 `m.try_lock(abs_time)`。
- 后置条件：`pm == addressof(m)` 且 `owns == res`，其中 `res` 是 `m.try_lock(abs_time)` 的返回值。

```cpp
template<class Rep, class Duration>
unique_lock(mutex_type& m, const chrono::duration<Rep, Duration> rel_time);
```

- 前置条件：如果 `mutex_type` 不是递归互斥，则调用线程拥有该互斥。提供的互斥满足 `Cpp17Lockable` 要求（`32.2.5.4`）。
- 效果：调用 `m.try_lock(rel_time)`。
- 后置条件：`pm == addressof(m)` 且 `owns == res`，其中 `res` 是 `m.try_lock(rel_time)` 的返回值。

```cpp
unique_lock& operator=(unique_lock&&) noexcept;
```

- 后置条件：`u.pm == u_pm` 且 `owns == u_pm`（其中 `u_pm` 是 `u` 赋值前的状态），`u.pm == 0` 且 `owns == false`。

```cpp
unique_lock& operator=(unique_lock&&)();
```

- 效果：调用 `pm->unlock()`。
- 后置条件：`u.pm == u_pm` 且 `owns == u_pm`（其中 `u_pm` 是 `u` 赋值前的状态），`u.pm == 0` 且 `owns == false`。
[注意：对于递归互斥，赋值前 `*this` 可能已经拥有该互斥。在这种情况下，赋值后 `*this` 将拥有该互斥]
- 异常：无。

```cpp
unique_lock();
```

- 效果：调用 `pm->unlock()`。

## 32.2.5.4 锁定 [thread.lock.unique]

```cpp
void lock();
```
