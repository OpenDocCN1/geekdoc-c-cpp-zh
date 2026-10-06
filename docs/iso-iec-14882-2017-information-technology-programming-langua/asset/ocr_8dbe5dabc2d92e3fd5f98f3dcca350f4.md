# ISO/IEC 14882:2017(E)

(3.2) - All of binary_op(init, init), binary_op(init, *first), and binary_op(*first, *first) shall be convertible to T.

(3.3) - binary_op shall neither invalidate iterators or surranges, nor modify elements in the ranges [first, last] or [result, + (last - first)].

4 Effects: For each integer K in [0, last - first) assigns to result + K the value of:

```
GENERALIZED_HOMCOMMUTATIVE_SUM(
binary_op_init, *(first + 0), *(first + 1), ..., *(first + K - 1))
```

5 Returns: The end of the range begins at result.

6 Complexity: O(last - first) applications of binary_op.

7 Remarks: result may be equal to first.

> [Note: The difference between exclusive_scan and inclusive_scan is that exclusive_scan excludes the ith element of the ith. If binary_op is not mathematically associative, the behavior of exclusive_scan may be nondeterministic. — end note]

# 29.8.8 Inclusive scan [inclusive.scan]

```
template<class InputIterator, class OutputIterator>
OutputIterator inclusive_scan(InputIterator first, InputIterator last, OutputIterator result);
```

1 Effects: Equivalent to:

```
return inclusive_scan(first, last, result, plus<>());

template<class ExecutionPolicy, class BinaryOperation>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec,nForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result);

template<class ExecutionPolicy, class BinaryOperation>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec,
ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result);
```

2 Effects: Equivalent to:

```
return inclusive_scan(std::forward<ExecutionPolicy>(exec), first, last, result, plus<>());

template<class InputIterator, class OutputIterator, class BinaryOperation>
OutputIterator inclusive_scan(InputIterator first, InputIterator last, OutputIterator result, BinaryOperation binary_op);

template<class ExecutionPolicy, class BinaryOperation,n
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec,
ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result, BinaryOperation binary_op);
```

```
template<class InputIterator, class OutputIterator, class BinaryOperation, class T>
OutputIterator inclusive_scan(InputIterator first, InputIterator last, OutputIterator result, BinaryOperation binary_op, T init);

template<class ExecutionPolicy, class BinaryOperation, class T>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec,
ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result, BinaryOperation binary_op, T init);
```

3 Requires:

+   (3.1) - If init is provided, T shall be MoveConstructible (Table 23); otherwise, ForwardIterator1's value type shall be MoveConstructible.

+   (3.2) - If init is provided, binary_op(init, init), binary_op(init, *first), and binary_-