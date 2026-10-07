

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

set_difference() 函数构造两个范围 [first1, last1) 和 [first2, last2) 之间的差集，并将结果复制到 `result` 所向的位置。生成的范围与原始范围中的任一一个都不重叠。该函数返回一个指向构造范围末尾的迭代器。差集是包含第一个集合中但不在第二个集合中的元素的集合。第一个版本使用 `<`，第二个版本使用比较对象 `comp` 来确定顺序。

# 附录 G 标准模板库方法和函数

## 堆（Heaps）

堆是一种常见的数据结构，其属性是堆中的第一个元素是最大的。每当第一个元素被移除或添加任何元素时，堆可能需要重新排列以维护其属性。堆的设计是为了高效地完成这两个操作。

## make_heap ()

```cpp
template<class RandomAccessIterator>
void make_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void make_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

make_heap () 函数将范围 [first, last) 构造为一个堆。第一个版本使用 `<` 来确定顺序，第二个版本使用 `comp` 比较对象。

## push_heap ()

```cpp
template<class RandomAccessIterator>
void push_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void push_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

push_heap () 函数假设范围 [first, last - 1) 是一个有效的堆，并将其位置 `last - 1` 处的值（即假设为有效的堆末尾之后）加入堆中，使得 [first, last) 成为一个有效的堆。第一个版本使用 `<` 来确定顺序，第二个版本使用 `comp` 比较对象。

## pop_heap ()

```cpp
template<class RandomAccessIterator>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

pop_heap () 函数假设范围 [first, last) 是一个有效的堆。它将位置 `last - 1` 的的值与 `first` 处的值交换，并使范围 [first, last - 1) 成为有效的堆。第一个版本使用 `<` 来确定顺序，第二个版本使用 `comp` 比较对象。

## STL 函数

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

sort_heap() 函数假设范围 [first, last] 是一个堆并对其排序。第一个版本使用 `<` 来确定顺序，第二个版本使用比较对象。

### is_heap() (C++11)

```cpp
template<class RandomAccessIterator>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

is_heap() 函数在范围 [first, last) 是堆时返回 true，否则返回 false。

### is_heap_until() (C++11)

```cpp
template<class RandomAccessIterator>
bool is_heap_until(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
bool is_heap_until(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

is_heap_until() 函数在范围 [first, last] 是堆时返回 true，否则返回 false。

### 寻找最小值和最大值

```cpp
template<class RandomAccessIterator>
Iterator min(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
Iterator min(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

min() 函数返回范围 [first, last) 中的最小元素。

```cpp
template<class RandomAccessIterator>
Iterator max(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
Iterator max(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

max() 函数返回范围 [first, last) 中的最大元素。

### minmax()

```cpp
template<class RandomAccessIterator>
pair<Iterator, Iterator> minmax(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
pair<Iterator, Iterator> minmax(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

minmax() 函数返回一个包含范围 [first, last) 中最小值和最大值的对。

