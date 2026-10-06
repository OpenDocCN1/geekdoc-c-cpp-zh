# ISO/IEC 14882:2017(E)

```
OutputIterator result);
template<class InputIterator, class OutputIterator, class BinaryOperation>
OutputIterator partial_sum(InputIterator first,
InputIterator last,
OutputIterator result,
BinaryOperation binary_op);
```

```
// 29.8.7, exclusive scan
template<class InputIterator, class OutputIterator, class T>
OutputIterator exclusive_scan(InputIterator first, InputIterator last,
OutputIterator result,
T init);
template<class InputIterator, class OutputIterator, class T. class BinaryOperation>
OutputIterator exclusive_scan(InputIterator first, InputIterator last,
OutputIterator result,
T init, BinaryOperation binary_op);
```

```
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator2, class T>
ForwardIterator2 exclusive_scan(ExecutionPolicy&& exec, // sec 29.8.4
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result,
T init);
```

```
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator2, class BinaryOperation>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec, // sec 29.8.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result,
T init, BinaryOperation binary_op);
```

```
// 29.8.8, inclusive scan
template<class InputIterator, class OutputIterator>
OutputIterator inclusive_scan(InputIterator first, InputIterator last,
OutputIterator result);
```

```
template<class InputIterator, class OutputIterator, class BinaryOperation, class T>
OutputIterator inclusive_scan(InputIterator first, InputIterator last,
OutputIterator result);
```

```
template<class InputIterator, class OutputIterator, class BinaryOperation>
OutputIterator inclusive_scan(InputIterator first, InputIterator last,
OutputIterator result,
BinaryOperation binary_op);
```

```
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator2>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec, // sec 29.8.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result,
T init);
```

```
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator2, class BinaryOperation>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec, // sec 29.8.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result,
BinaryOperation binary_op);
```

```
template<class ExecutionPolicy, class ForwardIterator, class BinaryOperation>
ForwardIterator2 inclusive_scan(ExecutionPolicy&& exec, // sec 29.8.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result, BinaryOperation binary_op, T init);
```