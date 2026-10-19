

9 [注 7：推荐同样禁止以下示例中 r1 == r2 == 42，x 和 y 初始时均为零：

```
// Thread 1:
r1 = x.load(memory_order::relaxed);
if (r1 == 42) y.store(42, memory_order::relaxed);

// Thread 2:
r2 = y.load(memory_order::relaxed);
if (r2 == 42) x.store(42, memory_order::relaxed);
```

— 结束注

10 原子读写修改操作应始终读取在读写修改操作关联的写之前修改顺序中写入的最后一个值。

11 实现应在一个合理的时间内使原子存储对原子加载可见。

```
template<class T>
  T kill_dependency(T y) noexcept;
```

12 效果：参数不向返回值传递依赖关系（6.9.2）。

13 返回：y。

## 31.5 无锁属性 [atomics.lockfree]

```
#define ATOMIC_BOOL_LOCK_FREE unspecified
#define ATOMIC_CHAR_LOCK_FREE unspecified
#define ATOMIC_CHAR8_T_LOCK_FREE unspecified
#define ATOMIC_CHAR16_T_LOCK_FREE unspecified
#define ATOMIC_CHAR32_T_LOCK_FREE unspecified
#define ATOMIC_WCHAR_T_LOCK_FREE unspecified
#define ATOMIC_SHORT_LOCK_FREE unspecified
#define ATOMIC_INT_LOCK_FREE unspecified
#define ATOMIC_LONG_LOCK_FREE unspecified
#define ATOMIC_LLONG_LOCK_FREE unspecified
#define ATOMIC_POINTER_LOCK_FREE unspecified
```

1 ATOMIC_..._LOCK_FREE 宏指示相应原子类型的无锁属性，有符号和无符号变体被分组在一起。该属性也适用于原子模板的相应（部分）特化。值为 0 表示该类型永远不是无锁的。值为 1 表示该类型有时是无锁的。值为 2 表示该类型始终是无锁的。

2 至少有一个有符号整数特化的原子模板，以及对应无符号类型的特化（6.8.2），始终是无锁的。

[注 1：此要求在 freestanding 实现中是可选的（16.4.2.4）。 — 结束注]

3 函数 atomic_is_lock_free（31.8.2）指示对象是否无锁。在任何给定的程序执行中，针对相同类型的指针，锁无关查询的结果应保持一致。

4 非无锁的原子操作被视为可能阻塞（6.9.2.3）。

5 推荐做法：无锁操作也应是地址无关的328。这些操作的实现不应依赖于任何每个进程的状态。

[注 2：此限制使通过映射到进程多次的内存以及在两个进程之间共享的内存进行通信成为可能。 — 结束注]

## 31.6 等待与通知 [atomics.wait]

1 原子等待操作和原子通知操作提供了一种机制，可以比轮询更有效地等待原子对象的值发生变化。原子等待操作可能会阻塞，直到被原子通知操作解除阻塞，具体取决于每个函数的效果。

[注 1：程序不保证能观察到瞬态原子值，这一问题被称为 A-B-A 问题，如果条件仅暂时满足，可能导致持续阻塞。 — 结束注]

2 [注 2：以下函数是原子等待操作：

- (2.1) — atomic<T>::wait,

## 31.7 类模板 atomic_ref [atomics.ref.generic]

### 31.7.1 通用 [atomics.ref.generic.general]

3 [注 3：以下函数是原子通知操作：

- atomic<T>::notify_one 和 atomic<T>::notify_all,
- atomic_flag::notify_one 和 atomic_flag::notify_all,
- atomic_notify_one 和 atomic_notify_all,
- atomic_flag_notify_one 和 atomic_flag_notify_all, 以及
- atomic_ref<T>::notify_one 和 atomic_ref<T>::notify_all.

4 对原子对象 M 的原子等待操作的调用，如果存在对 M 的副作用 X 和 Y，使得：

- 原子等待操作在观察到 X 的结果后已阻塞，
- X 在 M 的修改顺序中先于 Y，且
- Y 在对原子通知操作的调用之前发生，

则有资格被对 M 的原子通知操作调用解除阻塞。

```
namespace std {
  template<class T> struct atomic_ref {
  private:
    T* ptr; // exposition only
  public:
    using value_type = T;
    static constexpr size_t required_alignment = implementation-defined;
    static constexpr bool is_always_lock_free = implementation-defined;
    bool is_lock_free() const noexcept;
    explicit atomic_ref(T&);
    atomic_ref(const atomic_ref&) noexcept;
    atomic_ref& operator=(const atomic_ref&) = delete;
    void store(T, memory_order = memory_order::seq_cst) const noexcept;
    T operator=(T) const noexcept;
    T load(memory_order = memory_order::seq_cst) const noexcept;
    operator T() const noexcept;
    T exchange(T, memory_order = memory_order::seq_cst) const noexcept;
    bool compare_exchange_weak(T&, T, memory_order, memory_order) const noexcept;
    bool compare_exchange_strong(T&, T, memory_order, memory_order) const noexcept;
    bool compare_exchange_weak(T&, T, memory_order = memory_order::seq_cst) const noexcept;
    bool compare_exchange_strong(T&, T, memory_order = memory_order::seq_cst) const noexcept;
    void wait(T, memory_order = memory_order::seq_cst) const noexcept;
    void notify_one() const noexcept;
    void notify_all() const noexcept;
  };
}
```

```
T exchange(T desired, memory_order order = memory_order::seq_cst) const noexcept;
```

效果：原子地用 desired 替换 *ptr 引用的值。内存受 order 值影响。此操作是原子读写修改操作（6.9.2）。

返回：原子地返回 *ptr 引用的值在效果发生之前的即时值。

```
bool compare_exchange_weak(T& expected, T desired, memory_order success, memory_order failure) const noexcept;
```

```
bool compare_exchange_strong(T& expected, T desired, memory_order success, memory_order failure) const noexcept;
```

```
bool compare_exchange_weak(T& expected, T desired, memory_order order = memory_order::seq_cst) const noexcept;
```

```
bool compare_exchange_strong(T& expected, T desired, memory_order order = memory_order::seq_cst) const noexcept;
```

前提条件：failure 参数既不是 memory_order::release 也不是 memory_order::acq_rel。

效果：检索 expected 中的值。然后原子地将 *ptr 引用的值的表示与从 expected 先前检索到的值进行相等性比较，如果为真，则用 desired 中的值替换 *ptr 引用的值。如果且仅如果比较为真，则根据 success 的值影响内存；如果比较为假，则根据 failure 的值影响内存。当仅提供一个 memory_order 参数时，success 的值为 order，failure 的值为 order，但 memory_order::acq_rel 的值应被替换为 memory_order::acquire 的值，且 memory_order::release 的值应被替换为 memory_order::relaxed 的值。如果且仅如果比较为假，则在原子操作之后，expected 中的值将被替换为在原子比较期间从 *ptr 引用的值读取的值。如果操作返回 true，则这些操作是对 *ptr 引用的值的原子读写修改操作（6.9.2.2）。否则，这些操作是对该内存的原子加载操作。

返回：比较的结果。

说明：弱比较交换操作可能自发失败。也就是说，即使 expected 和 ptr 引用的内存内容相等，它也可能返回 false 并将相同的内存内容写回 expected。

[注 2：此自发失败使比较交换能够在更广泛的机器上实现，例如 load-locked store-conditional 机器。自发失败的一个后果是，几乎所有弱比较交换的使用都将在循环中。当比较交换在循环中时，弱版本在某些平台上会提供更好的性能。当弱比较交换需要循环而强比较交换不需要时，强比较交换更可取。 — 结束注]

```
void wait(T old, memory_order order = memory_order::seq_cst) const noexcept;
```

前提条件：order 既不是 memory_order::release 也不是 memory_order::acq_rel。

效果：按顺序重复执行以下步骤：

- 评估 load(order) 并将其值表示与 old 的值表示进行相等性比较。
- 如果比较不相等，则返回。
- 阻塞直到被原子通知操作解除阻塞或自发解除阻塞。

说明：此函数是对原子对象 *ptr 的原子等待操作（31.6）。

```
void notify_one() const noexcept;
```

效果：解除至少一个对 *ptr 的原子等待操作的执行，如果存在此类原子等待操作，则该操作有资格被此调用解除阻塞（31.6）。

说明：此函数是对原子对象 *ptr 的原子通知操作（31.6）。

