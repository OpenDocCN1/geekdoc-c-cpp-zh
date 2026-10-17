
`pair<OutputIterator, OutputIterator> stable_partition(InputIterator first, InputIterator last, Predicate pred, OutputIterator out_true, OutputIterator out_false);`

`template<class ExecutionPolicy, class InputIterator, class OutputIterator> pair<OutputIterator1, OutputIterator2> stable_partition(ExecutionPolicy&& exec, // sec 28.4.5) InputIterator first, InputIterator last, Predicate pred, OutputIterator1 out_true, OutputIterator2 out_false);`

```cpp
template<class ForwardIterator, class Predicate>
ForwardIterator partition_point(ForwardIterator first,
    ForwardIterator last,
    Predicate pred);
```

## 28.7, sorting and related operations

### 28.7.1, sorting

```cpp
template<class RandomAccessIterator>
void sort(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void sort(RandomAccessIterator first, RandomAccessIterator last,
    Compare comp);
```

# ISO/IEC 14882:2017(E)

```cpp
template<class ExecutionPolicy, class RandomAccessIterator>
void sort(ExecutionPolicy&& exec, // see 28.4.5
RandomAccessIterator first, RandomAccessIterator last);

template<class ExecutionPolicy, class RandomAccessIterator, class Compare>
void sort(ExecutionPolicy&& exec, // see 28.4.5
RandomAccessIterator first, RandomAccessIterator last,
Compare comp);
```

```cpp
template<class RandomAccessIterator>
void stable_sort(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void stable_sort(RandomAccessIterator first, RandomAccessIterator last,
Compare comp);
```

```cpp
template<class ExecutionPolicy, class RandomAccessIterator>
void sort(ExecutionPolicy&& exec, // see 28.4.5
RandomAccessIterator first, RandomAccessIterator last);

template<class ExecutionPolicy, class RandomAccessIterator, class Compare>
void sort(ExecutionPolicy&& exec, // see 28.4.5
RandomAccessIterator first, RandomAccessIterator last,
Compare comp);
```

```cpp
template<class RandomAccessIterator>
void partial_sort(RandomAccessIterator first, RandomAccessIterator middle, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void partial_sort(RandomAccessIterator first, // ... comp);
```

```cpp
template<class ExecutionPolicy, class RandomAccessIterator>
void sort(ExecutionPolicy&& exec, // see 28.4.5
RandomAccessIterator first, RandomAccessIterator last);

template<class ExecutionPolicy, class RandomAccessIterator, class Compare>
void sort(ExecutionPolicy&& exec, // see 28.4.5
RandomAccessIterator first, RandomAccessIterator last, //n ... comp);
```

```cpp
template<class InputIterator>
void partial_copy(InputIterator first, InputIterator last, RandomAccessIterator result_last);
```

```cpp
template<class ExecutionPolicy, class RandomAccessIterator, class Compare>
void sort(ExecutionPolicy&& exec, // see 28.4.5
RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

```cpp
template<class ExecutionPolicy, class ForwardIterator>
void sort(ExecutionPolicy&& exec, // see 28.4.5
ForwardIterator first, ForwardIterator last, RandomAccessIterator result_last);
```

```cpp
template<class ExecutionPolicy, class ForwardIterator, class RandomAccessIterator, class Compare>
RandomAccessIterator partial_sort_copy(
    ExecutionPolicy&& exec,    // see 28.4.5
    ForwardIterator first, ForwardIterator last,
    RandomAccessIterator result_first,
    RandomAccessIterator last, Compare comp);

