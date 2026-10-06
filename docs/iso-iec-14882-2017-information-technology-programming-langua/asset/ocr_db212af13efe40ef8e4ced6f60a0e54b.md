# ISO/IEC 14882:2017(E)

```
template <class BIlter>
bool operator===(const typename iterator_traits<BIlter>::value_type& lhs,
               const sub_match<BIlter&>& rhs);
ntemplate <class BIlter>
bool operator===(const typename iterator_traits<BIlter>::value_type& lhs,
               const sub_match<BIlter&>& rhs);
```

```
template <class BIlter>
bool operator===(const sub_match<BIlter&>& lhs,
               const typename iterator_traits<BIlter>::value_type& rhs);
```

```
template <class BIlter>
bool operator!=(const sub_match<BIlter&>& lhs,
               const typename iterator_traits<BIlter>::value_type& rhs);
```

```
template <class BIlter>
bool operator===(const sub_match<BIlter&>& lhs,
               const typename iterator_traits<BIlter>::value_type& rhs);
```

```
template <class BIlter>
bool operator>=(const sub_match<BIlter&>& lhs,
               const typename iterator_traits<BIlter>::value_type& rhs);
```

```
template <class BIlter>
bool operator!=(const sub_match<BIlter&>& lhs,
               const typename iterator_traits<BIlter>::value_type& rhs);
```

```
template <class BIlter>
bool operator===(const sub_match<BIlter&>& lhs,
               const typename iterator_traits<BIlter>::value_type& rhs);
```

```
template <class chart, class ST, class BIlter>
basic_ostream<chart, ST>& os,
operator<<(const basic_ostream<chart, ST>& os, const sub_match<BIlter&>& m);
```

```
// 11.6 match_results
template <class BidirectionalIterator, class Allocator = allocator<sub_match<BidirectionalIterator>>>
match_results;
```

```
using cmatch = match_results<const char*>;
using wmatch = match_results<const wchar*>;
using match = match_results<string>::const_iterator;
using wmatch = match_results<wstring>::const_iterator>;
```

```
// match_results comparisons
template <class BidirectionalIterator, class Allocator>
bool operator==(const match_results<BidirectionalIterator, Allocator>& m1,
               const match_results<BidirectionalIterator, Allocator>& m2);
template <class BidirectionalIterator, class Allocator>
bool operator!=(const match_results<BidirectionalIterator, Allocator>& m1,
               const match_results<BidirectionalIterator, Allocator>& m2);
```

```
// 11.10.7. match_results swap
template <class BidirectionalIterator, class Allocator>
void swap(match_results<BidirectionalIterator, Allocator>& m1,
         match_results<BidirectionalIterator, Allocator>& m2);
```