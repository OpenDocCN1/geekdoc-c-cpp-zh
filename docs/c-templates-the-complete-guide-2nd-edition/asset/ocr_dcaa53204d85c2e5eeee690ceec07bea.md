```
template<typename T> typename T::iterator null_iterator;
template<> BitIterator null_iterator<std::bitset<100>>;
// BitIterator doesn't match T::iterator, and that is fine
```