
```cpp
t == u, u == t, t != u 且 u != t 具有相同的域。
bool(t == u) == bool(u == t)
bool(t != u) != !bool(u == u)
bool(u != t) != bool(t != u).
```

```cpp
template<class T>
concept equality_comparable = weakly-equality-comparable-with<T, T>;
```

令 `a` 和 `b` 为类型 `T` 的对象。`T` 模型 `equality_comparable` 仅当 `bool(a == b)` 为真

且 `a` 等于 `b` (18.2) 时，否则为假。

> [注 1：`a == b` 保持相等性的要求意味着 `a` 具有传递性和对称性。

-- 注]

```cpp
template<class T, class U>
concept equality_comparable =
equality_comparable<T> && equality_comparable<U> &&
common_reference<const remove_reference<const T>, const remove_reference<const U>> &&
equality_comparable<
common_reference<
const remove_reference_t<T>,
const remove_reference_t<U>> &&
weakly-equality-comparable-with<T, U>;
```

给定 `T` 和 `U`，令 `a` 为类型 `remove_reference_t<T>` 的值，`b` 为类型 `const remove_reference_t<U>` 的值，且 `C` 为：

`common_reference_t<T>&, const remove_reference_t<U>& &&`

`T` 和 `U` 模型 `equality_comparable_with<T, U>` 仅当 `bool(a == u) == bool(C == C)` 时。[concept]]

# 18.5.4 Concept totally ordered

```cpp
template<class T>
concept totally_ordered =
equality_comparable<T> && partially-ordered-with<T, T>;
```

给定一个 `T` 和 `U`，令 `a, b` 为类型 `remove_reference_t<T>` 的值。`T` 模型 `totally-ordered` 仅当：

- `bool(a < b)`, `bool(a > b)`, 或 `bool(a == b)` 中恰好有一个为真。
- 如果 `(a < b)` 且 `bool(b < c)`，则 `bool(a < c)`。
- `bool(a <= b) == bool(b < a)`。
- `bool(a >= b) == bool(a < c)`。

```cpp
template<class T, class U>
concept totally_ordered =
totally_ordered<T> && totally_ordered<U> &&
equality_comparable_with<T, U> &&
common_reference_t<T,
const remove_reference_t<T>, const remove_reference_t<U>> &&
partially-ordered-with<T, U>;
```

给定 `T` 和 `U`，令 `a` 为类型 `remove_reference_t<T>` 的值，`b` 为类型 `const remove_reference_t<U>` 的值，`common_reference_t<T>, const remove_reference_t<U> &&`

`T` 和 `U` 模型 `totally_ordered_with<T, U>` 仅当 `bool(a == u) == bool(C == C)` 时。

- `bool(t == u) == bool(C == C)`.
- `bool(t > u) == bool(C > C)`.
- `bool(t < u) == bool(C <= C)`.
- `bool(t >= u) == bool(C >= C)`.
- `bool(u < t) == bool(C < C)`.
- `bool(u > t) == bool(C > C)`.
- `bool(u <= t) == bool(C <= C)`.
- `bool(u >= t) == bool(C >= C)`.

# 18.6. Object concepts

此子类描述了在 18.7 基础上的对象概念。

```cpp
template<class T>
concept movable = is_object(T) && move_constructible<T> &&
assignable<T>;
template<class T>
concept copyable = copy_constructible<T> && assignable<const T>;
template<class T>
concept swappable = movable<T> && copyable<T>;
template<class T>
concept destructible = default_destructible<T>;
template<class T>
concept regular = movable && copyable && swappable && destructible; 
template<class T>
concept standard_layout = regular && std::standard_layout_v<T>;
template<class T>
concept fully_copyable = regular && copy_copyable<T>;
template<class T>
concept fully_movable = regular && move_movable<T>;
```

# 18.7 Callable concepts

## 18.7.1 General

`Callable` 概念描述了 20.14 上的基础。

## 18.7.2 Invocable

`invocable` 概念指定了 `F` 和一组 `Args...` 之间的关系。

```cpp
template<class F, class... Args>
concept invocable = requires(F&& f, Args&&... args) {
    std::forward<F>(f)(std::forward<Args>(args)...);
} -> std::invocable_result<F, Args...>;
```

## 18.7.3 Regular_invocable

```cpp
template<class F, class... Args>
concept regular_invocable = invocable<F, Args...> && requires(F&& f, Args&&... args) {
    std::forward<F>(f)(std::forward<Args>(args)...);
} -> std::convertible_to<bool>; // no_except;
```

## 18.7.4 Predicate

```cpp
template<class F, class... Args>
concept predicate = regular_invocable<F, Args...> && requires(F&& f, Args&&... args) {
    std::forward<F>(f)(std::forward<Args>(args)...);
} -> std::convertible_to<bool>;
```

## 18.7.5 Relation

```cpp
template<class R, class T, class U>
concept relation =
predicate<R, T> && predicate<R, U> &&
predicate<R, T, U> && predicate<R, U, T>;
```

## 18.7.6 Equivalence_relation

```cpp
template<class R, class T, class U>
concept equivalence_relation = relation<R, T, U>;
```

一个关系模型 `equivalence_relation` 仅当在其参数上施加等价关系时。

## 18.7.7 Strict_weak_order

```cpp
template<class R, class T, class U>
concept strict_weak_order = relation<R, T, U>;
```

