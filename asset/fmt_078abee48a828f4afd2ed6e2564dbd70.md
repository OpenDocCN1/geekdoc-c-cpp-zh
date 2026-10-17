
```cpp
    // 32.6.5.3. 可中断等待 [thread.condvar]
    template<class Lock>
    void wait(Lock& lock);
    template<class Lock, class Predicate>
    void wait(Lock& lock, Predicate pred);

    template<class Lock, class Clock, class Duration>
    cv_wait_until(Lock& lock, const chrono::time_point<Clock, Duration>& abs_time);
    template<class Lock, class Rep, class Period>
    cv_wait_for(Lock& lock, const chrono::duration<Rep, Period>& rel_time);

    template<class Lock, class Clock, class Duration, class Predicate>
    bool wait_until(Lock& lock, const chrono::time_point<Clock, Duration>& abs_time, Predicate pred);
    template<class Lock, class Rep, class Period, class Predicate>
    bool wait_for(Lock& lock, const chrono::duration<Rep, Period>& rel_time, Predicate pred);
};
condition_variable_any();
```

`notify_one()` 影响：唤醒一个阻塞等待的线程。

`notify_all()` 影响：所有所有阻塞等待的线程。

## 32.6.5.1 不可中断等待 [thread.condvar.wait]

```cpp
template<class Lock>
void wait(unique_lock<Lock>& lock);
```

影响：

- 原子地调用 `lock.unlock()` 并阻塞在此。
- 解阻塞后，调用 `lock.lock()`（可能在锁上）并返回。
- 函数被 `notify_one()`、`notify_all()` 唤醒，或者由于异常。

> 备注：如果函数未能满足条件，将调用 `terminate()` (14.6.2)。

> 注意 2：如果重锁互斥量抛出异常，则可能发生这种情况。

后置条件：`lock` 被调用者锁定。

抛出：无。

```cpp
template<class Lock, class Predicate>
void wait(unique_lock<Lock>& lock, Predicate pred);
```

影响：等价于：

```
while (!pred())
    wait(lock);
```

```cpp
template<class Lock, class Clock, class Duration>
cv_wait_until(unique_lock<Lock>& lock, const chrono::time_point<Clock, Duration>& abs_time);
```

影响：

- 原子地调用 `lock.unlock()` 并阻塞在此。
- 解阻塞后，调用 `lock.lock()`（可能在锁上）并返回。
- 函数被 `notify_one()`、`notify_all()` 唤醒，绝对超时（32.2.4）过期，或者由于异常。

> 如果函数通过异常退出，在退出函数之前会调用 `lock.unlock()`。

> 备注：如果函数未能满足条件，将调用 `terminate()` (14.6.2)。

> 注意 2：如果重锁互斥量抛出异常，则可能发生这种情况。

后置条件：`lock` 被调用者锁定。

返回值：`cv_status`：如果绝对超时（32.2.4）过期，则为 `timeout`；否则 `cv_status:no_timeout`。

抛出：超时相关的异常 (32.2.4)。

```cpp
template<class Lock, class Rep, class Period>
cv_wait_for(unique_lock<Lock>& lock, const chrono::duration<Rep, Period>& rel_time);
```

影响：等价于：

```
return wait_until(lock, chrono::steady_clock::now() + rel_time);
```

返回值：如果指定的 `rel_time` 相对时间（32.2.4）过期，返回 `cv_status::timeout`，否则返回 `cv_status::no_timeout`。

备注：如果函数未能满足后条件，将调用 `terminate()`（14.6.2）。

> [注意 3：如果重新锁定互斥量抛出异常，可能会发生这种情况。 — 脚注结束]

后条件：调用线程持有该锁。

```
template<class Lock, class Clock, class Duration, class Predicate>
bool wait_until(Lock& lock, const chrono::point<Clock, Duration>& abs_time, Predicate pred);
```

等价于：

```
while (pred())
    if (wait_until(lock, abs_time) == cv_status::timeout)
        return pred();
return true;
```

