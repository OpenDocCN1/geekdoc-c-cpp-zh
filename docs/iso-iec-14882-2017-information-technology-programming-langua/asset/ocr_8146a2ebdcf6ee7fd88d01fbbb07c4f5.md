# ISO/IEC 14882:2017(E)

```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
class ForwardIterator>
ForwardIterator set_symmetric_difference(
ExecutionPolicy&&& exec, // sec 28.4.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 first2, ForwardIterator2 last2,
ForwardIterator result);

template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
class ForwardIterator, class Compare=>
ForwardIterator set_symmetric_difference(
ExecutionPolicy&&& exec, // sec 28.4.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 first2, ForwardIterator2 last2,
Compare comp);
```

```
// 28.7.7, heap operations
```

```
template<class RandomAccessIterator>
void push_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare=>
void push_heap(RandomAccessIterator first, RandomAccessIterator last,
Compare comp);
```

```
template<class RandomAccessIterator>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare=>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last,
Compare comp);
```

```
template<class RandomAccessIterator>
void make_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare=>
void make_heap(RandomAccessIterator first, RandomAccessIterator last,
Compare comp);
```

```
template<class RandomAccessIterator>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare=>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last,
Compare comp);
```

```
template<class RandomAccessIterator>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare=>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

```
template<class ExecutionPolicy>
bool is_heap(ExecutionPolicy&&& exec, // sec 28.4.5
RandomAccessIterator first, RandomAccessIterator last, Compare comp);
template<class ExecutionPolicy, class RandomAccessIterator, class Compare=>
bool is_heap(ExecutionPolicy&&& exec, // sec 28.4.5
RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

```
template<class RandomAccessIterator>
RandomAccessIterator is_heap_until(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare=>
RandomAccessIterator is_heap_until(RandomAccessIterator first, RandomAccessIterator last,
Compare comp);
```