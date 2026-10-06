# ISO/IEC 14882:2017(E)

# 29.7.9.4 indirect_array fill function

[indirect_array.fill]

```
void operator=(const T& const) const;
```

+   1 This function has reference semantics, assigning the value of its argument to the elements of the valarray<T> object to which the indirect_array object refers.

# 29.7.10 valarray range access

[valarray.range]

+   1 In the beginning and end function follows, unspecified1 is a type that meets the requirements of a mutable random iterator (27.2.7) and of a contiguous iterator (27.2.1) value_type is the template T and whose reference type is T. unspecified2 is a type that meets the requirements of a constant random iterator (27.2.7) and of a contiguous iterator (27.2.1) value_type is the template T and whose reference type is const T.

+   2 The iterators returned by begin and end are guaranteed to be valid until the member function resize(size_t, T) (29.7.2.8) is called for array or until the lifetime of array ends first.

```
template <class T> unspecified begin(valarray<T>& v);
template <class T> unspecified end(valarray<T>& v);
```

+   3 Returns: An iterator representing the first value in the array.

```
template <class T> unspecified end(valarray<T>& v);
template <class T> unspecified end(valarray<T>& v);
```

+   4 Returns: An iterator representing one past the last value in.

# 29.8 Generalized numeric operations

[numeric.ops]

# 29.8.1 Header <numeric> synopsis

[numeric.ops.overview]

```
namespace std {
  // 29.8.2. accumulate
  template <class Iterator, class T>
  T(InputIterator first, InputIterator last, T init);
  template <class Iterator, class T, class BinaryOperation>
  T(InputIterator first, InputIterator last, T init, BinaryOperation binary_op);
```

```
// 29.8.3. reduce
template<class Iterator>
  typename iterator_traits<Iterator>::value_type
  reduce(InputIterator first, InputIterator last);
  template<class Iterator, class T>
  T(InputIterator first, InputIterator last, T init);
  template<class Iterator, class T, class BinaryOperation>
  T(InputIterator first, InputIterator last, T init, BinaryOperation binary_op);
  template<class ForwardIteratorTag>
  template<class ExecutionPolicy, class ForwardIterator>
  typename iterator_traits<ForwardIterator>::value_type
  reduce(ExecutionPolicy& exec, // sec 28.4.1
    ForwardIterator first, ForwardIterator last);
  template<class ExecutionPolicy, class ForwardIterator>
  reduce(ExecutionPolicy&&, class D>
  reduce(ExecutionPolicy& exec, // sec 28.4.5
  template<class ExecutionPolicy, class T>
  T(ExecutionPolicy& exec, ForwardIterator first, ForwardIterator last, T init);
  template<class ExecutionPolicy, class T, class BinaryOperation>
  T(ExecutionPolicy& exec, // sec 28.4.5
    ForwardIterator first, ForwardIterator last, T init, BinaryOperation binary_op);
```

§ 29.8.1

©ISO/IEC 2017 - All rights reserved

1122