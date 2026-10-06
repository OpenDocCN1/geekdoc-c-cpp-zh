# ISO/IEC 14882:2017(E)

15    Returns:
    lhs.compare(<typename sub_match<BiIter>::string_type(rhs.data(), rhs.size())) < 0

```
template <class BiIter, class ST, class SA>
bool operator<>((
    const sub_match<BiIter>& lhs,
    const basic_string<typename iterator_traits<BiIter>::value_type, ST, SA>& rhs)
) {
    return rhs < lhs;
```

```
16    template <class BiIter, class ST, class SA>
bool operator>={(
    const sub_match<BiIter>& lhs,
    const basic_string<typename iterator_traits<BiIter>::value_type, ST, SA>& rhs)
) {
    Returns !(lhs < rhs);
```

```
template <class BiIter, class ST, class SA>
bool operator<=((
    const sub_match<BiIter>& lhs,
    const basic_string<typename iterator_traits<BiIter>::value_type, ST, SA>& rhs)
) {
    Returns !(rhs < lhs);
```

```
18   template <class BiIter>
bool operator===(const typename iterator_traits<BiIter>::value_type* lhs,
    const sub_match<BiIter>& rhs) {
    Returns rhs.compare(lhs) == 0;

```

```
19   template <class BiIter>
bool operator>=(const typename iterator_traits<BiIter>::value_type* lhs,
    const sub_match<BiIter>& rhs) {
    Returns lhs == rhs;

```

```
20   template <class BiIter>
bool operator<=(const typename iterator_traits<BiIter>::value_type* lhs,
    const sub_match<BiIter>& rhs) {
    Returns lhs > 0;

```

```
21   template <class BiIter>
bool operator>(const typename iterator_traits<BiIter>::value_type* lhs,
    const sub_match<BiIter>& rhs) {
    Returns rhs < lhs;

```

```
22   template <class BiIter>
bool operator>=(const typename iterator_traits<BiIter>::value_type* lhs,
    const sub_match<BiIter>& rhs) {
    Returns !(lhs < rhs);

```

```
23   template <class BiIter>
bool operator<=(const typename iterator_traits<BiIter>::value_type* lhs,
    const sub_match<BiIter>& rhs) {
    Returns !(rhs < lhs);

```

```
24   template <class BiIter>
bool operator<((const typename iterator_traits<BiIter>::value_type* lhs,
    const sub_match<BiIter>& rhs) {
    Returns !(rhs < lhs);

```

template <class BiIter>