> [注意 4：如果 `pred()` 为真或超时已经过期，则不会阻塞。 — 脚注结束]

> [注意 5：该值表示无论是否触发超时，谓词是否评估为真。 — 脚注结束]

```
template<class Lock, class Rep, class Duration, class Predicate>
bool wait_for(Lock& lock, const chrono::duration<Rep, Period>& rel_time, Predicate pred);
```

等价于：

```
return wait_until(lock, chrono::steady_clock::now() + rel_time, std::move(pred));
```

## 32.6.5.3 可中断的等待

如果在 `stop_token` 上请求了停止，则以下等待将收到通知。如果函数立即返回，且 `pred` 评估为假，则返回 false：

```
template<class Lock, class Predicate>
bool wait(Lock& lock, stop_token token, Predicate pred);
```

影响：在此调用的期间，*此将在在此调用期间收到停止请求的通知，并等价于：

```
while (!token.stop_requested())
    if (pred())
        return true;
    wait(lock);
return pred();
```

> [注意 1：返回的值表示无论是否有停止请求，谓词是否评估为真。 — 脚注结束]

后条件：调用线程持有该锁。

备注：如果函数未能满足后条件，将调用 `terminate`（14.6.2）。

> [注意 2：如果重新锁定互斥量抛出异常，可能会发生这种情况。 — 脚注结束]

影响：由 `pred` 抛出任何异常。

```
template<class Lock, class Clock, class Duration, class Predicate>
bool wait_until(Lock& lock, const chrono::point<Clock, Duration>& abs_time, Predicate pred);
```

影响：在此调用的期间，*此将在在此调用期间收到停止请求的通知，并等价于：

```
while (!token.stop_requested())
    if (pred())
        return true;
    if (wait_until(lock, abs_time) == cv_status::timeout)
        return pred();
return false;
```

> [注意 3：如果 `pred()` 初始为真、`token.stop_requested()` 已经为真或超时已经过期，则不会阻塞。 — 脚注结束]

> [注意 4：返回的值表示无论触发了超时还是发出了停止请求，谓词是否评估为真。 — 脚注结束]

后条件：调用线程锁定了锁。

备注：如果函数在后条件之后失败，将调用 `terminate`（14.6.2）。

[注意 5：如果重新锁定互斥量抛出异常，可能会发生这种情况。 — 脚注结束]

```
Throws：与超时相关的异常 <class Lock, class Rep, class Period, class Predicate>
bool wait_for(Lock& lock, stoken token,
             const chrono::duration<Rep, Period>& rel_time, Predicate pred);
```

等价于：

```
return wait_until(lock, stoken::move(token), chrono::steady_clock::now() + rel_time,
             pred(std));
```

## 32.7 信号量

### 32.7.1 通用

信号量是轻级同步原语，用于限制对共享资源的并发访问。它们被广泛用于实现其他同步原语，在适用情况下，比条件变量更高效。

计数信号量是模拟非负计数器的信号量对象。二进制信号量是只有两种状态的信号量对象。二进制信号量的效率应该高于具有单位计数器的计数信号量的默认实现。

## 32.7.2 头文件<semaphore> 摘要

```
namespace std {
template<ptrdiff_t max_value = implementation-defined>
class counting_semaphore {

    using binary_semaphore = counting_semaphore<1>;
}
```

## 32.7.3 计数 counting_semaphore

```
namespace std {
template<ptrdiff_t max_value = implementation-defined>
class counting_semaphore {
public:
    static constxpr ptrdiff_t max() noexcept;

    constrxpr explicit counting_semaphore(ptrdiff_t desired)
        -counting_semaphore(const counting_semaphore& other);

    counting_semaphore(const counting_semaphore& other) = delete;
    counting_semaphore& operator=(const counting_semaphore& other) = delete;

    void release(ptrdiff_t count = 1) noexcept;
    void acquire() noexcept;
    template<class Rep, class Period>
    bool acquire_for(const chrono::duration<Rep, Period>& rel_time);
    template<class Clock, class Duration>
    bool try_acquire_until(const chrono::time_point<Clock, Duration>& abs_time);

    private:
        ptrdiff_t counter; // 仅用于说明
    };
}; // namespace std
```

