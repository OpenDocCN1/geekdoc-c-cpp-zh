
# ISO/IEC 14882:2017(E)

- (2.1) - T shall be MoveConstructible (Table 23).
- (2.2) - All of
- (2.2.1) - binary_op(init, init),
- (2.2.2) - binary_op(init, binary_op2(*first1, *first2)),
- (2.2.3) - binary_op(binary_op2(*first1, *first2), init), and
- (2.2.4) - binary_op(binary_op2(*first1, *first2), binary_op2(*first1, *first2))
shall be convertible to T.
- (2.3) - Neither unary_op nor binary_op should invalidate subranges, or modify elements in the ranges [first1, last] and [first2, first2 + (last - first1)).

- 3 Returns:
GENERALIZED_SUM(binary_op, init, binary_op2(*i, *first2 + (i - first1)), ...)
for every iterator i in [first, last].

- 4 Complexity: O(last - first) applications of binary_op and binary_op2.
```cpp
template<class InputIterator, class T>
class BinaryOperation, class UnaryOperation>
transform<InputIterator first, InputIterator last, T init,
BinaryOperation op, UnaryOperation up);
template<class ExecutionPolicy, class T>
class ForwardIterator, class BinaryOperation
&& exec
transform_reduce(ExecutionPolicy& exec, ForwardIterator first,
ForwardIterator last, T init, BinaryOperation op, UnaryOperation_up);
```

- 5 Requires:
- (5.1) - T shall be MoveConstructible (Table 23).
- (5.2) - All of
- (5.2.1) - binary_op(init, init),
- (5.2.2) - binary_op(init, unary_op(*first)),
- (5.2.3) - binary_op(unary_op(*first), init), and
- (5.2.4) - binary_op(unary_op(*first), unary_op(*first))
shall be convertible to T.
- (5.3) - Neither unary_op nor binary_op should invalidate subranges, or modify elements in the ranges [first1, last].

- 6 Returns:
GENERALIZED_SUM(binary_op, init, unary_op(*i), ...)
for every iterator i in [first, last].

- 7 Complexity: O(last - first) applications of each unary_op and binary_op.

> [Note: transform_reduce does not apply unary_op to init. — end note]

# ISO/IEC 14882:2017(E)

# 29.8.6 Partial sum [partial.sum]

```cpp
template <class InputIterator, class OutputIterator>
OutputIterator partial_sum(
InputIterator first, InputIterator last,
OutputIterator result);
template <class InputIterator, class BinaryOperation>
OutputIterator partial_sum(
InputIterator first, InputIterator last,
OutputIterator result, BinaryOperation op);
```
Requires: InputIterator::value_type must be constructible from the type of *first. The result of the expression acc + i or binary_op(acc, i) shall be convertible to InputIterator's value type. acc shall be writable (27.2.1) to the output iterator. In [first, last] and [result, result + (last - first)] binary_op shall not modify elements or iterators.

- 2 Effects: For a non-empty range, the function creates an accumulator acc whose type is InputIterator's value type, initializes it with *first, and assigns the value to result. For every iterator i in [first, last) in order, acc is then modified by acc = acc + i or binary_op(acc, i) and the result is assigned to *(result + (i - first)).

- 3 Returns: result = (last - first).
- 4 Complexity: Lexington(last - first) - 1 applications of the binary operation.
- 5 Remarks: partial may be equal to first.

# 29.8.7 Exclusive scan [exclusive.scan]

```cpp
template <class InputIterator, class T>
OutputIterator exclusive_scan(InputIterator first, InputIterator last,
OutputIterator result, T init);
```
- 1 Effects: Equivalent to
```cpp
return exclusive_scan(first, last, result, init, plus<T>());
```
```cpp
template <class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class T>
ForwardIterator2 exclusive_scan(ExecutionPolicy exec, ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result, T init);
```
- 2 Effects: Equivalent to
```cpp
return exclusive_scan(std::forward<ExecutionPolicy>(exec),
first, last, result, init, plus<T>());
```
```cpp
template <class InputIterator, class OutputIterator, class T, class BinaryOperation>
OutputIterator exclusive_scan(InputIterator first, InputIterator last,
OutputIterator result, T init, BinaryOperation binary_op);

template <class ExecutionPolicy, class ForwardIterator, class T, class BinaryOperation>
ForwardIterator2 exclusive_scan(ExecutionPolicy exec, ForwardIterator first, ForwardIterator last,
ForwardIterator2 result, T init, BinaryOperation binary_op);
```
- 3 Requires:
- (3.1) T shall be MoveConstructible (Table 23).
- (3.2) All of binary_op(init, init), binary_op(init, *first), and binary_op(*first, *first) shall be convertible to T.
- (3.3) binary_op shall not invalidate iterators or subranges, nor modify elements in the ranges [first, last] or [result, result + (last - first)].
- 4 Effects: For each integer K in [0, last - first) assigns to result + K the value of:
```cpp
GENERALIZED_COMMUTATIVE_SUM(
binary_op, *(first + 0), *(first + 1), ..., *(first + K - 1))
```
- 5 Returns: The end of the range at result.
- 6 Complexity: O(last - first) applications of binary_op.
- 7 Remarks: result may be equal to first.
> [Note: The difference between exclusive_scan and inclusive_scan is that exclusive_scan excludes the ith element. If binary_op is not mathematically associative, the behavior of exclusive_scan may be non-deterministic. — end note]

