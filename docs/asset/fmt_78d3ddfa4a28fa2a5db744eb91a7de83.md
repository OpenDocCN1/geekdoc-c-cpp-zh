
影响：`pm->lock_shared()`。
后置条件：`owns == true`。
抛出：任何由 `pm->shared_lock(30.2.2)` 抛出的异常。如果 `pm` 为 `nullptr`，则抛出错误条件为 `operation_not_permitted` 的 `system_error`；如果 `owns` 为真，则抛出错误条件为 `resource_deadlock_would_occur` 的 `system_error`。

`bool try_lock();`
影响：`pm->try_lock_shared()`。
返回：调用 `pm->try_lock_shared()` 返回的值。
后置条件：`owns == res`，其中 `res` 是调用 `pm->try_lock_shared()` 返回的值。
抛出：任何由 `pm->shared_lock(30.2.2)`（注：此处原文可能有误应为try_lock_shared） 抛出的异常。`system_error`。如果 `pm` 为 `nullptr`，则抛出错误条件为 `operation_not_permitted` 的 `system_error`；如果 `owns` 为真，则抛出错误条件为 `resource_deadlock_would_occur` 的 `system_error`。

```cpp
template <class Lock, class Duration>
```

```cpp
bool try_lock_until(chrono::time_point<chrono::Clock, Duration>& abs_time);
```

影响：`pm->try_lock_shared_until(abs_time)`。

返回：调用 `pm->try_lock_shared_until(abs_time)` 返回的值。

后置条件：`owns == res`，其中 `res` 是调用 `pm->try_lock_shared_until(abs_time)` 返回的值。

抛出：任何由 `pm->shared_lock(30.2.2)` 抛出的异常。`system_error`。如果 `pm` 为 `nullptr`，则抛出错误条件为 `operation_not_permitted` 的 `system_error`；如果 `owns` 为真，则抛出错误条件为 `resource_deadlock_would_occur` 的 `system_error`。

```cpp
template <class Rep, class Period>
```

```cpp
bool try_lock_for(chrono::duration<Rep, Period>& rel_time);
```

影响：`pm->try_lock_shared_for(rel_time)`。
返回：调用 `pm->try_lock_shared_for(rel_time)` 返回的值。
后置条件：`owns == res`，其中 `res` 是调用 `pm->try_lock_shared_for(rel_time)` 返回的值。
抛出：任何由 `pm->shared_lock(30.2.2)` 抛出的异常。`system_error`。如果 `pm` 为 `nullptr`，则抛出错误条件为 `operation_not_permitted` 的 `system_error`；如果 `owns` 为真，则抛出错误条件为 `resource_deadlock_would_occur` 的 `system_error`。

```cpp
void unlock();
```

影响：`pm->unlock_shared()`。
后置条件：`owns == false`。

## 30.4.2.3.3 shared_lock 修改器

> [thread.shared]

```cpp
void swap(shared_lock& u) noexcept;
```

影响：交换 `this` 的数据成员。

```cpp
mutex_type* release() noexcept;
```

返回：之前的 `pm` 值。
后置条件：`pm == nullptr` 且 `owns == false`。

## 30.4.2.3.4 shared_lock 观察者

> [thread.shared]

`bool owns_lock() const noexcept;`
返回：`owns`。

`explicit operator bool() const noexcept;`
返回：`owns`。

`mutex_type* mutex() const noexcept;`
返回：`pm`。

## 30.4.3 通用锁定算法

[thread.lock]

`template <class L1, class L2, class L3> int try_lock(L1&, L2&, L3&);`
要求：每个模板参数类型均满足 `Lockable` 的要求。[注意：`unique_lock` 类模板在实例化时必须满足这些要求。 — 注意结束]
影响：从第一个参数开始顺序调用每个参数 `try_lock()`，直到所有参数处理完毕或 `try_lock()` 失败（通过返回 false 或抛出异常）。如果 `try_lock()` 调用失败，则应对所有已锁定的参数调用 `unlock()`。
返回：如果所有 `try_lock()` 调用均返回 true，否则返回指示 `try_lock` 返回 false 的参数的零基索引值。

