# ISO/IEC 14882:2017(E)

# 31.12 Regular expression iterators

# 31.12.1 Class template regex_iterator

The class regex_iterator is an iterator adaptor. It represents a new view of existing iterator sequence, by enumerating all occurrences of a regular expression within that sequence. A regex_iterator uses regex_search to find successive regex matches within the sequence from which it was constructed. The iterator is constructed, and stores a value of match_results<BidirectionalIterator>. If the end of the sequence is reached (regex_search returns false), the iterator becomes equal to the end-of-sequence iterator value. The default constructor constructs an end-of-sequence iterator (not defined), which is the only iterator permitted to be used for the end. The result of regex_iterator on an end-of-sequence iterator is not defined. For other iterator values a const match_results<BidirectionalIterator>& is returned. The result of operator* on match_results<BidirectionalIterator> is returned. It is possible to store things into regex_iterators. Two non-end-sequence iterators are equal. An end-sequence iterator is not equal when they are constructed from the same arguments.

```
namespace std {
    template <BidirectionalIterator>
    typename iterator_traits<BidirectionalIterator>::value_type;
    class traits : regex_traits<BidirectionalIterator>;
    class regex_iterator {
    public:
        regex_iterator() = basic_regex<charT, traits>
        using forward_iterator;
        using iterator_category = match_results<BidirectionalIterator>;
        using value_type = pdiff_t;
        using pointer = const value_type*;
        using reference = const value_type&;

        regex_iterator()
_iterator();
        regex_iterator(const BidirectionalIterator a, BidirectionalIterator b,
                       const regex_type* re,
                       const regex_constants::match_type m = regex_constants::match_default);
        regex_iterator(const BidirectionalIterator a, BidirectionalIterator,
                       const regex_constants::match_type flags = regex_constants::match_default) = delete;
                       const regex_type* re);
        regex_iterator(const regex_iterator& iter);
        regex_iterator& operator=(const regex_iterator& iter) = default;
        bool operator==(const regex_iterator& other) const;
        bool operator!=(const regex_iterator& other) const;
        const value_type& operator*() const;
        const value_type* operator->() const;
        regex_iterator& operator++();
        regex_iterator operator++(int);

    private:
        BidirectionalIterator begin; // exception only
        BidirectionalIterator end; // exception only
        const regex_type* prege; // exception only
        const regex_constants::match_type flags; // exception only
        match_results<BidirectionalIterator> match; // exception only
};
```

§ 31.12.1

© ISO/IEC 2017 - All rights reserved

1329