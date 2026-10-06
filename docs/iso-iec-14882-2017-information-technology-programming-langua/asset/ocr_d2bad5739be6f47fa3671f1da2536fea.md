# ISO/IEC 14882:2017(E)

```
constexpr move_iterator operator-(difference_type n) const;
constexpr move_iterator& operator=(difference_type n);
constexpr Iterator_unspecified operator[](difference_type n) const;
```

private:
Iterator current;
};

```
template <class Iterator, class Iterator2>
constexpr bool operator++(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator, class Iterator2>
constexpr bool operator--(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator, class Iterator2>
constexpr bool operator++(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator, class Iterator2>
constexpr bool operator--(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator, class Iterator2>
constexpr bool operator++(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator, class Iterator2>
constexpr bool operator--(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
```

```
template <class Iterator, class Iterator2>
constexpr operator-(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y) -> decltype(x.base() - y.base());
template <class Iterator>
constexpr operator*(
    typename iterator_traits<Iterator>::reference R, difference_type n, const move_iterator<Iterator>& x);
tntplate <class Iterator>
constexpr move_iterator(Iterator i);
}
```

+   1 R denote iterator_traits<Iterator>::reference. If is_reference_v<R> is true, the template specialization move_iterator<Iterator> shall define the type named reference as a synonym for remove_reference_t<R>; otherwise as for R.

# 27.5.3.2 move_iterator requirements [move.iter.ops]

+   1 The template Iterator shall meet the requirements of an iterator (27.2.3). Additionally, if any of the bidirectional or random access functions are instantiated, the template shall meet the requirements for a Birectional Iterator (27.2.6) or a Random Access Iterator (27.2.7), respectively.

# 27.5.3.3 move_iterator operations

# 27.5.3.3.1 move_iterator constructors [move.iter.op.const]

```
constexpr move_iterator();
```

+   1 Effects: Constructs a move_iterator, value-initializing current. Iterator operations applied to the resulting iterator have defined behavior if only if the corresponding operations are defined on a value-initialized iterator of type Iterator.

§ ISO/IEC –2017 – All rights reserved 974