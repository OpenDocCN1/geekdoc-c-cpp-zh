

# ISO/IEC 14882:2017(E)

## 32.6 类模板原子 atomic

```cpp
namespace std {
template <class T> struct atomic {
    using value_type = T;
    static constexpr bool is_always_lock_free = implementation-defined;
    bool is_lock_free() const noexcept;
    void store(T val, memory_order = memory_order_seq_cst) volatile noexcept;
    void store(T val, memory_order = memory_order_seq_cst) noexcept;
    T load(memory_order = memory_order_seq_cst) const noexcept;
    T load(memory_order = memory_order_seq_cst) const noexcept;
    operator T() const noexcept;
    T exchange(T desired, memory_order = memory_order_seq_cst) volatile noexcept;
    T exchange(T desired, memory_order = memory_order_seq_cst) noexcept;
    bool compare_exchange(T& expected, T desired, memory_order = memory_order_seq_cst) volatile noexcept;
    bool compare_exchange(T& expected, T desired, memory_order = memory_order_seq_cst) noexcept;
    bool compare_exchange_weak(T& expected, T desired, memory_order = memory_order_seq_cst) volatile noexcept;
    bool compare_exchange_weak(T& expected, T desired, memory_order = memory_order_seq_cst) noexcept;

    atomic() = default;
    constexpr atomic(T) noexcept;
    atomic(const atomic&) = delete;
    atomic& operator=(const atomic&) = delete;
    operator T() volatile noexcept;
    operator T(T) volatile noexcept;
};
```

- 1 T 的模板参数应当是平凡可拷贝的（trivially copyable）（6.9）。[注：未静态初始化的类型参数可能难以使用。——注结束]

- 2 特化版本

- 3 原子特化对象的表示不需要与其对应的参数类型具有相同的大小。特化版本应尽可能具有相同的大小，以减少迁移现有代码的努力量。——注结束]

## 32.6.1 原子类型上的操作

- 1 许多操作带有 `volatile` 限定符。标准中没有改变“volatile 设备寄存器”语义。该限定符意味着在对 volatile 对象应用这些操作时，易变性（volatility）会被保留。它并不意味着对非 volatile 对象的操作会变成 volatile。——注结束]

```cpp
atomic() = default;
```

- 2 效果：将原子初始化为未初始化状态。[注：这些语义确保了与 C 语言的兼容性。——注结束]

```cpp
constexpr atomic(T desired) noexcept;
```

- 3 效果：使用期望值初始化对象。初始化不是原子操作（4.7）。[注：可能会出现访问原子 A 与其构造发生竞态的情况，例如通过对原子指针变量执行 `memory_order_relaxed` 操作将刚构造的对象 Λ 的地址传递给线程，然后立即在接收端线程中访问 Λ。这会导致未定义行为。——注结束]

```cpp
#define ATOMIC_VAR_INIT(value) see below
```

该宏展开为标记标记序列，用于对静态存储类型的原子变量进行常量初始化，该类型与 `value` 兼容初始化。[注：此操作可能不会初始化。——注结束] 对正在初始化的变量的并发访问（即使通过原子操作）也构成数据竞态。[例：]

```cpp
atomic<int> y = ATOMIC_VAR_INIT(5);
// 例结束
```

```cpp
static const bool is_lock_free = implementation-defined;
```

如果原子类型的操作都是无锁（lock-free），则静态数据成员 `is_always_lock_free` 为 `true`，否则为 `false`。[注：`is_always_lock_free` 的值与相应的原子....LOCK_FREE 宏（如果定义）的值一致。——注结束]

```cpp
bool is_lock_free() const noexcept;
```

如果原子操作是非锁的，则返回 `true`，否则返回 `false`。[注：`is_lock_free` 函数的返回值与相同顺序下 `is_always_lock_free` 的值一致。——注结束]

```cpp
void store(T desired, memory_order order = memory_order_seq_cst) noexcept;
```

要求：`order` 不应为 `memory_order_consume`、`memory_order_acquire` 或 `memory_order_acq_rel`。

原子地将此对象指向的值替换为 `desired`。内存根据 `order` 的值受到影响。

```cpp
T operator=(T desired) noexcept;
T operator=(T desired) noexcept;
```

等价于：`store(desired)`。

返回：`desired`。

```cpp
T load(memory_order order = memory_order_seq_cst) const noexcept;
```

要求：`order` 不应为 `memory_order_release` 或 `memory_order_acq_rel`。内存根据 `order` 的值受到影响。

原子地返回此对象的值。

```cpp
operator T() const noexcept;
```

等价于：`load()`。

```cpp
T exchange(T desired, memory_order order = memory_order_seq_cst) noexcept;
```

原子地将此对象指向的值替换为 `desired`。内存根据 `order` 的值受到影响。这些操作是原子读-写操作（4.7）。

- 16 返回：原子地返回在效果发生之前此对象指向的值。

```cpp
bool compare_exchange(T& expected, T desired, memory_order success, memory_order failure) volatile noexcept;
bool compare_exchange(T& expected, T desired, memory_order success, memory_order failure) noexcept;
bool compare_exchange_weak(T& expected, T desired, memory_order success, memory_order failure) volatile noexcept;
bool compare_exchange_weak(T& expected, T desired, memory_order success, memory_order failure) noexcept;
bool compare_exchange_weak(T& expected, T desired, memory_order order = memory_order_seq_cst) volatile noexcept;
bool compare_exchange_strong(T& expected, T desired, memory_order order = memory_order_seq_cst) noexcept;
```

- 17 要求：`failure` 参数不能为 `memory_order_release` 或 `memory_order_acq_rel`。

- 18 效果：`expected` 中的值被替换。它随后原子地将从 `expected` 替换的值与此内存的内容进行比较，如果比较成功，则此内存的内容为 `desired`。如果比较失败，则内存受到 `success` 值的影响。当只提供一个 `memory_order` 参数时，`success` 的值为 `order`，而 `failure` 的值除允许在比较成功时由 `memory_order_acq_rel` 替换为 `memory_order_acquire` 或 `memory_order_release` 外，否则，这些操作是对该内存的原子加载操作。

- 19 返回：比较的结果。

- 20 [注：例如，`compare_exchange_strong` 的效果是：

```cpp
if (memcmp(this, &expected, sizeof(*this)) == 0)
    memcpy(this, &desired, sizeof(*this));
else
    memcpy(expected, sizeof(*this));

// 例：比较交换操作的期望值如下。
 比较交换操作需要在再次迭代循环时更新 `expected`。
expected = current.load();
do {
    desired = function(expected);
} while (!current.compare_exchange_weak(expected, desired));

// 例：因为期望值仅在失败操作时更新，在成功时释放包含期望值的内存是有效的。例如，列表插入将按原子方式运行，如下：
do {
    p->next = head; // 使新列表节点指向当前头部
} while (!head.compare_exchange_weak(head, p)); // 尝试插入
```]

