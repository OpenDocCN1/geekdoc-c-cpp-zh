# count()

```
template<class InputIterator, class T>
typename iterator_traits<InputIterator>::difference_type
    count(InputIterator first, InputIterator last, const T& value);
```

The count() function returns the number of elements in the range [first,last) that match the value value. The == operator for the value type is used to compare values. The return type is an integer type that is large enough to contain the maximum number of items the container can hold.

# count_if()

```
template<class InputIterator, class Predicate>
typename iterator_traits<InputIterator>::difference_type
    count_if(InputIterator first, InputIterator last, Predicate pred);
```

The count_if() function returns the number of elements in the range [first,last) for which the function object pred returns a true value when passed the element as an argument.

# mismatch()

```
template<class InputIterator1, class InputIterator2>
pair<InputIterator1, InputIterator2>
    mismatch(InputIterator1 first1,
             InputIterator1 last1, InputIterator2 first2);

template<class InputIterator1, class InputIterator2,
                         class BinaryPredicate>
pair<InputIterator1, InputIterator2>
    mismatch(InputIterator1 first1,
             InputIterator1 last1, InputIterator2 first2,
             BinaryPredicate pred);
```

Each of the mismatch() functions finds the first element in the range [first1,last1) that doesn’t match the corresponding element in the range beginning at first2 and returns a pair holding iterators to the two mismatching elements. If no mismatch is found, the return value is pair<last1, first2 + (last1 - first1)>. The first version uses the == operator to test matching. The second version uses the binary predicate function object pred to compare elements. That is, elements pointed to by it1 and it2 don’t match if pred(*it1, *it2) is false.

# equal()

```
template<class InputIterator1, class InputIterator2>
bool equal(InputIterator1 first1, InputIterator1 last1,
           InputIterator2 first2);
```