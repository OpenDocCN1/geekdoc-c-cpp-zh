

## ISO/IEC 14882:2020(E)

(14.1.2) — 否则，如果 flags() & regex_constants::collate 为真，则当 traits_inst.translate(c) == traits_inst.translate(d) 时两个字符相等；

(14.1.3) — 否则，当 c == d 时两个字符相等。

(14.2) — 在正则表达式有限状态机对字符序列进行匹配时，将排序元素范围 c1–c2 与字符 c 进行比较的方式如下：如果 flags() & regex_constants::collate 为 false，则当 c1 <= c && c <= c2 时字符 c 匹配；否则，根据以下算法对 c 进行匹配：

```
string_type str1 = string_type(1,
    flags() & icase ?
        traits_inst.translate_nocase(c1) : traits_inst.translate(c1));
string_type str2 = string_type(1,
    flags() & icase ?
        traits_inst.translate_nocase(c2) : traits_inst.translate(c2));
string_type str = string_type(1,
    flags() & icase ?
        traits_inst.translate_nocase(c) : traits_inst.translate(c));
return traits_inst.transform(str1.begin(), str1.end())
    <= traits_inst.transform(str.begin(), str.end())
&& traits_inst.transform(str.begin(), str.end())
    <= traits_inst.transform(str2.begin(), str2.end());
```

(14.3) — 在正则表达式有限状态机对字符序列进行匹配时，测试某个排序元素是否为主等价类的成员，需先使用 traits::transform_primary 将该排序元素和等价类转换为排序键，然后比较各排序键是否相等。

(14.4) — 在正则表达式有限状态机对字符序列进行匹配时，如果 traits_inst.isctype(c, traits_inst.lookup_classname(first, last, flags() & icase)) 为 true，则字符 c 是迭代器范围 [first, last) 所指定字符类的成员。

另见：ECMA-262 15.10

## 31 原子操作库 [atomics]

### 31.1 概述 [atomics.general]

本章描述用于细粒度原子访问的组件。此类访问通过对原子对象的操作提供。

以下子条款描述了针对类型和操作的原子需求及组件，如表 143 所示。

表 143：原子库摘要 [tab:atomics.summary]

| 子条款 | 头文件 |
|---|---|
| 31.3 | 类型别名 — `<atomic>` |
| 31.4 | 顺序与一致性 |
| 31.5 | 无锁属性 |
| 31.6 | 等待与通知 |
| 31.7 | 类模板 atomic_ref |
| 31.8 | 类模板 atomic |
| 31.9 | 非成员函数 |
| 31.10 | 标志类型与操作 |
| 31.11 | 栅栏 |

### 31.2 头文件 `<atomic>` 概要 [atomics.syn]

```
namespace std {
  // 31.4, order and consistency
  enum class memory_order : unspecified;
  template<class T>
    T kill_dependency(T y) noexcept;

  // 31.5, lock-free property
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

  // 31.7, class template atomic_ref
  template<class T> struct atomic_ref;
  // 31.7.5, partial specialization for pointers
  template<class T> struct atomic_ref<T*>;

  // 31.8, class template atomic
  template<class T> struct atomic;
  // 31.8.5, partial specialization for pointers
  template<class T> struct atomic<T*>;

  // 31.9, non-member functions
  template<class T>
    bool atomic_is_lock_free(const volatile atomic<T>*) noexcept;
  template<class T>
    bool atomic_is_lock_free(const atomic<T>*) noexcept;
}
```

## ISO/IEC 14882:2020(E)

