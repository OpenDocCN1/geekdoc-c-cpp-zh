```
template<typename Iterator, typename Distance>
void advanceIter(Iterator& x, Distance n)
{
    advanceIterImpl(x, n,
        typename
        std::iterator_traits<Iterator>::iterator_category());
}
```