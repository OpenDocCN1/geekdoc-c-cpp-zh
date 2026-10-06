# ISO/IEC 14882:2017(E)

```
template<class ExecutionPolicy, class ForwardIterator, class Size, class Generator>
ForwardIterator generate_n(ExecutionPolicy&& exec, // see 28.4.5
ForwardIterator first, Size n, Generator gen);
```

```
// 28.6.8. remove
template<class ForwardIterator, class T>
ForwardIterator remove(ForwardIterator first, ForwardIterator last,
const T& value);
template<class ExecutionPolicy, class ForwardIterator, class T>
ForwardIterator remove(ExecutionPolicy&& exec, // see 28.4.5
ForwardIterator first, ForwardIterator last,
const T& value);
template<class ForwardIterator, class Predicate>
ForwardIterator remove_if(ForwardIterator first, ForwardIterator last,
Predicate pred);
template<class ExecutionPolicy, class ForwardIterator, class Predicate>
ForwardIterator remove_if(ExecutionPolicy&& exec, // see 28.4.5
ForwardIterator first, ForwardIterator last,
Predicate pred);
```

```
template<class InputIterator, class OutputIterator, class T>
OutputIterator remove_copy(InputIterator first, InputIterator last,
OutputIterator result, const T& value);
template<class ExecutionPolicy, class InputIterator, class ForwardIterator2>
ForwardIterator2 remove_copy(ExecutionPolicy&& exec, // see 28.4.5
ForwardIterator2 first, ForwardIterator2 last,
Predicate pred);
template<class InputIterator, class OutputIterator, class Predicate>
OutputIterator remove_copy(InputIterator first, InputIterator last,
OutputIterator result, Predicate pred);
template<class ExecutionPolicy, class InputIterator, class ForwardIterator2>
ForwardIterator2 remove_copy(ExecutionPolicy&& exec, // see 28.4.5
ForwardIterator2 first, ForwardIterator2 last,
Predicate pred);
```

```
// 28.6.9. unique
template<class ForwardIterator>
ForwardIterator unique(ForwardIterator first, ForwardIterator last);
template<class ForwardIterator, class BinaryPredicate>
ForwardIterator unique(ForwardIterator first, ForwardIterator last,
BinaryPredicate pred);
template<class ExecutionPolicy, class ForwardIterator>
ForwardIterator unique(ExecutionPolicy&& exec, // see 28.4.5
ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator, class BinaryPredicate>
ForwardIterator unique(ExecutionPolicy&& exec, // see 28.4.5
ForwardIterator first, ForwardIterator last,
BinaryPredicate pred);
template<class InputIterator, class OutputIterator>
OutputIterator unique_copy(InputIterator first, InputIterator last,
OutputIterator result);
template<class InputIterator, class OutputIterator, class BinaryPredicate>
OutputIterator unique_copy(InputIterator first, InputIterator last,
OutputIterator result, BinaryPredicate pred);
```