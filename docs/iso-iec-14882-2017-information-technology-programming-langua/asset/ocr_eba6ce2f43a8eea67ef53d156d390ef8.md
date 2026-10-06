# ISO/IEC 14882:2017(E)

```
// 28.6.13, shuffle
template<class RandomAccessIterator, class UniformRandomBitGenerator>
void shuffle(RandomAccessIterator first,
    RandomAccessIterator last,
    UniformRandomBitGenerator& g);
```

```
// 28.7.4, partitions
template<class InputIterator, class Predicate>
bool is_partitioned(InputIterator first, InputIterator last, Predicate pred);
template<class ExecutionPolicy, class Predicate>
bool is_partitioned(ExecutionPolicy&& exec, ForwardIterator last, Predicate pred) // see 28.4.5
ForwardIterator first, ForwardIterator last, Predicate pred);
```

```
template<class ForwardIterator, class Predicate>
ForwardIterator partition(ForwardIterator first,
    ForwardIterator last,
    Predicate pred);
```

```
template<class ExecutionPolicy, class Predicate>
ForwardIterator partition(ExecutionPolicy&& exec, ForwardIterator last, Predicate pred) // see 28.4.5
ForwardIterator first, ForwardIterator last,
    Predicate pred);
```

```
template<class BidirectionalIterator, class Predicate>
BidirectionalIterator stable_partition(BidirectionalIterator first,
    BidirectionalIterator last,
    Predicate pred);
```

```
template<class ExecutionPolicy, class Predicate>
BidirectionalIterator stable_partition(ExecutionPolicy&& exec, BidirectionalIterator last, Predicate pred) // see 28.4.5
ForwardIterator first, ForwardIterator last,
    Predicate pred);
```

```
template<class InputIterator, class OutputIterator>
pair<OutputIterator, OutputIterator> stable_partition(InputIterator first, InputIterator last,
    Predicate pred,
    OutputIterator out_true, OutputIterator out_false);
```

```
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator2>
pair<ForwardIterator1, ForwardIterator2> stable_partition(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, Predicate pred) // see 28.4.5
ForwardIterator first, ForwardIterator last,
    ForwardIterator1 out_true, ForwardIterator2 out_false,
    Predicate pred);
```

```
template<class ForwardIterator, class Predicate>
ForwardIterator partition_point(ForwardIterator first,
    ForwardIterator last,
    Predicate pred);
```

```
// 28.7, sorting and related operations
// 28.7.1, sorting
```

```
template<class RandomAccessIterator>
void sort(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare>
void sort(RandomAccessIterator first, RandomAccessIterator last,n    Compare comp);
```