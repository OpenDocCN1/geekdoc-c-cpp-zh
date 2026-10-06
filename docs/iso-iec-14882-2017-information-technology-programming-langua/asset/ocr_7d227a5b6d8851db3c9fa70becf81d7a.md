# ISO/IEC 14882:2017(E)

```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
             class ForwardIterator>
ForwardIterator
    set_difference(ExecutionPolicy&& exec,
                   ForwardIterator1 first1, ForwardIterator1 last1,
                   ForwardIterator2 first2, ForwardIterator2 last2,
                   ForwardIterator2 result);
```

```
template<class InputIterator1, class InputIterator2,
             class OutputIterator, class Compare>
OutputIterator
    set_symmetric_difference(InputIterator1&& first1, InputIterator1 last1,
                             InputIterator2&& first2, InputIterator2 last2,
                             OutputIterator result, Compare comp);
```

```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
             class ForwardIterator>
ForwardIterator
    set_symmetric_difference(ExecutionPolicy&& exec,
                               ForwardIterator1 first1, ForwardIterator1 last1,
                               ForwardIterator2 first2, ForwardIterator2 last2,
                               ForwardIterator2 result, Compare comp);
```

+   1. Effects: The elements of the range [first1, last1) which are not present in the range [first2, last2) go to the range beginning. The elements in the constructed range are sorted.
2. Returns: The end of the constructed range.
3. Complexity: At most 2 * (last1 - first1) + (last2 - first2) - 1 comparisons.
4. Remarks: If first contains m elements that are equivalent to each other and [first2, last2) contains n elements that are equivalent to them, the max(m - n, 0) elements from [first1, last1) will be copied to the output.

# 28.7.6.5 set_symmetric_difference

```
template<class InputIterator1, class InputIterator2,
             class OutputIterator>
OutputIterator
    set_symmetric_difference(InputIterator1&& first1, InputIterator1 last1,
                             InputIterator2&& first2, InputIterator2 last2,
                             OutputIterator result);
```

```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
             class ForwardIterator>
ForwardIterator
    set_symmetric_difference(ExecutionPolicy&& exec,
                               ForwardIterator1 first1, ForwardIterator1 last1,
                               ForwardIterator2 first2, ForwardIterator2 last2,
                               ForwardIterator2 result);
```

```
template<class InputIterator1, class InputIterator2,
             class OutputIterator, class Compare>
OutputIterator
    set_symmetric_difference(InputIterator1&& first1, InputIterator1 last1,
                             InputIterator2&& first2, InputIterator2 last2,
                             OutputIterator result, Compare comp);
```