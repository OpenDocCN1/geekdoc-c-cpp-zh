# ISO/IEC 14882:2017(E)

ForwardIterator first2, ForwardIterator last2,
BinaryPredicate pred);

+   Effects: Finds a sequence in the range [first1, last1 - (last2 - first2)) that for every
non-negative integer n < (last2 - first2), the following corresponding conditions hold: *(i +
n) = *(first2 + n), pred*(i + n), *(first2 + n)) != false. Returns last1 if [first2,
last2) is empty or if no iterator is found.

+   Complexity: At most (last2 - first2) * (last1 - first1 - (last2 - first2) + 1) applications of the corresponding predicate.

# 28.5.7 Find

```
template<class Iterator, class ForwardIterator>
InputIterator
find_of(InputIterator first1, InputIterator last1,
ForwardIterator first2, ForwardIterator last2);
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator2>
ForwardIterator
find_of(ExecutionPolicy&& exec, 
ForwardIterator first1, ForwardIterator last1,
ForwardIterator first2, ForwardIterator last2);
template<class Iterator, class ForwardIterator,
class BinaryPredicate>
InputIterator
find_of(InputIterator first1, InputIterator last1,
ForwardIterator first2, ForwardIterator last2,
BinaryPredicate pred);
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator2,
class BinaryPredicate>
ForwardIterator
find_of(ExecutionPolicy&& exec, 
ForwardIterator first1, ForwardIterator last1,
ForwardIterator first2, ForwardIterator last2,
BinaryPredicate pred);
```

+   Effects: Finds an element that matches one of a set of values.

+   Returns: The first iterator in the range [first1, last1) such that some iterator j in the range
[first2, last2) follows the conditions: i == pred*(i, j) != false. Returns last1
if [first2, last2) is empty or if no iterator is found.

+   Complexity: At most (last1 - first1) * (last2 - first2) applications of the corresponding predicate.

# 28.5.8 Adjacent find

```
template<class ForwardIterator>
ForwardIterator adjacent_find(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
ForwardIterator
adjacent_find(ExecutionPolicy&& exec, 
ForwardIterator first, ForwardIterator last);
```

```
template<class ForwardIterator, class BinaryPredicate>
ForwardIterator adjacent_find(ForwardIterator first, ForwardIterator last,
BinaryPredicate pred);
```