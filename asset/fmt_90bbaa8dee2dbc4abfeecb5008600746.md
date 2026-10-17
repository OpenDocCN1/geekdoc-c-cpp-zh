
```cpp
// 25.10.5. 内积
  template<class Iterator1, class Iterator2, class T>
  constexpr T inner_product(Iterator1 first1, Iterator1 last1, Iterator2 first2, T init);
  template<class Iterator1, class Iterator2, class T, BinaryOperation = class BinaryOperation2>
  constexpr T inner_product(Iterator1 first1, Iterator1 last1, Iterator2 first2, T init, BinaryOperation binary_op);

  // 25.10.6. 变换归约
  template<class Iterator1, class Iterator2, class T>
  constexpr T transform_reduce(ExecutionPolicy exec, Iterator1 first1, Iterator1 last1, T init);
  template<class Iterator1, class Iterator2, class T, BinaryOperation = class BinaryOperation>
  constexpr T transform_reduce(ExecutionPolicy exec, Iterator1 first1, Iterator1 last1, Iterator2 first2, T init, BinaryOperation binary_op, BinaryOperation2 binary_op2);
  template<class Iterator, class T, UnaryOperation = class UnaryOperation>
  constexpr T transform_reduce(Iterator first, Iterator last, T init, BinaryOperation binary_op, UnaryOperation unary_op);

  template<class ExecutionPolicy, class ForwardIterator, class T>
  T transform_reduce(ExecutionPolicy&& exec, ForwardIterator firsti, ForwardIterator lasti, T init); // sec 25.3.5
```

```cpp
template<class ExecutionPolicy,
class ForwardIterator1, class ForwardIterator2, class T,
class BinaryOperation1, class BinaryOperation2>
T transform_reduce(ExecutionPolicy&& exec, // sec 25.9.5
    ForwardIterator1 first, ForwardIterator1 last,
    ForwardIterator2 first, T init,
    BinaryOperation binary_op, BinaryOperation2 binary_op2);
template<class ExecutionPolicy, class ForwardIterator, class T,
class BinaryOperation, class UnOperation> // sec 25.9.5
T transform_reduce(ExecutionPolicy&& exec,
    ForwardIterator first, ForwardIterator last, T init,
    BinaryOperation binary_op, UnOperation unary_op);
```

```cpp
// 25.10.7. 前缀和

template<class InputIterator, class OutputIterator>
constexpr OutputIterator
    partial_sum(InputIterator first, InputIterator last,
    OutputIterator result);
template<class InputIterator, class OutputIterator, class BinaryOperation>
constexpr OutputIterator
    partial_sum(InputIterator first, InputIterator last,
    OutputIterator result, BinaryOperation binary_op);
```

```cpp
// 25.10.8. 互斥扫描

template<class InputIterator, class OutputIterator, class T>
constexpr OutputIterator
    exclusive_scan(InputIterator first, InputIterator last,
    OutputIterator result, T init);
template<class InputIterator, class OutputIterator, class T, class BinaryOperation>
constexpr OutputIterator
    exclusive_scan(InputIterator first, InputIterator last,
    OutputIterator result, T init, BinaryOperation binary_op);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class T>
ForwardIterator2
    exclusive_scan(ExecutionPolicy&& exec, // sec 25.9.5
    ForwardIterator1 first, ForwardIterator1 last,
    ForwardIterator2 result, T init, BinaryOperation binary_op);
```

```cpp
// 25.10.9. 包含扫描

template<class InputIterator, class OutputIterator>
constexpr OutputIterator
    include_scan(InputIterator first, InputIterator last,
    OutputIterator result);
template<class InputIterator, class OutputIterator, class BinaryOperation>
constexpr OutputIterator
    include_scan(InputIterator first, InputIterator last,
    OutputIterator result, BinaryOperation binary_op);
template<class InputIterator, class OutputIterator, class BinaryOperation, class T>
constexpr OutputIterator
    include_scan(InputIterator first, InputIterator last,
    OutputIterator result, BinaryOperation binary_op, T);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
ForwardIterator2
    include_scan(ExecutionPolicy&& exec, // sec 25.9.5
    ForwardIterator1 first, ForwardIterator1 last,
    ForwardIterator2 result);
```

