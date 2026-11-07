
## Table G.14 Mutating Sequence Operations

| Function | Description |
| --- | --- |
| remove() | Removes all occurrences of an indicated value from a range and returns a past-the-end iterator for the resulting range. |
| remove_if() | Removes all occurrences of values for which a predicate object returns true from a range and returns a past-the-end iterator for the resulting range. |
| remove_copy() | Copies elements from one range to another, omitting elements that equal a specified value. |
| remove_copy_if() | Copies elements from one range to another, omitting elements for which a predicate function object returns true. |
| unique() | Reduces each sequence of two or more equivalent elements in a range to a single element. |
| unique_copy() | Copies elements from one range to another, reducing each sequence of two or more equivalent elements to one. |
| reverse() | Reverses the elements in a range. |
| reverse_copy() | Copies a range in reverse order to a second range. |
| rotate() | Treats a range as a circular ordering and rotates the elements left. |
| rotate_copy() | Copies one range to another in a rotated order. |
| random_shuffle() | Randomly rearranges the elements in a range. |
| shuffle() | Randomly rearranges the elements in a range using a function object type satisfying C++11 requirements for a uniform random generator. (C++11) |
| is_partitioned() | Returns true if a range is partitioned by a given predicate. |
| partition() | Places all the elements that satisfy a predicate function object before all elements that don't. |
| stable_partition() | Places all the elements that satisfy a predicate function object before all elements that don't. The relative order of elements in each group is preserved. |
| partition_copy() | Copies all the elements that satisfy a predicate function object to one output range and the remaining elements to a second output range. (C++11) |
| partition_point() | For a range partitioned by a given predicate, returns an iterator to the first element not satisfying the predicate. |

### copy_n() (C++11)

```cpp
template<class InputIterator, class Size, class OutputIterator>
OutputIterator copy_n(InputIterator first, Size n,
        OutputIterator result);
```

The copy_n() function copies n elements, starting from the location first, into the range [result, result + n). It returns result + n—that is, an iterator pointing one past the last copied-to location. The function does not require that the target can't overlap the source.

### copy_if() (C++11)

```cpp
template<class InputIterator, class OutputIterator,
         class Predicate>
OutputIterator copy_if(InputIterator first, InputIterator last,
                       OutputIterator result, Predicate pred);
```

The copy_if() function copies those elements referred to by the iterator i in the range [first, last), for which pred(*i) is true, into the range [result, result + (last - first)). It returns result + (last - first)—that is, an iterator pointing one past the last copied-to location. The function requires that result not be in the range [first, last)—that is, the target can't overlap the source.

### copy_backward()

```cpp
template<class BidirectionalIterator1,
         class BidirectionalIterator2>
BidirectionalIterator2 copy_backward(BidirectionalIterator1 first,
        BidirectionalIterator1 last, BidirectionalIterator2 result);
```

The copy_backward() function copies the elements in the range [first, last) into the range [result - (last - first), result). Copying begins with the element at last - 1 being copied to location result - 1 and proceeds backward from there to first. It returns result - (last - first)—that is, an iterator pointing one past the last copied-to location. The function requires that result not be in the range [first, last). However, because copying is done backward, it is possible for the target and source to overlap.

### move() (C++11)

```cpp
template<class InputIterator, class OutputIterator>
OutputIterator move(InputIterator first, InputIterator last,
                    OutputIterator result);
```

The move() function uses std::move() to move the elements in the range [first, last) into the range [result, result + (last - first)). It returns result + (last - first)—that is, an iterator pointing one past the last copied-to location. The function requires that result not be in the range [first, last)—that is, the target can't overlap the source.

### move_backward() (C++11)

```cpp
template<class BidirectionalIterator1,
        class BidirectionalIterator2>
BidirectionalIterator2 move_backward(BidirectionalIterator1 first,
        BidirectionalIterator1 last, BidirectionalIterator2 result);
```

The move_backward() function uses std::move() to move the elements in the range [first, last) into the range [result - (last - first), result). Copying begins with the element at last - 1 being copied to location result - 1 and proceeds backward from there to first. It returns result - (last - first)—that is, an iterator pointing one past the last copied-to location. The function requires that result not be in the range [first, last). However, because copying is done backward, it is possible for the target and source to overlap.

### swap()

```cpp
template<class T> void swap(T& a, T& b);
```

The swap() function exchanges values stored at two locations specified by references. (C++ moves this function to the utility header file.)

### swap_ranges()

```cpp
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator2 swap_ranges(
        ForwardIterator1 first1, ForwardIterator1 last1,
        ForwardIterator2 first2);
```

The swap_ranges() function exchanges values in the range [first1, last1) with the corresponding values in the range beginning at first2. The two ranges should not overlap.

### iter_swap()

```cpp
template<class ForwardIterator1, class ForwardIterator2>
void iter_swap(ForwardIterator1 a, ForwardIterator2 b);
```

The iter_swap() function exchanges values stored at two locations specified by iterators.

### transform()

```cpp
template<class InputIterator, class OutputIterator, class UnaryOperation>
OutputIterator transform(InputIterator first, InputIterator last,
        OutputIterator result, UnaryOperation op);

template<class InputIterator1, class InputIterator2, class OutputIterator,
         class BinaryOperation>
OutputIterator transform(InputIterator1 first1, InputIterator1 last1,
                         InputIterator2 first2, OutputIterator result,
                         BinaryOperation binary_op);
```

The first version of transform() applies the unary function object op to each element in the range [first, last) and assigns the return value to the corresponding element in the range beginning at result. So *result is set to op(*first), and so on. It returns result + (last - first)—that is, the past-the-end value for the target range.

The second version of transform() applies the binary function object op to each element in the range [first1, last1) and to each element in the range [first2, last2) and assigns the return value to the corresponding element in the range beginning at result. So *result is set to op(*first1, *first2), and so on. It returns result + (last - first), the past-the-end value for the target range.

### replace()

```cpp
template<class ForwardIterator, class T>
void replace(ForwardIterator first, ForwardIterator last,
             const T& old_value, const T& new_value);
```

The replace() function replaces each occurrence of the value old_value in the range [first, last) with the value new_value.

### replace_if()

```cpp
template<class ForwardIterator, class Predicate, class T>
void replace_if(ForwardIterator first, ForwardIterator last,
                Predicate pred, const T& new_value);
```

The replace_if() function replaces each value old in the range [first, last) for which pred(old) is true with the value new_value.

### replace_copy()

```cpp
template<class InputIterator, class OutputIterator, class T>
OutputIterator replace_copy(InputIterator first, InputIterator last,
                            OutputIterator result, const T& old_value, const T& new_value);
```

The replace_copy() function copies the elements in the range [first, last) to a range beginning at result but substituting new_value for each occurrence of old_value. It returns result + (last - first), the past-the-end value for the target range.

### replace_copy_if()

```cpp
template<class Iterator, class OutputIterator, class Predicate, class T>
OutputIterator replace_copy_if(Iterator first, Iterator last,
                               OutputIterator result, Predicate pred, const T& new_value);
```
