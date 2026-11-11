
对 `std::atomic<floating-point type>` 的附加操作

| 成员函数 | 描述 |
|---|---|
| ++, -- | 对原子对象进行递增或递减（前置递增和后置递增）。 |

看一下这个简短示例。

```cpp
int intArray[5];
std::atomic<int*> p(intArray);
p++;
assert(p.load() == &intArray[1]);
p+=1;
assert(p.load() == &intArray[2]);
--p;
assert(p.load() == &intArray[1]);
```

在 C++11 中，为整型数据类型提供了原子类型。

### 2.3.3.4 `std::atomic<integral type>`

对于每种整型，都有一个 `std::atomic` 的完全特化 `std::atomic<integral type>`。`std::atomic<integral type>` 支持 `std::atomic<T*>` 或 `std::atomic<floating-point type>` 所支持的所有操作。此外，`std::atomic<integral type>` 还支持按位逻辑运算符 AND、OR 和 XOR。

原子对象上的所有操作

| 成员函数 | 描述 |
|---|---|
| fetch_or, \|= | 以原子方式与该值执行按位（AND、OR 和 XOR）运算。 |
| fetch_and, &=<br>fetch_xor, ^= | 返回旧值。 |

复合按位赋值操作与 fetch 版本之间有一个小差别。复合按位赋值操作返回新值；fetch 变体返回旧值。

更深入的观察可提供更多见解：没有可用的原子乘法、原子除法，也没有原子移位操作。这并不是一个显著的限制，因为这些操作很少需要，并且很容易实现。下面是一个原子 `fetch_mul` 函数的示例。

`std::atomic<bool>` 和 `std::atomic<integral type>` 的类型别名

| 类型别名 | 定义 |
|---|---|
| `std::atomic_char16_t` | `std::atomic<char16_t>` |
| `std::atomic_char32_t` | `std::atomic<char32_t>` |
| `std::atomic_wchar_t` | `std::atomic<wchar_t>` |
| `std::atomic_int8_t` | `std::atomic<std::int8_t>` |
| `std::atomic_uint8_t` | `std::atomic<std::uint8_t>` |
| `std::atomic_int16_t` | `std::atomic<std::int16_t>` |
| `std::atomic_uint16_t` | `std::atomic<std::uint16_t>` |
| `std::atomic_int32_t` | `std::atomic<std::int32_t>` |
| `std::atomic_uint32_t` | `std::atomic<std::uint32_t>` |
| `std::atomic_int64_t` | `std::atomic<std::int64_t>` |
| `std::atomic_uint64_t` | `std::atomic<std::uint64_t>` |
| `std::atomic_int_least8_t` | `std::atomic<std::int_least8_t>` |
| `std::atomic_uint_least8_t` | `std::atomic<std::uint_least8_t>` |
| `std::atomic_int_least16_t` | `std::atomic<std::int_least16_t>` |
| `std::atomic_uint_least16_t` | `std::atomic<std::uint_least16_t>` |
| `std::atomic_int_least32_t` | `std::atomic<std::int_least32_t>` |
| `std::atomic_uint_least32_t` | `std::atomic<std::uint_least32_t>` |
| `std::atomic_int_least64_t` | `std::atomic<std::int_least64_t>` |
| `std::atomic_uint_least64_t` | `std::atomic<std::uint_least64_t>` |
| `std::atomic_int_fast8_t` | `std::atomic<std::int_fast8_t>` |
| `std::atomic_uint_fast8_t` | `std::atomic<std::uint_fast8_t>` |
| `std::atomic_int_fast16_t` | `std::atomic<std::int_fast16_t>` |
| `std::atomic_uint_fast16_t` | `std::atomic<std::uint_fast16_t>` |
| `std::atomic_int_fast32_t` | `std::atomic<std::int_fast32_t>` |
| `std::atomic_uint_fast32_t` | `std::atomic<std::uint_fast32_t>` |
| `std::atomic_int_fast64_t` | `std::atomic<std::int_fast64_t>` |
| `std::atomic_uint_fast64_t` | `std::atomic<std::uint_fast64_t>` |
| `std::atomic_intptr_t` | `std::atomic<std::intptr_t>` |
| `std::atomic_uintptr_t` | `std::atomic<std::uintptr_t>` |
| `std::atomic_size_t` | `std::atomic<std::size_t>` |
| `std::atomic_ptrdiff_t` | `std::atomic<std::ptrdiff_t>` |
| `std::atomic_intmax_t` | `std::atomic<std::intmax_t>` |
| `std::atomic_uintmax_t` | `std::atomic<std::uintmax_t>` |
| `std::atomic_signed_lock_free` (C++20) | `std::atomic<signed integral>` |
| `std::atomic_unsigned_lock_free` (C++20) | `std::atomic<unsigned integral>` |

类型别名 `atomic_signed_lock_free` 和 `atomic_unsigned_lock_free` 是原子类型的特化，其模板参数为有符号或无符号整型。只有支持无锁整型特化的实现才提供这些别名。实现可以选择最高效的整型特化。

## 2.3.4 所有原子操作

首先，这里是原子对象上所有操作的列表。

原子对象上的所有操作

