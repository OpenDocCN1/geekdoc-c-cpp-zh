# ISO/IEC 14882:2017(E)

+   1 Returns: The first iterator i such that i and i + 1 are in the range for which the following conditions hold: *i == *(i + 1), pred(*i, *(i + 1)) != false. Returns last if no such iterator is found.
2 Complexity: For the overloads with ExecutionPolicy, min((i - first) + 1, last - first) applications of the corresponding predicate, where i is adjacent_first's return value. For the overloads with ExecutionPolicy, O(last - first) applications of the corresponding predicate.

# 28.5.9 Count

```
template<class InputIterator, class T>
typename iterator_traits<InputIterator>::difference_type
count(InputIterator first, InputIterator last, const T&);
template<class ExecutionPolicy, class ForwardIterator>
typename iterator_traits<ForwardIterator>::difference_type
count(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, const T&);
tntemplate<class InputIterator, class Predicate>
typename iterator_traits<InputIterator>::difference_type
count_if(InputIterator first, InputIterator last, Predicate pred);
template<class ExecutionPolicy, class ForwardIterator, class Predicate>
typename iterator_traits<ForwardIterator>::difference_type
count_if(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, Predicate pred);
```

+   1 Returns: The number of iterators in the range [first, last) for which the following conditions hold: *i == value, pred(*i) == false.
2 Complexity: Exactly first applications of the corresponding predicate.

# 28.5.10 Mismatch

```
template<class InputIterator1, class InputIterator2>
pair<InputIterator1, InputIterator2>
mismatch(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
pair<ForwardIterator1&&, ForwardIterator2>
mismatch(ExecutionPolicy&& exec, ForwardIterator1 first1, ForwardIterator1 last1, ForwardIterator2 first2);
template<class InputIterator1, class InputIterator2, class BinaryPredicate>
pair<InputIterator1, InputIterator2>
mismatch(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, BinaryPredicate pred);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class BinaryPredicate>
pair<ForwardIterator1, ForwardIterator2>
mismatch(ExecutionPolicy&& exec, ForwardIterator1 first1, ForwardIterator1 last1, ForwardIterator2 first2, BinaryPredicate pred);
```