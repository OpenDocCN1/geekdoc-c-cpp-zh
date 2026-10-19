Returns: The end of the resulting range beginning at result.

Complexity: 𝒪(last - first) applications of binary_op.

Remarks: result may be equal to first.

> [Note 1: The difference between exclusive_scan and inclusive_scan is that inclusive_scan includes the iᵗʰ input element in the iᵗʰ sum. If binary_op is not mathematically associative, the behavior of inclusive_scan can be nondeterministic. — end note]

# 25.10.10 Transform exclusive scan [transform.exclusive.scan]

```
template<class InputIterator, class OutputIterator, class T,
    class BinaryOperation, class UnaryOperation>
constexpr OutputIterator
transform_exclusive_scan(InputIterator first, InputIterator last,
    OutputIterator result, T init,
    BinaryOperation binary_op, UnaryOperation unary_op);
```

```
template<class ExecutionPolicy,
    class ForwardIterator1, class ForwardIterator2, class T,
    class BinaryOperation, class UnaryOperation>
ForwardIterator2
transform_exclusive_scan(ExecutionPolicy&& exec,
    ForwardIterator1 first, ForwardIterator1 last,
    ForwardIterator2 result, T init,
    BinaryOperation binary_op, UnaryOperation unary_op);
```

Mandates: All of

+   — binary_op(init, init),
+   — binary_op(init, unary_op(*first)), and
+   — binary_op(unary_op(*first), unary_op(*first))

are convertible to T.

Preconditions:

+   — T meets the Cpp17MoveConstructible (Table 28) requirements.
+   — Neither unary_op nor binary_op invalidates iterators or subranges, nor modifies elements in the ranges [first, last] or [result, result + (last - first)].

Effects: For each integer K in [0, last - first) assigns through result + K the value of:

```
GENERALIZED_NONCOMMUTATIVE_SUM(
    binary_op, init,
    unary_op(*(first + 0)), unary_op(*(first + 1)), ..., unary_op(*(first + K - 1)))
```

Returns: The end of the resulting range beginning at result.

Complexity: 𝒪(last - first) applications each of unary_op and binary_op.

Remarks: result may be equal to first.

> [Note 1: The difference between transform_exclusive_scan and transform_inclusive_scan is that transform_exclusive_scan excludes the iᵗʰ input element from the iᵗʰ sum. If binary_op is not mathematically associative, the behavior of transform_exclusive_scan can be nondeterministic. transform_exclusive_scan does not apply unary_op to init. — end note]

# 25.10.11 Transform inclusive scan [transform.inclusive.scan]

```
template<class InputIterator, class OutputIterator,
    class BinaryOperation, class UnaryOperation>
constexpr OutputIterator
transform_inclusive_scan(InputIterator first, InputIterator last,
    OutputIterator result,
    BinaryOperation binary_op, UnaryOperation unary_op);
```