| 成员函数 | 描述 |
|---|---|
| test_and_set | 以原子方式将标志设为 true，并返回先前的值。 |
| clear | 以原子方式将标志设为 false。 |
| is_lock_free<br>atomic_ref<T>::is_always_lock_free | 检查原子对象是否无锁。<br>在编译时检查原子类型是否始终无锁。 |
| load<br>operator T | 以原子方式返回原子对象的值。<br>以原子方式返回原子对象的值。等价于 atomic.load()。 |
| store | 以原子方式用非原子值替换原子对象的值。 |
| exchange | 以原子方式用新值替换该值。返回旧值。 |
| compare_exchange_strong<br>compare_exchange_weak | 以原子方式比较并最终交换该值。详情见此处。 |
| fetch_add, +=<br>fetch_sub, -= | 以原子方式加上（减去）该值。<br>返回旧值。 |
| fetch_or, \|=<br>fetch_and, &=<br>fetch_xor, ^= | 以原子方式与该值执行按位（AND、OR 和 XOR）运算。<br>返回旧值。 |
| ++, -- | 对原子对象进行递增或递减（前置递增和后置递增）。 |
| notify_one (C++20)<br>notify_all (C++20) | 通知一个原子等待操作。<br>通知所有原子等待操作。 |
| wait (C++20) | 阻塞直到被通知。<br>将自身与旧值比较，以防止虚假唤醒和丢失唤醒。<br>如果与旧值比较不相等，则返回。 |

原子类型没有拷贝构造函数或拷贝赋值运算符，但它们支持通过隐式转换到底层内置类型来进行赋值。复合赋值运算符返回新值；fetch 变体返回旧值。复合赋值运算符返回值，而不是对被赋值对象的引用。

### 到基础类型的隐式转换

```cpp
std::atomic<long long> atomObj(2011);
atomObj = 2014;
long long nonAtomObj = atomObj;
```

每个成员函数都支持一个额外的内存序参数。内存序参数的默认值是 `std::memory_order_seq_cst`，但也可以使用 `std::memory_order_relaxed`、`std::memory_order_consume`、`std::memory_order_acquire`、`std::memory_order_release` 或 `std::memory_order_acq_rel`。`compare_exchange_strong` 和 `compare_exchange_weak` 成员函数可以用两个内存序参数化。一个用于成功情况，一个用于失败情况。如果只显式提供一个内存序，则它同时用于成功和失败情况。这里是关于内存序的详细信息。

当然，并非所有操作都可用于每种原子类型。该表显示了取决于原子类型的原子操作列表。

取决于原子类型的所有原子操作

| 成员函数 | atomic_flag | atomic<bool><br>atomic<T*><br>atomic<smart T> | atomic<floating-point> | atomic<T> | atomic<integral> |
|---|---|---|---|---|---|
| test_and_set | 是 | | | | |
| clear | 是 | | | | |
| is_lock_free | | 是 | 是 | 是 | 是 |
| atomic<T>::is_always_lock_free | | 是 | 是 | 是 | 是 |
| load | | 是 | 是 | 是 | 是 |
| operator T | | 是 | 是 | 是 | 是 |
| store | | 是 | 是 | 是 | 是 |
| exchange | | 是 | 是 | 是 | 是 |
| compare_exchange_strong | | 是 | 是 | 是 | 是 |
| compare_exchange_weak | | 是 | 是 | 是 | 是 |
| fetch_add, += | | | 是 | 是 | 是 |
| fetch_sub, -= | | | 是 | 是 | 是 |
| fetch_or, \|= | | | | | 是 |
| fetch_and, &= | | | | | 是 |
| fetch_xor, ^= | | | | | 是 |
| ++, -- | | | | 是 | |
| notify_one (C++20) | 是 | 是 | 是 | 是 | 是 |
| notify_all (C++20) | 是 | 是 | 是 | 是 | 是 |
| wait (C++20) | 是 | 是 | 是 | 是 | 是 |

## 2.3.5 自由原子函数

标志 `std::atomic_flag` 和类模板 `std::atomic` 的功能也可以通过自由函数使用。由于这些函数使用指针而不是引用，因此它们与 C 兼容。原子自由函数可用于 `std::atomic_flag` 以及诸如可与类模板 `std::atomic` 一起使用的那些类型。

用于 `std::atomic_flag` 的自由函数称为：`std::atomic_clear()`、`std::atomic_clear_explicit`、`std::atomic_flag_test_and_set()` 和 `std::atomic_flag_test_set_explicit()`。所有四种变体的第一个参数都是指向 `std::atomic_flag` 的指针。此外，两个 `_explicit` 变体期望一个内存序。

对于每种 `std::atomic` 类型，都有一个对应的自由函数可用。自由函数遵循直接的命名约定：只需在其前面添加前缀 `atomic_`。例如，对 `std::atomic` 的成员函数调用 `a.store()` 会变成 `std::atomic_store()` 和 `std::atomic_store_explicit()`。在这种情况下，第一个重载期望一个指针，第二个重载还期望一个内存序。

为完整起见，这里是所有重载：`atomic`¹³。

除一个例外，自由函数仅适用于原子类型。这条规则的显著例外是 `std::shared_ptr`。

### 2.3.5.1 `std::shared_ptr`（在 C++20 中弃用）

`std::shared_ptr` 是唯一可以应用原子操作的非原子数据类型。首先，让我谈谈这个例外的动机。

C++ 委员会认为，智能指针有必要在多线程程序中提供最低限度的原子性保证。最小原子性保证的含义是什么

¹³ http://en.cppreference.com/w/cpp/atomic