# 29.8.8 Inclusive scan [inclusive.scan]

```cpp
template<class InputIterator, class OutputIterator>
OutputIterator inclusive_scan(InputIterator first, InputIterator last, OutputIterator result);
```
- 1 Effects: Equivalent to:
```cpp
return inclusive_scan(first, last, result, plus<>());
```
```cpp
template<class ExecutionPolicy, class ForwardIterator>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, ForwardIterator2 result);

template<class ExecutionPolicy, class BinaryOperation>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec, ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result);
```
- 2 Effects: Equivalent to:
```cpp
return inclusive_scan(std::forward<ExecutionPolicy>(exec), first, last, result, plus<>());
```
```cpp
template<class InputIterator, class OutputIterator, class BinaryOperation>
OutputIterator inclusive_scan(InputIterator first, InputIterator last, OutputIterator result, BinaryOperation binary_op);

template<class ExecutionPolicy, class BinaryOperation>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec, ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result, BinaryOperation binary_op);
```
```cpp
template<class InputIterator, class OutputIterator, class BinaryOperation, class T>
OutputIterator inclusive_scan(InputIterator first, InputIterator last, OutputIterator result, BinaryOperation binary_op, T init);

template<class ExecutionPolicy, class BinaryOperation, class T>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec, ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result, BinaryOperation binary_op, T init);
```
- 3 Requires:
- (3.1) If init is provided, T shall be MoveConstructible (Table 23); otherwise, ForwardIterator1's value type shall be MoveConstructible.
- (3.2) If init is provided, binary_op(init, init), binary_op(init, *first), and binary_op(*first, *first) shall be convertible to T; otherwise, binary_op(*first, *first) shall be convertible to ForwardIterator1's value type.
binary_op shall not invalidate iterators or subranges, nor modify elements in the ranges [first, last] or [result, result + (last - first)].
- 4 Effects: For each integer K in [0, last - first) assigns through result + K the value of:
```cpp
GENERALIZED_NONCOMMUTATIVE_SUM
  binary_op, init, *(first + 0), *(first + 1), ..., *(first + K)
```
if it is provided, or
- GENERALIZED_NONCOMMUTATIVE_SUM
  binary_op, *(first + 0), *(first + 1), ..., *(first + K)
otherwise.
- 5 Returns: The end of the result range beginning at result.
- 6 Complexity: (last - first) applications of binary_op.
- 7 Remarks: result may be equal to first.
> [Note: The difference between exclusive_scan and inclusive_scan is that inclusive_scan includes the input element in the ith sum. If binary_op is not mathematically associative, the behavior of inclusive_scan may be non-deterministic. — end note]

# 29.8.9 Transform exclusive_scan [transform.exclusive.scan]

```cpp
template<class InputIterator, class OutputIterator, class T, class BinaryOperation, class UnaryOperation>
OutputIterator transform_exclusive_scan(InputIterator first, InputIterator last,
OutputIterator result, T,
BinaryOperation binary_op,
UnaryOperation unary_op);
template<class ExecutionPolicy, class ForwardIterator2, class T, class BinaryOperation, class UnaryOperation>
ForwardIterator2 transform_exclusive_scan(ExecutionPolicy&& exec,
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result, T,
BinaryOperation binary_op,
UnaryOperation unary_op);
```
Requires:
- T shall be MoveConstructible(Table 23).

All of:
- binary_op(init, init),
- binary_op(init, unary_op*(first)), and
- binary_op(unary_op*(first), unary_op*(first))
shall be convertible to T.

Neither unary_op nor binary_op shall invalidate iterators or subranges, nor modify elements in the ranges [first, last] or [result, result + (last - first)].