`template <class L1, class L2, class... L3> void lock(L1&, L2&, L3&);`
要求：每个模板参数类型均满足 `Lockable` 的要求。[注意：`unique_lock` 类模板在实例化时必须满足这些要求。 — 注意结束]
影响：通过对每个参数调用 `lock()`、`try_lock()` 或 `unlock()` 来锁定所有参数。调用序列不应导致死锁，其余另如此。[注意：必须使用尝试并退避（try-and-back-off）的算法，除非特定参数未说明以避免过度竞争。 — 注意结束] 如果 `lock()` 或 `try_lock()` 调用抛出异常，则应对任何被 `lock()` 或 `try_lock()` 锁定的参数调用 `unlock()`。

## 30.4.4 调用一次 (Call once)

[thread.once]

`class_once` 是一种不透明的数据结构，`call_once` 使用它在不引起数据竞争或死锁的情况下初始化数据。

## 30.4.4.1 结构体 once_flag

[thread.once.onceflag]

`constexpr once_flag() noexcept;`
影响：构造一个 `once_flag` 对象。
同步：`once_flag` 对象的构造不是同步的。
后置条件：对象的内部状态被设置为指示一个以该对象为初始参数的 `call_once` 尚未被函数调用。

## 30.4.4 函数 call_once

```cpp
template<class Class, ...Args>
void call_once(const Class& flag, Callable&& func, Args&&... args);
```

- 要求：Callable 和 Args 中的每个 Ti 均满足 MoveConstructible 要求。INVOKE(DECAY, DECOPY(std::forward<Callable>(func), DECAY, DECOPY(std::forward<Args>(args))...)) (20.9.2) 必须是一个有效表达式。
- 影响：未调用 func 的 call_once 执行是被动执行。调用了 func 的 call_once 执行是主动执行。主动执行应当调用 INVOKE(DECAY-DECOPY(std::forward<Callable>(func), DECAY, DECOPY(std::forward<Args>(args))...))。如果抛出异常的调用是主动执行，则抛出异常，否则返回。主动执行应当将异常传播给 call_once 的调用者。对于任何给定的 call_flag 的所有 call_once 执行中：最多一个为主动执行；只有当存在一个返回的执行时，才存在被动执行，且该执行是返回的。注意：被动执行与其他线程同步，以可靠地获取由先返回的执行产生的结果。——注释结束
- 同步：对于任何给定的 call_flag：所有主动执行按一个总顺序发生；主动执行的完成与 (1.10) 该总顺序中的下一个执行的开始同步；返回的执行与所有被动执行的返回同步。
- 抛出：当需要异常时抛出 system_error (30.2.2)，或者抛出 func 抛出的任何异常。

```cpp
// flag，普通函数
void init();
std::once_flag flag;
void f() {
    std::call_once(flag, init);
}
// 函数静态静态 flag，函数对象
struct initializer {
    void operator()();
};
void g() {
    static std::once_flag flag2;
    std::call_once(flag2, initializer());
}
// 对象 flag，成员函数
class information {
    std::once_flag verified;
    void verifier();
public:
    void verify() { std::call_once(verified, &information::verifier, *this); }
};
// 示例结束
```

## 30.5 条件变量

- 条件变量提供了同步原语，用于阻塞线程，直到被其他线程通知某个条件已满足，或到达某个系统状态。Class condition_variable 提供了一种只能在 unique_lock<mutex> 类型对象上等待的条件，这在某些平台上可以实现最高效率。Class condition_variable_any 提供了一个通用的条件变量，可以在用户提供的锁类型对象上等待。
- 2 两个条件防止了 wait、wait_for、wait_until、notify_one 以及所有成员函数的并发调用。
- 3 notify_one 和 notify_all 的执行是原子的。wait、wait_for 和 wait_until 的执行之前应先有三个原子部分：
    - 1. 释放互斥锁并进入等待状态；
    - 2. 重新获取锁。
- 4 实现行为应当表现为所有 notify_one、notify_all 的执行以及 wait、wait_for 和 wait_until 执行的每个部分都在一个未指定的总顺序中执行，该顺序与“发生于”（happens-before）顺序一致。
- 5 条件变量的构造和析毁不需要同步。

### Header_condition_variable_synopsis

```cpp
namespace std {
    condition_variable;
    condition_variable_any;
    void notify_all_at_thread_exit(condition_variable& cond, unique_lock<mutex> lk);
    enum class class_status { no_timeout, };
}
```

`void notify_all_at_thread_exit(condition_variable& cond, unique_lock<mutex> lk);`

