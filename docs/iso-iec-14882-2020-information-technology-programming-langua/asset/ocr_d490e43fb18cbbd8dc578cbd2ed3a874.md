# 25.10.4 Reduce

```
template<class InputIterator>
constexpr typename iterator_traits<InputIterator>::value_type
reduce(InputIterator first, InputIterator last);
```

Effects: Equivalent to:

```
return reduce(first, last, typename iterator_traits<InputIterator>::value_type{});
```

```
template<class ExecutionPolicy, class ForwardIterator>
typename iterator_traits<ForwardIterator>::value_type
reduce(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last);
```

Effects: Equivalent to:

```
return reduce(std::forward<ExecutionPolicy>(exec), first, last, typename iterator_traits<ForwardIterator>::value_type{});
```

```
template<class InputIterator, class T>
constexpr T reduce(InputIterator first, InputIterator last, T init);
```

Effects: Equivalent to:

```
return reduce(first, last, init, plus<>());
```

```
template<class ExecutionPolicy, class ForwardIterator, class T>
T reduce(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, T init);
```

Effects: Equivalent to:

```
return reduce(std::forward<ExecutionPolicy>(exec), first, last, init, plus<>());
```

```
template<class InputIterator, class T, class BinaryOperation>
constexpr T reduce(InputIterator first, InputIterator last, T init, BinaryOperation binary_op);
```

```
template<class ExecutionPolicy, class ForwardIterator, class T, class BinaryOperation>
T reduce(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, T init, BinaryOperation binary_op);
```

Mandates: All of

+   - binary_op(init, *first),
+   - binary_op(*first, init),
+   - binary_op(init, init), and
+   - binary_op(*first, *first)

are convertible to T.

Preconditions:

+   - T meets the Cpp17MoveConstructible (Table 28) requirements.
+   - binary_op neither invalidates iterators or subranges, nor modifies elements in the range [first, last].

Returns: GENERALIZED_SUM(binary_op, init, *i, ...) for every i in [first, last).

Complexity: O(last - first) applications of binary_op.

[Note 1: The difference between reduce and accumulate is that reduce applies binary_op in an unspecified order, which yields a nondeterministic result for non-associative or non-commutative binary_op such as floating-point addition. — end note]

# 25.10.5 Inner product

```
template<class InputIterator1, class InputIterator2, class T>
constexpr T inner_product(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, T init);
```