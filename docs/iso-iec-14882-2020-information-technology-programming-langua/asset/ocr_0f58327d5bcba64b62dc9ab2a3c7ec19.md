# 23.6.4.2 Class istreambuf_iterator::proxy [istreambuf.iterator.proxy]

1 Class istreambuf_iterator<charT,traits>::proxy is for exposition only. An implementation is permitted to provide equivalent functionality without providing a class with this name. Class istreambuf_iterator<charT, traits>::proxy provides a temporary placeholder as the return value of the post-increment operator (operator++). It keeps the character pointed to by the previous value of the iterator for some possible future access to get the character.

```
namespace std {
template<class charT, class traits>
class istreambuf_iterator<charT, traits>::proxy { // exposition only
    charT keep_;
    basic_streambuf<charT,traits>* sbuf_;
    proxy(charT c, basic_streambuf<charT,traits>* sbuf)
      : keep_(c), sbuf_(sbuf) { }
  public:
    charT operator*() { return keep_; }
  };
}
```

# 23.6.4.3 Constructors [istreambuf.iterator.cons]

1 For each istreambuf_iterator constructor in this subclause, an end-of-stream iterator is constructed if and only if the exposition-only member sbuf_ is initialized with a null pointer value.

```
constexpr istreambuf_iterator() noexcept;
constexpr istreambuf_iterator(default_sentinel_t) noexcept;
```

2 Effects: Initializes sbuf_ with nullptr.

```
istreambuf_iterator(istream_type& s) noexcept;
```

3 Effects: Initializes sbuf_ with s.rdbuf().

```
istreambuf_iterator(streambuf_type* s) noexcept;
```

4 Effects: Initializes sbuf_ with s.

```
istreambuf_iterator(const proxy& p) noexcept;
```

5 Effects: Initializes sbuf_ with p.sbuf_.

# 23.6.4.4 Operations [istreambuf.iterator.ops]

```
charT operator*() const;
```

1 Returns: The character obtained via the streambuf member sbuf_->sgetc().

```
istreambuf_iterator& operator++();
```

2 Effects: As if by sbuf_->sbumpc().
3 Returns: *this.

```
proxy operator++(int);
```

4 Returns: proxy(sbuf_->sbumpc(), sbuf_).

```
bool equal(const istreambuf_iterator& b) const;
```

5 Returns: true if and only if both iterators are at end-of-stream, or neither is at end-of-stream, regardless of what streambuf object they use.

```
template<class charT, class traits>
bool operator==(const istreambuf_iterator<charT,traits>& a,
                const istreambuf_iterator<charT,traits>& b);
```

6 Returns: a.equal(b).