```cpp
template<class ExecutionPolicy, class ForwardIterator, class T,
class BinaryOperation>
ForwardIterator2
    inclusive_scan(ExecutionPolicy&& exec, // sec 25.3.5
    ForwardIterator first, ForwardIterator last,
    ForwardIterator2 result, BinaryOperation binary_op);
template<class ExecutionPolicy, class ForwardIterator, class T,
class BinaryOperation, class T>
ForwardIterator2
    inclusive_scan(ExecutionPolicy&& exec, // sec 25.3.5
    ForwardIterator first, ForwardIterator last,
    ForwardIterator2 result, BinaryOperation binary_op, T init);
```

```cpp
// 25.10.10. 变换互斥扫描

template<class InputIterator, class OutputIterator, class T,
class BinaryOperation, class UnOperation>
constexpr OutputIterator
    transform_exclusive_scan(InputIterator first, InputIterator last,
    OutputIterator result, T init,
    BinaryOperation binary_op, UnOperation unary_op);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class T,
class BinaryOperation, class UnOperation>
ForwardIterator2
    transform_exclusive_scan(ExecutionPolicy&& exec, // sec 25.3.5
    ForwardIterator1 first, ForwardIterator1 last,
    ForwardIterator2 result, T init,
    BinaryOperation binary_op, UnOperation unary_op);
```

```cpp
// 25.10.11. 变换包含扫描

template<class InputIterator, class OutputIterator, class BinaryOperation, class UnOperation>
constexpr OutputIterator
    transform_inclusive_scan(InputIterator first, InputIterator last,
    OutputIterator result,
    BinaryOperation binary_op, UnOperation unary_op);
template<class InputIterator, class OutputIterator, class BinaryOperation, class UnOperation, class T>
constexpr OutputIterator
    transform_inclusive_scan(InputIterator first, InputIterator last,
    OutputIterator result,
    BinaryOperation binary_op, UnOperation unary_op, T init);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class T,
class BinaryOperation, class UnOperation>
ForwardIterator2
    transform_inclusive_scan(ExecutionPolicy&& exec, // sec 25.3.5
    ForwardIterator1 first, ForwardIterator1 last,
    ForwardIterator2 result, BinaryOperation binary_op,
    UnOperation unary_op);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
class BinaryOperation, class UnOperation, class T>
ForwardIterator2
    transform_inclusive_scan(ExecutionPolicy&& exec, // sec 25.3.5
    ForwardIterator1 first, ForwardIterator1 last,
    ForwardIterator2 result,
    BinaryOperation binary_op, UnOperation unary_op, T init);
```

```cpp
// 25.10.12. 差分

template<class InputIterator, class OutputIterator>
constexpr OutputIterator
    adjacent_difference(InputIterator first, InputIterator last,
    OutputIterator result);
template<class InputIterator, class OutputIterator, class BinaryOperation>
constexpr OutputIterator
    adjacent_difference(InputIterator first, InputIterator last,
    OutputIterator result, BinaryOperation binary_op);
```

# ISO/IEC 14882:2020(E)

```cpp
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
ForwardIterator2
    adjacent_difference(ExecutionPolicy&& exec, // sec 25.3.5
                        ForwardIterator1 first, ForwardIterator1 last,
                        ForwardIterator2 result);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
    class BinaryOperation>
    adjacent_difference(ExecutionPolicy&& exec, // sec 25.3.5
                        ForwardIterator1 first, ForwardIterator1 last,
                        ForwardIterator2 result, BinaryOperation binary_op);
```

```cpp
// 25.10.13, iota

template<class T>
constexpr T iota(ForwardIterator1 first, ForwardIterator1 last, T value);
```

```cpp
// 25.10.14, greatest common divisor

template<class M, class N>
constexpr common_type_t<M, N> gcd(M m, N n);
```

```cpp
// 25.10.15, least common multiple

template<class M, class N>
constexpr common_type_t<M, N> lcm(M m, N n);
```

```cpp
// 25.10.16, midpoint

template<class T>
constexpr T midpoint(T a, T b) noexcept;
template<class T>
constexpr T* midpoint(T* a, T* b);
}
```
