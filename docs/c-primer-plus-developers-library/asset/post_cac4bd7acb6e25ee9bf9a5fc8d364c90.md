
### count()

```cpp
template<class InputIterator, class T>
typename iterator_traits<InputIterator>::difference_type
    count(InputIterator first, InputIterator last, const T& value);
```

The count() function returns the number of elements in the range [first,last) that match the value value. The == operator for the value type is used to compare values. The return type is an integer type that is large enough to contain the maximum number of items the container can hold.

### count_if()

```cpp
template<class InputIterator, class Predicate>
typename iterator_traits<InputIterator>::difference_type
    count_if(InputIterator first, InputIterator last, Predicate pred);
```

The count_if() function returns the number of elements in the range [first,last) for which the function object pred returns a true value when passed the element as an argument.

### mismatch()

```cpp
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

### equal()

```cpp
template<class InputIterator1, class InputIterator2>
bool equal(InputIterator1 first1, InputIterator1 last1,
           InputIterator2 first2);

template<class InputIterator1, class InputIterator2,
         class BinaryPredicate>
bool equal(InputIterator1 first1, InputIterator1 last1,
           InputIterator2 first2, BinaryPredicate pred);
```

The equal() function returns true if each element in the range [first1,last1) matches the corresponding element in the sequence beginning at first2 and false otherwise. The first version uses the == operator for the value type to compare elements. The second version uses the binary predicate function object pred to compare elements. That is, elements pointed to by it1 and it2 match if pred(*it1, *it2) is true.

### is_permutation() (C++11)

```cpp
template<class InputIterator1, class InputIterator2>
bool is_permutation(InputIterator1 first1, InputIterator1 last1,
                    InputIterator2 first2);

template<class InputIterator1, class InputIterator2,
         class BinaryPredicate>
bool is_permutation(InputIterator1 first1, InputIterator1 last1,
                    InputIterator2 first2, BinaryPredicate pred);
```

The is_permutation() function returns true if each element in the range [first1, last1) matches the corresponding element in some permutation of the equal-length sequence beginning at first2; it returns false otherwise. The first version uses the == operator for the value type to compare elements. The second version uses the binary predicate function object pred to compare elements. That is, elements pointed to by it1 and it2 match if pred(*it1, *it2) is true.

### search()

```cpp
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator1 search(
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2);

template<class ForwardIterator1, class ForwardIterator2,
         class BinaryPredicate>
ForwardIterator1 search(
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    BinaryPredicate pred);
```

The search() function finds the first occurrence in the range [first1, last1) that matches the corresponding sequence found in the range [first2, last2). It returns last1 if no such sequence is found. The first version uses the == operator for the value type to compare elements. The second version uses the binary predicate function object pred to compare elements. That is, elements pointed to by it1 and it2 match if pred(*it1, *it2) is true.

### search_n()

```cpp
template<class ForwardIterator, class Size, class T>
ForwardIterator search_n(ForwardIterator first, ForwardIterator last,
                         Size count, const T& value);

template<class ForwardIterator, class Size, class T, class BinaryPredicate>
ForwardIterator search_n(ForwardIterator first, ForwardIterator last,
                         Size count, const T& value, BinaryPredicate pred);
```

The search_n() function finds the first occurrence in the range [first,last) that matches the sequence consisting of count consecutive occurrences of value. It returns last if no such sequence is found. The first version uses the == operator for the value type to compare elements. The second version uses the binary predicate function object pred to compare elements. That is, elements pointed to by it1 and it2 match if pred(*it1, *it2) is true.

## Mutating Sequence Operations

Table G.14 summarizes the mutating sequence operations. Arguments are not shown, and overloaded functions are listed just once. A fuller description, including the prototypes, follows the table. Thus, you can scan the table to get an idea of what a function does and then look up the details if you find the function appealing.

Now let’s take a more detailed look at these mutating sequence operations. For each function, the discussion shows the prototype(s), followed by a brief explanation. As you saw earlier, pairs of iterators indicate ranges, with the chosen template parameter name indicating the type of iterator. As usual, a range in the form [first,last) goes from first up to, but not including, last. Functions passed as arguments are function objects, which can be function pointers or objects for which the `()` operation is defined. As in Chapter 16, a predicate is a Boolean function with one argument, and a binary predicate is a Boolean function with two arguments. (The functions need not be type `bool`, as long as they return 0 for false and a nonzero value for true.) Also as in Chapter 16, a unary function object is one that takes a single argument, and a binary function object is one that takes two arguments.

### copy()

```cpp
template<class InputIterator, class OutputIterator>
OutputIterator copy(InputIterator first, InputIterator last,
                    OutputIterator result);
```

The `copy()` function copies the elements in the range [first,last) into the range [result,result + (last - first)). It returns result + (last - first)—that is, an iterator pointing one past the last copied-to location. The function requires that result not be in the range [first,last)—that is, the target can't overlap the source.

### Table G.14 Mutating Sequence Operations

| Function | Description |
| --- | --- |
| `copy()` | Copies elements from a range to a location identified by an iterator. |
| `copy_n()` | Copies n elements from one location identified by an iterator to a second location identified by an iterator. (C++11) |
| `copy_if()` | Copies elements satisfying a predicate test from a range to a location identified by an iterator. (C++11) |
| `copy_backward()` | Copies elements from a range to a location identified by an iterator. Copying begins at the end of the range and proceeds backward. |
| `move()` | Moves elements from a range to a location identified by an iterator. (C++11) |
| `move_backward()` | Moves elements from a range to a location identified by an iterator. Moving begins at the end of the range and proceeds backward. (C++11) |
| `swap()` | Exchanges two values stored at locations specified by references. |
| `swap_ranges()` | Exchanges corresponding values in two ranges. |
| `iter_swap()` | Exchanges two values stored at locations specified by iterators. |
| `transform()` | Applies a function object to each element in a range (or to each pair of elements in a pair of ranges) and copies the return value to the corresponding location of another range. |
| `replace()` | Replaces each occurrence of a value in a range with another value. |
| `replace_if()` | Replaces each occurrence of a value in a range with another value if a predicate function object applied to the original value returns `true`. |
| `replace_copy()` | Copies one range to another and replaces each occurrence of a specified value with another value. |
| `replace_copy_if()` | Copies one range to another and replaces each value for which a predicate function object is `true` with an indicated value. |
| `fill()` | Sets each value in a range to an indicated value. |
| `fill_n()` | Sets n consecutive elements to a value. |
| `generate()` | Sets each value in a range to the return value of a generator, which is a function object that takes no arguments. |
| `generate_n()` | Sets the first n values in a range to the return value of a generator, which is a function object that takes no arguments. |