template<class ForwardIterator>
bool is_sorted(ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
bool is_sorted(ForwardIterator first, ForwardIterator last,
Compare comp);

template<class ExecutionPolicy, class ForwardIterator>
bool is_sorted(ExecutionPolicy&& exec,    // see 28.4.5
    ForwardIterator first, ForwardIterator last);

template<class ExecutionPolicy, class ForwardIterator, class Compare>
bool is_sorted(ExecutionPolicy&& exec,    // see 28.4.5
    ForwardIterator first, ForwardIterator last,
    Compare comp);

template<class ForwardIterator>
bool is_sorted_until(ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
bool is_sorted_until(ForwardIterator first, ForwardIterator last,
    Compare comp);

template<class ExecutionPolicy, class ForwardIterator>
is_sorted_until(ExecutionPolicy&& exec,    // see 28.4.5
    ForwardIterator first, ForwardIterator last,
    Compare comp);

template<class ExecutionPolicy, class ForwardIterator, class Compare>
void is_sorted_until(ExecutionPolicy&& exec,    // see 28.4.5
    ForwardIterator first, ForwardIterator last,
    Compare comp);
```

## 28.7.2. nth_element

```cpp
void nth_element(RandomAccessIterator first, RandomAccessIterator nth,
RandomAccessIterator last, class comp);

template<class ForwardIterator, class Compare>
void nth_element(RandomAccessIterator first, RandomAccessIterator nth,
    RandomAccessIterator last, class comp);

template<class ExecutionPolicy, class RandomAccessIterator>
void nth_element(ExecutionPolicy&& exec, // see 28.4.5
    RandomAccessIterator first, RandomAccessIterator nth,
    RandomAccessIterator last, class comp);

template<class ExecutionPolicy, class RandomAccessIterator, class Compare>
void nth_element(ExecutionPolicy&& exec, // see 28.4.5
    RandomAccessIterator first, RandomAccessIterator nth,
    RandomAccessIterator last, class comp);
```

## 28.7.3. binary search

```cpp
template<class ForwardIterator, class T>
bool binary_search(ForwardIterator first, ForwardIterator last, const T& value);

template<class ForwardIterator, class T, class Compare>
bool binary_search(ForwardIterator first, ForwardIterator last,
    const T& value, Compare comp);
```

```cpp
template<class ForwardIterator, class T>
ForwardIterator lower_bound(ForwardIterator first, ForwardIterator last,
    const T& value);

template<class ForwardIterator, class T, class Compare>
ForwardIterator upper_bound(ForwardIterator first, ForwardIterator last,
    const T& value, Compare comp);
```

```cpp
template<class ForwardIterator, class T>
pair<ForwardIterator, ForwardIterator> equal_range(ForwardIterator first,
    ForwardIterator last, const T& value);

template<class ForwardIterator, class T, class Compare>
pair<ForwardIterator, ForwardIterator> equal_range(ForwardIterator first,
    ForwardIterator last, const T& value, Compare comp);
```

```cpp
template<class ForwardIterator, class T>
bool binary_search(ForwardIterator first, ForwardIterator last,
    const T& value);

template<class ForwardIterator, class T, class Compare>
bool binary_search(ForwardIterator first, ForwardIterator last,
    const T& value, Compare comp);
```

## 28.7.5. merge

```cpp
template<class InputIterator, class InputIterator, class OutputIterator>
OutputIterator merge(InputIterator first1, InputIterator last1,
                      InputIterator first2, InputIterator last2,
                      OutputIterator result);

template<class InputIterator, class InputIterator, class OutputIterator, class Compare>
OutputIterator merge(InputIterator first1, InputIterator last1,
                      InputIterator first2, InputIterator last2,
                      OutputIterator result, Compare comp);
```

```cpp
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator>
ForwardIterator merge(ExecutionPolicy policy, ForwardIterator first1,
    ForwardIterator last1, ForwardIterator first2, ForwardIterator last2,
    OutputIterator result);

template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator, class Compare>
ForwardIterator merge(ExecutionPolicy policy, ForwardIterator first1,
    ForwardIterator last1, ForwardIterator first2, ForwardIterator last2,
    OutputIterator result, Compare comp);
```

```cpp
template<class BidirectionalIterator>
```
