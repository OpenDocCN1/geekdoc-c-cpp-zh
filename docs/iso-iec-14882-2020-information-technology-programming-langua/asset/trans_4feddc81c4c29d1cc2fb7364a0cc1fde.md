

该操作是对该内存的原子加载操作，并且 `expected` 会在尝试的原子更新中，用从原子对象读取的现有值进行更新。对应于写入 `expected` 的 `use_count` 更新是原子操作的一部分。对 `expected` 本身的写入不要求是原子操作的一部分。

```
bool compare_exchange_weak(weak_ptr<T>& expected, weak_ptr<T> desired,
    memory_order order = memory_order::seq_cst) noexcept;
```

效果：等价于：

```
return compare_exchange_weak(expected, desired, order, fail_order);
```

其中 `fail_order` 与 `order` 相同，但 `memory_order::acq_rel` 的值应替换为 `memory_order::acquire` 的值，`memory_order::release` 的值应替换为 `memory_order::relaxed` 的值。

```
bool compare_exchange_strong(weak_ptr<T>& expected, weak_ptr<T> desired,
    memory_order order = memory_order::seq_cst) noexcept;
```

效果：等价于：

```
return compare_exchange_strong(expected, desired, order, fail_order);
```

其中 `fail_order` 与 `order` 相同，但 `memory_order::acq_rel` 的值应替换为 `memory_order::acquire` 的值，`memory_order::release` 的值应替换为 `memory_order::relaxed` 的值。

```
void wait(weak_ptr<T> old, memory_order order = memory_order::seq_cst) const noexcept;
```

前置条件：`order` 既不是 `memory_order::release` 也不是 `memory_order::acq_rel`。

效果：按顺序重复执行以下步骤：

+   — 计算 `load(order)` 并将其与 `old` 进行比较。
+   — 如果两者不相等，则返回。
+   — 阻塞，直到被原子通知操作解除阻塞，或被虚假唤醒。

备注：如果两个 `weak_ptr` 对象存储相同的指针，并且要么共享所有权，要么都为空，则它们等价。此函数是一个原子等待操作（31.6）。

```
void notify_one() noexcept;
```

效果：如果存在符合条件被此调用解除阻塞（31.6）的原子等待操作，则解除至少一个此类操作的执行阻塞。

备注：此函数是一个原子通知操作（31.6）。

```
void notify_all() noexcept;
```

效果：解除所有符合条件被此调用解除阻塞（31.6）的原子等待操作的执行阻塞。

备注：此函数是一个原子通知操作（31.6）。

## 31.9 非成员函数 [atomics.nonmembers]

1 名称匹配模式 `atomic_f` 或 `atomic_f_explicit` 的非成员函数模板，会调用成员函数 `f`，其中第一个参数的值作为对象表达式，其余参数（如果有）的值按顺序作为成员函数调用的参数。对于类型为 `atomic<T>::value_type*` 的参数，在传递给成员函数调用时会进行解引用。如果不存在这样的成员函数，则程序为病式。

2 [注1：非成员函数使程序员能够编写既可以作为 C 编译也可以作为 C++ 编译的代码，例如在共享头文件中。——尾注]

## 31.10 标志类型和操作 [atomics.flag]

```
namespace std {
  struct atomic_flag {
    constexpr atomic_flag() noexcept;
    atomic_flag(const atomic_flag&) = delete;
    atomic_flag& operator=(const atomic_flag&) = delete;
  }
}
```

```
void atomic_flag_wait(const volatile atomic_flag* object, bool old) noexcept;
void atomic_flag_wait(const atomic_flag* object, bool old) noexcept;
void atomic_flag_wait_explicit(const volatile atomic_flag* object,
    bool old, memory_order order) noexcept;
void atomic_flag_wait_explicit(const atomic_flag* object,
    bool old, memory_order order) noexcept;
void atomic_flag::wait(bool old, memory_order order =
    memory_order::seq_cst) const volatile noexcept;
void atomic_flag::wait(bool old, memory_order order =
    memory_order::seq_cst) const noexcept;
```