# ISO/IEC 14882:2020(E)

## 19 诊断库 [diagnostics]

## 19.1 通用 [diagnostics.general]

此类类描述了 C++ 程序可能用于检测和报告错误状况的组件。

以下子类描述了用于报告几类异常情况的组件、记录程序断言以及用于错误码的全局变量，如表 40 所示。

表 40：诊断库摘要 [tab.diagnostics.summary]

| 子类 | 头文件 |
| --- | --- |
| 19.2 异常类 | <stdexcept> |
| 19.3 断言 | <cassert> |
| 19.4 错误码 | <cerrno> |
| 19.5 系统错误支持 | <system_error> |

## 19.2 异常类 [std.exceptions]

### 19.2.1 通用 [std.exceptions.general]

C++ 标准库类被用于报告 C++ 程序中的某些错误。在由这些类所反映的模型中，错误分为两类：逻辑错误和运行时错误。

逻辑错误的区分特征是它们源于程序内部逻辑的错误。在理论上，它们是可以预防的。

相比之下，运行时错误是由于超出了程序的范围。它们无法预先预测。`<stdexcept>` 定义了若干类型的预定义异常，用于报告 C++ 程序中的错误。这些异常通过继承关系相关联。

### 19.2.2 头文件 <stdexcept> 概要 [stdexcept.syn]

```
namespace std {
    class logic_error;
    class domain_error;
    class invalid_argument;
    class length_error;
    class out_of_range;
    class runtime_error;
    class range_error;
    class overflow_error;
    class underflow_error;
}
```

### 19.2.3 类 logic_error [logic.error]

```cpp
namespace std {
    class logic_error : public exception {
    public:
        explicit logic_error(const string& what_arg);
        explicit logic_error(const char* what_arg);
    };
}
```

`logic_error` 定义了作为异常抛出的对象类型，用于报告假设在程序执行之前的问题，例如违反先置条件或类不变性。

```cpp
logic_error(const string& what_arg);
后置条件：strcmp(what(), what_arg.c_str()) == 0.
```

```cpp
logic_error(const char* what_arg);
3 后置条件：strcmp(what(), what_arg) == 0.
```

### 19.2.4 类 domain_error [domain.error]

```cpp
namespace std {
    class domain_error : public logic_error {
    public:
        explicit domain_error(const string& what_arg);
        explicit domain_error(const char* what_arg);
    };
}
```

`domain_error` 类定义了实现类作为异常抛出的对象类型，用于报告域错误。

`domain_error(const string& what_arg);`

2 后置条件：`strcmp(what(), what_arg.c_str()) == 0.`

`domain_error(const char* what_arg);`

3 后置条件：`strcmp(what(), what_arg) == 0.`

### 19.2.5 类 invalid_argument [invalid.argument]

```cpp
namespace std {
    class invalid_argument : public logic_error {
    public:
        explicit invalid_argument(const string& what_arg);
        explicit invalid_argument(const char* what_arg);
    };
}
```

`invalid_argument` 类定义了作为异常抛出的对象类型，用于报告无效参数。

`invalid_argument(const string& what_arg);`

2 后置条件：`strcmp(what(), what_arg.c_str()) == 0.`

`invalid_argument(const char* what_arg);`

3 后置条件：`strcmp(what(), what_arg) == 0.`

### 19.2.6 类 length_error [length.error]

```cpp
namespace std {
    class length_error : public logic_error {
    public:
        explicit length_error(const string& what_arg);
        explicit length_error(const char* what_arg);
    };
}
```

`length_error` 定义了作为异常抛出的对象类型，用于报告长度超过其允许大小。

`length_error(const string& what_arg);`

2 后置条件：`strcmp(what(), what_arg.c_str()) == 0.`

`length_error(const char* what_arg);`

3 后置条件：`strcmp(what(), what_arg) == 0.`

### 19.2.7 类 out_of_range [out.of.range]

```cpp
namespace std {
    class out_of_range : public logic_error {
    public:
        explicit out_of_range(const string& what_arg);
        explicit out_of_range(const char* what_arg);
    };
}
```

1 `out_of_range` 类定义了作为异常抛出的对象类型，用于报告值不在预期范围内。

`out_of_range(const string& what_arg);`

2 后置条件：`strcmp(what(), what_arg.c_str()) == 0.`

`out_of_range(const char* what_arg);`

3 后置条件：`strcmp(what(), what_arg) == 0.`

### 19.2.8 类 runtime_error [runtime.error]

```cpp
namespace std {
    class runtime_error : public exception {
    public:
        explicit runtime_error(const string& what_arg);
        explicit runtime_error(const char* what_arg);
    };
}
```

1 `runtime_error` 定义了作为异常抛出的对象类型，用于报告在程序执行之前的错误。

`runtime_error(const string& what_arg);`

2 后置条件：`strcmp(what(), what_arg.c_str()) == 0.`

`runtime_error(const char* what_arg);`

3 后置条件：`strcmp(what(), what_arg) == 0.`

### 19.2.9 类 range_error [range.error]

```cpp
namespace std {
    class range_error : public runtime_error {
    public:
        explicit range_error(const string& what_arg);
        explicit range_error(const char* what_arg);
    };
}
```

1 `range_error` 定义了作为异常抛出的对象类型，用于报告域错误。
