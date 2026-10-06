

# ISO/IEC 14882:2017(E)

template <class L1, class L2, class L3> void lock(L1&, L2&, L3&);

要求: 每个模板参数类型都应满足 Lockable 要求，[注：unique_lock 类模板在实例化时满足这些要求。—注结束]；

影响: 所有参数都通过对参数调用 lock()`、`try_lock()` 和 `unlock()` 的序列被锁定。调用序列不应导致死锁，除非另有规定。[注：必须使用诸如 try-and-back 之类的死锁避免算法，但未指定具体算法以避免对实现产生过度限制。—注结束] 如果调用 lock() 或 `try_lock()` 抛出异常，则应对任何已通过 lock() 或 `try_lock()` 锁定的参数调用 `unlock()`。

## 33.4.6 只调用一次 [thread.once]

### 33.4.6.1 结构 once_flag [thread.once.once_flag]

```cpp
namespace std {
    struct once_flag;
    constexpr once_flag(const once_flag&) = delete;
    once_flag& operator=(const once_flag&) = delete;
};
```

+   1 once_flag 是一个不透明的数据结构，call_once 用于初始化数据，而不会引起数据竞态或死锁。

constexpr once_flag() noexcept;

+   2 影响: 构建一个类型为 once_flag 对象。

+   3 同步: once_flag 对象的构造不是同步的。

+   4 后置条件: 对象的内部状态被设置为指示：作为初始参数的 call_once 尚未被调用，且尚没有函数被调用。

## 33.4.6.2 函数 call_once [thread.once.callonce]

```cpp
template<class Callable, class... Args>
void call_once(once_flag& flag, Callable&& f, Args&&... args);
```

+   1 要求:
   INVOKE(forward<Callable>(f), forward<Args>(args)...) 
   (23.14.3) 应当是一个有效表达式。

+   2 影响: 一个未调用 func 的 call_once 执行是被动执行。call_once(forward<Callable>(f), forward<Args>(args)...) 的执行是主动执行。如果此类调用抛出异常，则该执行是异常的，否则是返回。异常执行会将异常传播给 call_once 的调用者。对于任何 once_flag 的所有 call_once 执行后：最多应有一个是返回执行；如果存在返回执行，它应当是最后一次主动执行；并且存在被动执行。被动执行允许其他线程可靠地观察由先前的执行产生的结果.—注结束

+   3 同步: 对于任何给定的 once_flag，所有主动执行都发生在一个总顺序中；主动执行的完成与 (4.7) 该顺序中下一个执行的开始同步；返回执行与从所有被动执行的返回同步。

 4 抛出: 当需要异常时抛出 system_error (33.2.2)，或 func 抛出的任何异常。

 5 [示例:

```cpp
// 全局标记，普通标记
void init(){
std::once_flag flag;
}

void f(){
std::call_once(flag, init);
}

// 静态标记，函数对象
struct initializer {
void operator()();
};

void g(){
static std::call_once(flag2, initializer());
}

// 对象标记，成员函数
class information {
std::once_flag verified;
void verifier();
public:
void verifier() { std::call_once(verified, &information::verifier, *this); }
};

```

## 33.5 条件变量

+   1 条件变量提供了同步原语，用于阻塞线程，直到被其他某个线程通知某个条件已满足，或者只等待直到某个系统时间到达。condition_variable 类提供了一个只能在类型为 unique_lock<mutex> 的对象上等待的条件变量。condition_variable_any 提供了一个通用条件变量，可以在用户提供的类型的对象上等待。

+   2 条件变量允许并发调用 wait、wait_for、wait_until、notify_one 和 notify_all 成员函数。

+   3 notify_one 和 notify_all 的执行应该是原子的。wait、wait_for 和 wait_until 的执行应分三个原子部分执行：
1 释放互斥锁并进入等待状态；
2 解除 wait 的阻塞；
3 重新获取锁。

+   4 实现行为应当类似于所有 notify_one、notify_all 以及每个 wait、wait_for 和 wait_until 执行的每个部分都在一个未指定的顺序中执行，且该顺序与“发生于”（happens before）顺序一致。

+   5 条件变量的构造和析构不需要同步。

## 33.5.1 头文件 <condition_variable> 概要

```cpp
namespace std {
    class condition_variable;
    class condition_variable_any;

