# ISO/IEC 14882:2017(E)

+   1 Requires: The range [first, last) shall be a valid non-empty heap. RandomIterator shall satisfy the requirements of ValueSwappable(20.5.3.2). The type of *first shall satisfy the requirements of MoveConstructible (Table 23) and of MoveAssignable (Table 25).

+   2 Effects: Swaps the value in the heap first with the value in the last - 1 and makes [first, last - 1) into a heap.

+   3 Complexity: At 2log(last - first) comparisons.

# 28.7.3 make_heap

```
template<class RandomAccessIterator>
void make_heap(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void make_heap(RandomAccessIterator first, RandomAccessIterator last,
               Compare comp);
```

+   1 Requires: The type of *first shall satisfy the MoveConstructible requirements (Table 23) and the MoveAssignable requirements (Table 25).

+   2 Effects: Creates a heap out of the range [first, last).

+   3 Complexity: At most 3(last - first) comparisons.

# 28.7.7.4 sort_heap

```
template<class RandomAccessIterator>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last,
               Compare comp);
```

+   1 Requires: The range [first, last) shall be a valid heap. RandomAccessIterator shall satisfy the requirements of ValueSwappable(20.5.3.2). The type of *first shall satisfy the requirements of MoveConstructible (Table 23) and of MoveAssignable (Table 25).

+   2 Effects: Sort elements in the heap (first, last).

+   3 Complexity: At most NlogN comparisons, where N = last - first.

# 28.7.7.5 is_heap

```
template<class RandomAccessIterator>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last);
```

+   1 Returns: is_heap_until(first, last) == last

```
template<class ExecutionPolicy, class RandomAccessIterator>
bool is_heap(ExecutionPolicy&& exec, exec,
             RandomAccessIterator first, RandomAccessIterator last);
```

+   2 Returns: is_heap_until(forward<ExecutionPolicy>(exec), first, last) == last

```
template<class RandomAccessIterator, class Compare>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

+   3 Returns: is_heap_until(first, last, comp) == last