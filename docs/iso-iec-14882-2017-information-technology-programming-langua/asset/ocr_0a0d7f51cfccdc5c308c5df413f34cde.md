# ISO/IEC 14882:2017(E)

```
template<class ForwardIterator, class T>
ForwardIterator upper_bound(ForwardIterator first, ForwardIterator last,
                               const T& value);
```

```
template<class ForwardIterator, class T, class Compare>
ForwardIterator upper_bound(ForwardIterator first, ForwardIterator last,
                               const T& value, Compare comp);
```

```
template<class ForwardIterator, class T>
pair<ForwardIterator, ForwardIterator>
             equal_range(ForwardIterator first, ForwardIterator last,
                          const T& value);
```

```
template<class ForwardIterator, class T, class Compare>
pair<ForwardIterator, ForwardIterator>
             equal_range(ForwardIterator first, ForwardIterator last,
                          const T& value, Compare comp);
```

```
template<class ForwardIterator, class T>
bool binary_search(ForwardIterator first, ForwardIterator last,
                   const T& value);
```

```
template<class ForwardIterator, class T, class Compare>
bool binary_search(ForwardIterator first, ForwardIterator last,
                   const T& value, Compare comp);
```

// 28.7.5. merge

```
template<class InputIterator, class InputIterator, class OutputIterator>
OutputIterator merge(InputIterator first1, InputIterator last1,
                      InputIterator first2, InputIterator last2,
                      OutputIterator result);
```

```
template<class InputIterator, class OutputIterator, class Compare>
OutputIterator merge(InputIterator first1, InputIterator last1,
                      InputIterator first2, InputIterator last2,
                      OutputIterator result, Compare comp);
```

```
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator>
ForwardIterator merge(ExecutionPolicy policy, ForwardIterator first1, ForwardIterator last1,
                                       ForwardIterator first2, ForwardIterator last2,
                                       ForwardIterator result);
```

```
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator, class Compare>
ForwardIterator merge(ExecutionPolicy policy, ForwardIterator first1, ForwardIterator last1,
                                       ForwardIterator first2, ForwardIterator last2,
                                       ForwardIterator result, Compare comp);
```

```
template<class BidirectionalIterator>
void inplace_merge(BidirectionalIterator first,
                   BidirectionalIterator middle,
                   BidirectionalIterator last);
```

```
template<class BidirectionalIterator, class Compare>
void inplace_merge(BidirectionalIterator first,
                   BidirectionalIterator middle,
                   BidirectionalIterator last, Compare comp);
```