对于 `atomic_flag_wait`，令 `order` 为 `memory_order::seq_cst`。令 `flag` 在非成员函数中为 `object`，在成员函数中为 `this`。

前置条件：`order` 既不是 `memory_order::release` 也不是 `memory_order::acq_rel`。

效果：按顺序重复执行以下步骤：

+   - 计算 `flag->test(order) != old`。
+   - 如果该评估结果为 true，则返回。
+   - 阻塞，直到被原子通知操作解除阻塞，或被虚假唤醒。

备注：此函数是一个原子等待操作（31.6）。

```
void atomic_flag_notify_one(volatile atomic_flag* object) noexcept;
void atomic_flag_notify_one(atomic_flag* object) noexcept;
void atomic_flag::notify_one() volatile noexcept;
void atomic_flag::notify_one() noexcept;
```

效果：如果存在符合条件被此调用解除阻塞（31.6）的原子等待操作，则解除至少一个此类操作的执行阻塞。

备注：此函数是一个原子通知操作（31.6）。

```
void atomic_flag_notify_all(volatile atomic_flag* object) noexcept;
void atomic_flag_notify_all(atomic_flag* object) noexcept;
void atomic_flag::notify_all() volatile noexcept;
void atomic_flag::notify_all() noexcept;
```

效果：解除所有符合条件被此调用解除阻塞（31.6）的原子等待操作的执行阻塞。

备注：此函数是一个原子通知操作（31.6）。

## 31.11 栅栏 [atomics.fences]

本子条款引入了称为栅栏的同步原语。栅栏可以具有获取语义、释放语义或两者兼有。具有获取语义的栅栏称为获取栅栏。具有释放语义的栅栏称为释放栅栏。

如果存在原子操作 X 和 Y，它们都作用于某个原子对象 M，使得 A 在 X 之前被排序，X 修改 M，Y 在 B 之前被排序，并且 Y 读取了 X 写入的值，或读取了 X 假如是释放操作时假设释放序列中任何副作用所写入的值，则释放栅栏 A 与获取栅栏 B 同步。

如果存在原子操作 X，使得 A 在 X 之前被排序，X 修改 M，并且 B 读取了 X 写入的值，或读取了 X 假如是释放操作时假设释放序列中任何副作用所写入的值，则释放栅栏 A 与在原子对象 M 上执行获取操作的原子操作 B 同步。

如果存在作用于 M 的某个原子操作 X，使得 X 在 B 之前被排序，并且读取了 A 写入的值或读取了以 A 为首的释放序列中任何副作用所写入的值，则在原子对象 M 上执行释放操作的原子操作 A 与获取栅栏 B 同步。

```
extern "C" void atomic_thread_fence(memory_order order) noexcept;
```

效果：取决于 `order` 的值，此操作：

+   - 如果 `order == memory_order::relaxed`，则无效果；
+   - 如果 `order == memory_order::acquire` 或 `order == memory_order::consume`，则是获取栅栏；
# ISO/IEC 14882:2020(E)

+   (5.3) — 如果 `order == memory_order::release`，则是释放栅栏；
+   (5.4) — 如果 `order == memory_order::acq_rel`，则既是获取栅栏又是释放栅栏；
+   (5.5) — 如果 `order == memory_order::seq_cst`，则是顺序一致的获取和释放栅栏。

```
extern "C" void atomic_signal_fence(memory_order order) noexcept;
```

6 *效果：* 等价于 `atomic_thread_fence(order)`，不同之处在于所产生的排序约束仅建立在线程与在同一线程中执行的信号处理程序之间。

