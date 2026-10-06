# ISO/IEC 14882:2017(E)

```
template <class InputIterator, class classBinaryOperation>
OutputIterator adjacent_difference(InputIterator first,
                               InputIterator last,
                               BinaryOperation binary_op);
template <class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2> // sec 28.4.5
ForwardIterator2 adjacent_difference(ExecutionPolicy&& exec,
                               ForwardIterator1 first,
                               ForwardIterator1 last,
                               ForwardIterator2 result);
template <class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
           classBinaryOperation>
ForwardIterator2 adjacent_difference(ExecutionPolicy&& exec, // sec 28.4.5
                               ForwardIterator1 first,
                               ForwardIterator1 last,
                               ForwardIterator2 result,
                               BinaryOperation binary_op);
```

```
// 28.12, iota
template <class ForwardIterator, class T>
void iota(ForwardIterator first, ForwardIterator last, T value);
```

```
// 28.13, greatest common divisor
template <class M, class N>
constexpr common_type_t<M, N> gcd(M m, N n);
```

```
// 28.14, least multiple
template <class M, class N>
constexpr common_type_t<M, N> lcm(M m, N n);
```

+   1 The requirements on the types of algorithms' arguments that are introduced in the Introduction to Class 28 also apply to the following algorithms.

+   2 Throughout this subclass, the parameters UnOperation, BinaryOperation, BinaryOperation1, and BinaryIterator2 are used whenever an algorithm expects a function object (23.14).

> 3 [ The use of closed ranges as well as semi-open ranges to specify requirements throughout this subclause is intentional. — end note]

# 29.8.2 Accumulate [accumulate]

```
template <class InputIterator, class T>
T accumulate(InputIterator first, InputIterator last, T init);
template <class InputIterator, class T, class BinaryOperation>
T accumulate(InputIterator first, InputIterator last, T init, BinaryOperation&& binary_op);

Requires: T must meet the requirements of Constructible (Table 24) and CopyAssignable (Table 26) types. In the range [first, last), binary_op must satisfy neither elements invalidate iterators or subranges. 281
```

+   2 Effects: Updates its result by initializing the accumulator with the initial value init and modifies it with acc = acc + i or acc = binary_op(acc, i) for every iterator i in the range [first, last) in order. 282

The use of closed ranges reduces reduction operator and Common List reduce function, but it avoids the difficulty of defining the result on an empty sequence by always requiring an initial value.

+   281 fully closed ranges
282 accumulate is stands for the APL reduction

§ 29.8.2 © ISO/IEC 2017 - All rights reserved 1126