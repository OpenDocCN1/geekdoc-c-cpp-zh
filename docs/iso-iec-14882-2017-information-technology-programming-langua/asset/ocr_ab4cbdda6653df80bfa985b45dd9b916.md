# ISO/IEC 14882:2017(E)

# 29.8.3 Reduce

```
template<class InputIterator>
typename iterator_traits<InputIterator>::value_type
reduce(InputIterator first, InputIterator last);
```

Effects Equivalent to:

```
return reduce(first, last,
typename iterator_traits<InputIterator>::value_type());
```

```
template<class ExecutionPolicy, class ForwardIterator>
typename iterator_traits<ForwardIterator>::value_type
reduce(ExecutionPolicy&& exec, ForwardIterator last);
```

Effects Equivalent to:

```
return reduce(std::forward<ExecutionPolicy>(exec), first, last,
typename iterator_traits<ForwardIterator>::value_type());
```

```
template<class InputIterator, class T>
reduce(InputIterator first, InputIterator last, T init, T binary_op);
```

Effects Equivalent to:

```
return reduce(first, last, init, plus<T>());
```

```
template<class ExecutionPolicy, class ForwardIterator, class T>
reduce(ExecutionPolicy&& exec, ForwardIterator last, T init, T binary_op);
```

Effects Equivalent to:

```
return reduce(std::forward<ExecutionPolicy>(exec), first, last, init, plus<T>());
```

```
template<class InputIterator, class T, class BinaryOperation>
reduce(InputIterator first, InputIterator last, T init, BinaryOperation binary_op);
```

```
template<class ExecutionPolicy, class ForwardIterator, class T, class BinaryOperation>
reduce(ExecutionPolicy&& exec, ForwardIterator last, T init, BinaryOperation binary_op);
```

Requires:

+   (5.1) T shall be Constructable (Table 23). binary_op(*first, init), binary_op(init, init), and binary_op(*first, *first) shall be convertible to T.

+   (5.3) binary_op shall not invalidate iterators or subranges, nor modify elements in the range range [first, last).

+   6 Returns: GENERALIZED_SUM(binary_op, init, i...) for i in [first, last).

+   7 Complexity: O(last - first) applications of binary_op.

> [Note: The difference between reduce and accumulate is that reduce applies binary_op in an unspecified order, which yields a deterministic result for non-associative or non-commutative binary_op such as floating-point addition. end note]