```
template<class T>
    void atomic_store(volatile atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    void atomic_store(atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    void atomic_store_explicit(volatile atomic<T>*, typename atomic<T>::value_type,
                               memory_order) noexcept;
template<class T>
    void atomic_store_explicit(atomic<T>*, typename atomic<T>::value_type,
                               memory_order) noexcept;
template<class T>
    T atomic_load(const volatile atomic<T>*) noexcept;
template<class T>
    T atomic_load(const atomic<T>*) noexcept;
template<class T>
    T atomic_load_explicit(const volatile atomic<T>*, memory_order) noexcept;
template<class T>
    T atomic_load_explicit(const atomic<T>*, memory_order) noexcept;
template<class T>
    T atomic_exchange(volatile atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    T atomic_exchange(atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    T atomic_exchange_explicit(volatile atomic<T>*, typename atomic<T>::value_type,
                               memory_order) noexcept;
template<class T>
    T atomic_exchange_explicit(atomic<T>*, typename atomic<T>::value_type,
                               memory_order) noexcept;
template<class T>
    bool atomic_compare_exchange_weak(volatile atomic<T>*,
                                      typename atomic<T>::value_type*,
                                      typename atomic<T>::value_type) noexcept;
template<class T>
    bool atomic_compare_exchange_weak(atomic<T>*,
                                      typename atomic<T>::value_type*,
                                      typename atomic<T>::value_type) noexcept;
template<class T>
    bool atomic_compare_exchange_strong(volatile atomic<T>*,
                                        typename atomic<T>::value_type*,
                                        typename atomic<T>::value_type) noexcept;
template<class T>
    bool atomic_compare_exchange_strong(atomic<T>*,
                                        typename atomic<T>::value_type*,
                                        typename atomic<T>::value_type) noexcept;
template<class T>
    bool atomic_compare_exchange_weak_explicit(volatile atomic<T>*,
                                               typename atomic<T>::value_type*,
                                               typename atomic<T>::value_type,
                                               memory_order, memory_order) noexcept;
template<class T>
    bool atomic_compare_exchange_weak_explicit(atomic<T>*,
                                               typename atomic<T>::value_type*,
                                               typename atomic<T>::value_type,
                                               memory_order, memory_order) noexcept;
template<class T>
    bool atomic_compare_exchange_strong_explicit(volatile atomic<T>*,
                                                 typename atomic<T>::value_type*,
                                                 typename atomic<T>::value_type,
                                                 memory_order, memory_order) noexcept;
template<class T>
    bool atomic_compare_exchange_strong_explicit(atomic<T>*,
                                                 typename atomic<T>::value_type*,
                                                 typename atomic<T>::value_type,
                                                 memory_order, memory_order) noexcept;
```

## ISO/IEC 14882:2020(E)

```
template<class T>
    T atomic_fetch_add(volatile atomic<T>*, typename atomic<T>::difference_type) noexcept;
template<class T>
    T atomic_fetch_add(atomic<T>*, typename atomic<T>::difference_type) noexcept;
template<class T>
    T atomic_fetch_add_explicit(volatile atomic<T>*, typename atomic<T>::difference_type,
                                memory_order) noexcept;
template<class T>
    T atomic_fetch_add_explicit(atomic<T>*, typename atomic<T>::difference_type,
                                memory_order) noexcept;
template<class T>
    T atomic_fetch_sub(volatile atomic<T>*, typename atomic<T>::difference_type) noexcept;
template<class T>
    T atomic_fetch_sub(atomic<T>*, typename atomic<T>::difference_type) noexcept;
template<class T>
    T atomic_fetch_sub_explicit(volatile atomic<T>*, typename atomic<T>::difference_type,
                                memory_order) noexcept;
template<class T>
    T atomic_fetch_sub_explicit(atomic<T>*, typename atomic<T>::difference_type,
                                memory_order) noexcept;
template<class T>
    T atomic_fetch_and(volatile atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    T atomic_fetch_and(atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    T atomic_fetch_and_explicit(volatile atomic<T>*, typename atomic<T>::value_type,
                                memory_order) noexcept;
template<class T>
    T atomic_fetch_and_explicit(atomic<T>*, typename atomic<T>::value_type,
                                memory_order) noexcept;
template<class T>
    T atomic_fetch_or(volatile atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    T atomic_fetch_or(atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    T atomic_fetch_or_explicit(volatile atomic<T>*, typename atomic<T>::value_type,
                               memory_order) noexcept;
template<class T>
    T atomic_fetch_or_explicit(atomic<T>*, typename atomic<T>::value_type,
                               memory_order) noexcept;
template<class T>
    T atomic_fetch_xor(volatile atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    T atomic_fetch_xor(atomic<T>*, typename atomic<T>::value_type) noexcept;
template<class T>
    T atomic_fetch_xor_explicit(volatile atomic<T>*, typename atomic<T>::value_type,
                                memory_order) noexcept;
template<class T>
    T atomic_fetch_xor_explicit(atomic<T>*, typename atomic<T>::value_type,
                                memory_order) noexcept;
template<class T>
    void atomic_wait(const volatile atomic<T>*, typename atomic<T>::value_type);
template<class T>
    void atomic_wait(const atomic<T>*, typename atomic<T>::value_type);
template<class T>
    void atomic_wait_explicit(const volatile atomic<T>*, typename atomic<T>::value_type,
                              memory_order);
template<class T>
    void atomic_wait_explicit(const atomic<T>*, typename atomic<T>::value_type,
                              memory_order);
template<class T>
    void atomic_notify_one(volatile atomic<T>*);
```