> [注1：`atomic_signal_fence` 可用于指定线程执行的操作对信号处理程序可见的顺序。编译器优化以及加载和存储的重排序会以与 `atomic_thread_fence` 相同的方式被抑制，但 `atomic_thread_fence` 原本会插入的硬件栅栏指令不会被发出。——尾注]

管理”延迟，表示为持续时间 Dₘ。延迟持续时间可能因超时而异，但在所有情况下，越短越好。

3 名称以 `_for` 结尾的函数接受一个指定持续时间的参数。这些函数产生相对超时。实现应使用稳定时钟来测量这些函数的时间。329 给定持续时间参数 Dₜ，超时的实时持续时间为 Dₜ + Dᵢ + Dₘ。

4 名称以 `_until` 结尾的函数接受一个指定时间点的参数。这些函数产生绝对超时。实现应使用时间点中指定的时钟来测量这些函数的时间。给定时钟时间点参数 Cₜ，当时钟在超时期间未被调整时，超时返回的时钟时间点应为 Cₜ + Dᵢ + Dₘ。如果时钟在超时期间被调整到时间 Cₐ，则行为应如下：

+   (4.1) — 如果 Cₐ > Cₜ，等待函数应尽可能快地唤醒，即 Cₐ + Dᵢ + Dₘ，因为超时已满足。此规范可能导致等待的总持续时间在使用稳定时钟测量时减少。
+   (4.2) — 如果 Cₐ ≤ Cₜ，等待函数不应超时，直到 `Clock::now()` 返回时间 Cₙ ≥ Cₜ，即在 Cₜ + Dᵢ + Dₘ 时唤醒。

> [注1：当时钟被向后调整时，此规范可能导致等待的总持续时间在使用稳定时钟测量时增加。当时钟被向前调整时，此规范可能导致等待的总持续时间在使用稳定时钟测量时减少。——尾注]

实现会在从上述指定时间点到使用稳定时钟的相对超时（基于 Cₜ 与调用 `_until` 函数时的时间点之差）返回的时间点之间的任何时刻从这种超时返回。

建议做法：实现应在时钟被向前调整时减少等待的持续时间。

5 [注2：如果时钟未与稳定时钟同步，例如 CPU 时间时钟，则这些超时可能无法提供有用的功能。——尾注]

6 实现提供的计时分辨率取决于操作系统和硬件。实现提供的最精细分辨率称为本机分辨率。

7 用于这些函数的实现提供的时钟满足 Cpp17TrivialClock 要求（27.3）。

8 如果在其执行期间，时钟、时间点或时间持续时间抛出异常，则接受指定超时参数的函数将抛出异常。此类异常称为超时相关异常。

> [注3：实现按 27.7 规定提供的时钟、时间点和持续时间类型的实例不会抛出异常。——尾注]

## 32.2.5 Cpp17Lockable 类型的要求 [thread.req.lockable]

### 32.2.5.1 总则 [thread.req.lockable.general]

1 执行代理是一个实体，例如线程，它可以与其他执行代理并行执行工作。

> [注1：实现或用户可以引入其他类型的代理，例如进程或线程池任务。——尾注]

调用代理由上下文决定，例如包含调用的调用线程，等等。

2 [注2：某些可锁定对象是“代理无关的”，因为它们适用于任何执行代理模型，因为它们不确定或存储代理的 ID（例如，普通的自旋锁）。——尾注]

3 标准库模板 `unique_lock`（32.5.5.4）、`shared_lock`（32.5.5.5）、`scoped_lock`（32.5.5.3）、`lock_guard`（32.5.5.2）、`lock`、`try_lock`（32.5.6）和 `condition_variable_any`（32.6.5）都操作于用户提供的可锁定对象。Cpp17BasicLockable 要求、Cpp17Lockable 要求和 Cpp17TimedLockable 要求列出了这些库类型为了由给定执行代理获取或释放锁的所有权而施加的要求。

> [注3：任何锁所有权的性质及其所带来的任何同步都不属于这些要求。——尾注]