ISO/IEC 14882:2020(E)

- 1. `counting_semaphore` 类维护一个内部计数器，在信号量创建时初始化。当线程获取信号量时，计数器减1；当线程释放信号量时，计数器增加。如果线程在计数器为零时尝试获取信号量，该线程将阻塞，直到另一个线程通过信号量增加计数器。
- 2. `least_max_value` 应是非负的；否则程序格式是错误的。
- 3. `counting_semaphore` 成员函数（析构函数外）的并发调用会引入数据竞态。

```
static constexpr ptrdiff_t max() noexcept;
```

返回值：计数器的最大值。该值大于或等于 `least_max_value`。

```
constexpr explicit counting_semaphore(ptrdiff_t desired);
```

前置条件：`desired >= 0` 为真且 `desired <= max()` 为真。

影响：用 `desired` 初始化计数器。

抛出：无。

```
void release(ptrdiff_t update = 1);
```

前置条件：`update >= 0` 为真且 `update <= max() - counter` 为真。

影响：原子性执行 `counter += update`。然后

同步：发生在 `try_acquire` 的调用之前；观察影响的结果。

- 11. 抛出：当需要异常时抛出 `system_error`（32.2.2）。
- 12. 错误条件：允许类型允许的任何错误条件（32.5.4.2）。

```
bool try_acquire() noexcept;
```

影响：尝试减少计数器（如果它为正），且不阻塞。如果计数器没有减1，则立即返回。实现即使计数器为正，也可能无法减1。

> [注意：1：部分失败通常不常见，但它让实现关注简单的比较和交换（第 31 节）。 — 脚注结束]

实现应确保在没有竞争信号量操作的情况下，`try_acquire` 不一致返回 false。

返回值：如果计数器被减则返回 true，否则返回 false。

```
void acquire();
```

15. 影响：重复执行以下步骤：
- (15.1) 评估 `try_acquire`。如果结果为真，则返回。
- (15.2) 阻塞直到计数器大于零。
- 16. 抛出：当需要异常时抛出 `system_error`（32.2.2）。
- 17. 错误条件：类型允许的任何错误条件（32.5.4.2）。

```
template<class Class, class Duration>
bool try_acquire_for(const std::duration<Duration>& rel_time);
template<class Class, class Duration>
bool try_acquire_until(const std::time_point<Clock, Duration>& abs_time);
```

18. 影响：重复执行以下步骤：
- (18.1) 评估 `try_acquire()`。如果结果为真，则返回。
- (18.2) 阻塞直到计数器大于零或超时过期。如果由于超时过期而解除阻塞，则返回 false。

超时过期发生在当前时间到达 `abs_time`（对于 `try_acquire_until`）或从函数开始已经过了至少 `rel_time`（对于 `try_acquire_for`）。

抛出：与超时相关的异常 (32.2.4)，或者在需要非超时相关异常时抛出 `system_error` (32.2.2)。

2. 错误条件：互斥类型检测到的任何错误条件 (32.5.4.2)。

## 32.8 协调类型

### 32.8.1 通用

+ 1 子类 32.8 描述了与线程相关的各种概念，并定义了协调类型 latch（栅栏）和 barrier（屏障）。这些类型通过多个线程促进并发计算。

### 32.8.2 Latches

#### 32.8.2.1 通用

+ 1 latch 是一种线程协调机制，允许任何线程阻塞，直到预期的线程数量到达 latch（通过 `count_down` 函数）。预期计数在创建 latch 时设置。单个 latch 是单次使用的对象；一旦达到预期计数，latch 无法无法重用。

#### 32.8.2.2 Header<latch> 摘要

```cpp
namespace std {
    class latch;
}
```
