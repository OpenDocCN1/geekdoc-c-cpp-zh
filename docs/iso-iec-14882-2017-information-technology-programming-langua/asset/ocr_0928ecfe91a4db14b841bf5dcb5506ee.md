# ISO/IEC 14882:2017(E)

p.second is the end of the output range beginning at out_false.

Complexity: Exactly last - first applications of pred.

```
template<class Forwarditator_point(Forwarditator partition_first,
    Forwarditator last,
    Predicate pred);
```

Requires: Forwarditator's value type shall be convertible to Predicate's argument type. [first, last) shall be partitioned by pred, i.e. all elements that satisfy pred appear before those that do not.

Returns an iterator if all_of(first, mid, pred) and none_of(mid, last, pred) are both true.

Complexity: O(log(last - first)) applications of pred.

# 28.7.5 Merge

```
template<class InputItator1, class InputItator2,
    OutputItator>
```

```
merge(InputItator1 first1, InputItator1 last1,
    InputItator2 first2, InputItator2 last2,
    OutputItator result);
template<class ExecutionPolicy, class ForwardItator1, class ForwardItator2,
    class ForwardItator>
merge(ExecutionPolicy&& ex, ForwardItator1 first1, ForwardItator1 last1,
    ForwardItator2 first2, ForwardItator2 last2,
    ForwardItator result);
```

```
template<class InputItator1, class InputItator2,
    class OutputItator, class Compare>
    OutputItator
```

```
merge(InputItator1 first1, InputItator1 last1,
    InputItator2 first2, InputItator2 last2,
    OutputItator result, Compare comp);
template<class ExecutionPolicy, class ForwardItator1, class ForwardItator2,
    class ForwardItator>
merge(ExecutionPolicy&& ex, ForwardItator1 first1, ForwardItator1 last1,
    ForwardItator2 first2, ForwardItator2 last2,
    ForwardItator result, Compare comp);
```

+   Requires: The ranges [first, last) and [first2, last) shall be sorted with respect to operator or comp. The resulting range shall not overlap with either of the original ranges.

+   Effects: Copies all of the two ranges [first, last) and [first2, last) into the range [result, result_last), where result_last is result + (last - first) + (last2 - first2), such that the resulting range satisfies is_sorted(result, result_last) or is_sorted(result, result_last, comp).

+   Returns: result + (last - first1) + (last2 - first2)

+   Complexity: Let N = (last - first1) + (last2 - first2):