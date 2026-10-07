
# set_difference()

```cpp
template<class InputIterator1, class InputIterator2,
class OutputIterator>
Iterator set_difference(InputIterator1 first1,
Iterator1 last1, InputIterator2 first2,
Iterator2 last2, OutputIterator result);
```

```cpp
template<class InputIterator1, class InputIterator2,
class OutputIterator, class Compare>
Iterator set_difference(InputIterator1 first1,
Iterator1 last1, InputIterator2 first2,
Iterator2 last2, OutputIterator result,
Compare comp);
```

set_difference() function constructs the set that is the difference between the ranges [first1, last1) and [first2, last2) and copies the result to the location pointed by result. The resulting range does not overlap either of the original ranges. The function returns a past-the-end iterator for the constructed range. The difference is the set that contains the elements found in the first set but not the second. The first version uses <, and the second version uses the comparison object comp to determine the order.

# Appendix G The Standard Template Library Methods and Functions

## Working with Heaps

A heap is a common data form with the property that the first element in a heap is the largest. Whenever the first element is removed or any element is added, the heap may have to be rearranged to maintain its property. A heap is designed so that these two operations are done efficiently.

## make_heap ()

```cpp
template<class RandomAccessIterator>
void make_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void make_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

The make_heap () function makes a heap of the range [first, last). The first version uses < to determine the ordering, and the second version uses the comp comparison object.

## push_heap ()

```cpp
template<class RandomAccessIterator>
void push_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void push_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

The push_heap () function assumes that the range [first, last - 1) is a valid heap, and it adds the value at location last - 1 (that is, one past the end of the heap that is assumed to be valid) into the heap, making [first, last) a valid heap. The first version uses < to determine the ordering, and the second version uses the comp comparison object.

## pop_heap ()

```cpp
template<class RandomAccessIterator>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

The pop_heap () function assumes that the range [first, last) is a valid heap. It swaps the value at location last - 1 with the value at first and makes the range [first, last - 1) a valid heap. The first version uses < to determine the ordering, and the second version uses the comp comparison object.

## STL Functions

### sort_heap()

```cpp
template<class RandomAccessIterator>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last,
    Compare comp);
```

sort_heap() function assumes that the range [first, last] is a heap and sorts it. The first version uses < to determine the ordering, and the second version uses the comparison object.

### is_heap() (C++11)

```cpp
template<class RandomAccessIterator>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

is_heap() function returns true if the range [first, last) is a heap, false otherwise.

### is_heap_until() (C++11)

```cpp
template<class RandomAccessIterator>
bool is_heap_until(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
bool is_heap_until(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

is_heap_until() function returns true if the range [first, last] is a heap, false otherwise.

### Finding Minimum and Maximum Values

```cpp
template<class RandomAccessIterator>
Iterator min(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
Iterator min(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

min() function returns the minimum element in the range [first, last).

```cpp
template<class RandomAccessIterator>
Iterator max(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
Iterator max(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

max() function returns the maximum element in the range [first, last).

### minmax()

```cpp
template<class RandomAccessIterator>
pair<Iterator, Iterator> minmax(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
pair<Iterator, Iterator> minmax(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

minmax() function returns a pair containing the minimum and maximum elements in the range [first, last).
