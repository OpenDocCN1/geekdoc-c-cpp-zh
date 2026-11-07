The unique() function reduces each sequence of two or more equivalent elements in the
range [first,last) to a single element and returns a past-the-end iterator for the new
range.The first version uses the == operator for the value type to compare elements.The
second version uses the binary predicate function object pred to compare elements.That
is,elements pointed to by it1 and it2 match if pred(*it1, *it2) is true.

# ### unique_copy()

```
```
template<class InputIterator, class OutputIterator>
OutputIterator unique_copy(InputIterator first, InputIterator last,
                            OutputIterator result);
```
```

```
```
template<class InputIterator, class OutputIterator, class BinaryPredicate>
OutputIterator unique_copy(InputIterator first, InputIterator last,
                            OutputIterator result, BinaryPredicate pred);
```
```

The unique_copy() function copies the elements from the range [first,last) to the range
beginning at result,reducing each sequence of two or more identical elements to a sin-
gle element.It returns a past-the-end iterator for the new range.The first version uses the
== operator for the value type to compare elements.The second version uses the binary
predicate function object pred to compare elements.That is,elements pointed to by it1
and it2 match if pred(*it1, *it2) is true.

# ### reverse()

```
```
template<class BidirectionalIterator>
void reverse(BidirectionalIterator first, BidirectionalIterator last);
```
```

The reverse() function reverses the elements in the range [first,last) by invoking
swap(first, last - 1),and so on.

# ### reverse_copy()

```
```
template<class BidirectionalIterator, class OutputIterator>
OutputIterator reverse_copy(BidirectionalIterator first,
                            BidirectionalIterator last,
                            OutputIterator result);
```
```

The reverse_copy() function copies the elements in the range [first,last) to the
range beginning at result in reverse order.The two ranges should not overlap.

# ### rotate()

```
```
template<class ForwardIterator>
void rotate(ForwardIterator first, ForwardIterator middle,
            ForwardIterator last);
```
```

The rotate() function performs a left rotation on the elements in the range [first,
last).The element at middle is moved to first, the element at middle + 1 is moved to