    void notify_all_thread_exit(condition_variable& cond, unique_lock<mutex> lk);
    enum class condition_status { no, timeout };}

## 33.5.2 成员函数

```cpp
void notify_all_thread_exit(condition_variable& cond, unique_lock<mutex> lk);
```

+   1 要求:
   lk 已经被调用线程锁定且
   - 没有任何其他线程在 cond 上等待或
   - wait, wait_for 或 wait_until 的执行。

+2 影响: 转移 l l 的所有权到调用线程，
   - lk 线程释放并导致 wait, wait_for 或 wait_until 的执行。

+3 同步: lk 释放在调用 notify_all_thread_exit 之后。

+4 异常:
   (4.1) resource_unavailable_try — 如果某些内存资源限制阻止初始化。

+5 要求: 不有线程在 *this 上阻塞。 | 注: 也就是说，所有线程都已被通知；它们随后可能在锁上阻塞。这放宽了通常规则，即必须在析构之前发生。用户应该确保 wait 在当等待线程在循环中调用 wait 或使用 wait、wait_for 或 wait_until 的重载时，在 *this 之前发生。

## 33.5.3 类 condition_variable

```cpp
namespace std {
    class condition_variable {
    public:
        condition_variable();
        ~condition_variable();

        condition_variable(const condition_variable&) = delete;
        condition_variable& operator=(const condition_variable&) = delete;

        notify_one() noexcept;
        notify_all() noexcept;
        wait(unique_lock<mutex>& lk);
        template <class Pred>
        wait(unique_lock<mutex>& lk, pred);
        template <class Clock, class Duration>
        condition_status wait_until(unique_lock<mutex>& lk, time_point<Clock, Duration>& abs_time);
}

template <class Clock, class Duration, class Predicate>
bool wait_until(unique_lock<mutex>& lk, time_point<Clock, Duration>& abs_time, pred);

template <class Rep, class Period>
bool wait_for(unique_lock<mutex>& lk, duration<Rep, Period>& rel_time);

using native_handle_type = implementation-defined; // sec 32.3
native_handle_type native_handle(); // sec 32.3
}
```

+1 condition_variable 类应该是标准布局（第 12 节）。

+2 condition_variable();

+2 影响: 构建一个类型为 condition_variable 对象。

+3 抛出: 当需要异常时抛出 system_error (33.2.2)。

+4 错误条件:

   (4.1) resource_unavailable_try — 如果某些内存资源限制阻止初始化。

+-condition_variable();

+5 要求: 不有线程在 *this 上阻塞。 | 注: 也就是说，所有线程都已被通知；它们随后可能在锁上阻塞。这放宽了通常规则，即必须在析构之前发生。用户应该确保 wait 在析构之前发生。特别是当等待线程在循环中调用 wait 或使用 wait、wait_for 或 wait_until 的重载直到一个谓词、一个周期，且不

+6 影响: 析毁对象。

```cpp
void notify_one() noexcept;
```

+7 影响: 如果有线程在 *this 上阻塞，则唤醒其中一个线程。

```cpp
void notify_all() noexcept;
```

+8 影响: 唤醒所有在 *this 上阻塞的线程。

```cpp
void wait(unique_lock<mutex>& lk);
```

+9 要求: lock.owns_lock() 为 true 且 lock.mutex() 被调用线程锁定，并且要么

   (9.1) 没有其他线程在当前 condition_variable 对象上等待，或者

   (9.2) lock.mutex() 对于所有并发等待（通过 wait、wait_for 或 wait_until）的线程提供的每个参数返回相同的值。

+10

+ 影响:

   (10.1) 原子地释放 locks.unlock() 并阻塞在 *this 上。