- 6 要求：lk 被条件和线程锁定
    - (6.1) 没有线程在 cond 上等待，或
    - (6.2) lk.mutex() 返回了每个并发等待（通过 wait、wait_for 或 wait_until）的线程所提供的每个锁参数的值。
- 影响：将与 lk 关联的锁的所有权转移到内部存储，并调度 cond 在当前线程退出时执行，即在所有与当前线程相关的线程存储持续期对象被销毁之后。此通知应满足以下条件：
```cpp
lk.unlock();
cond.unlock();
```
- 8 同步：隐含的 lk.unlock() 在所有与当前线程相关的线程存储持续期对象销毁后被调用。

注意：提供的锁将保持到线程退出为止，并注意确保这不会因锁顺序问题导致死锁。调用 notify_all_at_thread_exit 后，建议尽快退出线程，并且不要在该线程上运行阻塞或耗时的任务。

注意：确保等待的线程在经历虚假唤醒时不会错误地假设线程已完成，是用户的责任。这通常要求在持有 lk 的锁时，所正在等待的条件必须是满足的，并且该锁在调用 notify_all_at_thread_exit 之前不被释放。

## 30.5.1 Class condition_variable

### [thread.condition.condvar]

```cpp
namespace std {
    class condition_variable {
    public:
        condition_variable();
        ~condition_variable();
        condition_variable(const condition_variable&) = delete;
        condition_variable& operator=(const condition_variable&) = delete;
        void notify_one() noexcept;
        void notify_all() noexcept;
        template<class Predicate>
        void wait(unique_lock<mutex>& lock, Predicate pred);
        template<class Clock, class Predicate>
        void wait_for(unique_lock<mutex>& lock, const std::chrono::duration<Clock>& rel, Predicate pred);
        template<class Clock, class Predicate>
        void wait_until(unique_lock<mutex>& lock, const std::chrono::time_point<Clock>& tp, Predicate pred);
        template<class Predicate>
        bool wait(unique_lock<mutex>& lock, Predicate pred);
        template<class Clock, class Predicate>
        bool wait_for(unique_lock<mutex>& lock, const std::chrono::duration<Clock>& rel, Predicate pred);
        template<class Clock, class Predicate>
        bool wait_until(unique_lock<mutex>& lock, const std::chrono::time_point<Clock>& tp, Predicate pred);
    };
}
```

- 1 condition_variable 应当是标准布局（standard layout）。
- 2 影响：构造一个条件变量。
- 3 抛出：当需要异常时抛出 system_error (30.2.2)。
- 4 析构销毁条件变量。
- 5 要求：析毁不需要同步。
- 6 `notify_one()` 影响：通知其中一个等待的线程。
- 7 `notify_all()` 影响：通知所有等待的线程。
- 8 `wait(unique_lock<mutex>& lock, Predicate pred)`：
    - 原子地释放锁并在条件上阻塞。
    - 被通知时，重新获取锁。
    - 如果谓词为真，则返回。
    - 如果为假，则循环。

# © ISO/IEC N4296

- (19.1) 没有其他线程在等待 condition_variable，或者
- (19.2) lock_mutex() 对于所有并发正在等待（通过 wait、wait_for 或 wait_until）的线程所提供的每个 lock 参数，都返回相同的值。

20 效果：
- (20.1) 原子地调用 `lock.unlock()` 并在 *this* 上阻塞。
- (20.2) 当解除阻塞时，调用 `lock.lock()`（可能在 lock 上加锁），然后返回。
- (20.3) 当通过调用 `notify_one()`、调用 `notify_all()` 或由 `abs_time` 指定的超时 (30.2.4) 到期，或虚假唤醒时，函数将释放锁。
- (20.4) 如果函数通过异常退出，则在进入函数之前应调用 `lock.lock()`。

21 注意：如果函数满足后置条件，则应调用 `terminate()` (15.5.1) [注释：这可能发生在互斥锁重锁时。—— 注释]

22 后置条件：`lock.owns_lock()` 为真，且 `lock.mutex()` 被调用线程锁定。

23 返回：如果 `abs_time` 指定的超时 (30.2.4) 到期，则 `cv_status=timeout`，否则返回 `cv_status=no_timeout`。

24 抛出：超时相关的异常 (30.2.4)。

```cpp
```
