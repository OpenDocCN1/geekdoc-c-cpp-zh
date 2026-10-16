```
using char_type = C;
using traits_type = Tr;
using int_type = typename Tr::int_type;
using streambuf_type = basic_streambuf<C,Tr>;
using istream_type = basic_istream<C,Tr>;
// ...
};
```

The reference member of the iterator base is not used and is consequently left unspecified. If you use an istreambuf_iterator as an input iterator, its effect is like that of other input iterators:
a stream of characters can be read from input using c=*p++:

```
istreambuf_iterator p {};
istreambuf_iterator p {p2}; istreambuf_iterator p {is};
istreambuf_iterator p {psb}; istreambuf_iterator p {nullptr}; istreambuf_iterator p {prox}; p.~istreambuf_iterator() istreambuf_iterator<C,Tr> (§iso.24.6.3)
```

p is an end-of-stream iterator; noexcept; constexpr Copy constructor; noexcept
p is an iterator for is.rdbuf(); noexcept
p is an iterator to the istreambuf *psb; noexcept p is an end-of-stream iterator
p points to the istreambuf designated by prox; noexcept Destructor

c=*p c is the character returned by the streambuf’s sgetc() p->m The member m of *p, if that is a class object

p++p The streambuf’s sbumpc()
prox=p++ Let prox designate the same position as p; then ++p p.equal(p2) Are both p and p2, or neither, at end-of-stream

```
p==p2 p.equal(p2)
p!=p2 !p.equal(p2)
```

Note that any attempt to be clever when comparing istreambuf_iterators will fail: you cannot rely on two iterators referring to the same character while input is going on.

# 38.6.3.2 ostreambuf_iterator

An ostreambuf_iterator writes a stream of characters to an ostream_buffer:

```
template<typename C, typename Tr = char_traits<C>> // §iso.24.6.4
class ostreambuf_iterator
:public iterator<output_iterator_tag, void, void, void, void> {
public:
using char_type = C;
using traits_type = Tr;
using streambuf_type = basic_streambuf<C,Tr>;
using ostream_type = basic_ostream<C,Tr>;
// ...
};
```

By most measures, ostreambuf_iterator’s operations are odd, but the net effect is that if you use it as an output iterator, its effect is like that of other output iterators: a stream of