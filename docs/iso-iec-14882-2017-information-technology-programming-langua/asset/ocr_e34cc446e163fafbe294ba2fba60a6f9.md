# ISO/IEC 14882:2017(E)

```
using reference = const T&;
using char_type = charT;
using traits_type = traits;
using istream_type = basic_istream<charT,traits>;

constexpr istream_iterator();
ististream_iterator(istream_type s);
istream_iterator(const istream_iterator& x) = default;
-istream_iterator() operator++() = default;

const T& operator*() const;
const T* operator->() const;
istream_iterator& operator++(int);
istream_iterator& operator++*(int);
private:
    basic_char<charT,traits> in_stream; // exposition only
    T value; // exposition only

template<class T, class charT, class traits, class Distance>
bool operator=(const istream_iterator<T,charT,traits,Distance>& x, y);
template<class T, class charT, class traits, class Distance>
bool operator+=(const istream_iterator<T,charT,traits,Distance>& x, y);

```

27.6.1.1 istream_iterator destructors and destructor [istream.iterator.cons

```
constexpr istream_iterator();

```

+   1 Effects: Constructs the end-of-stream iterator. If is_trivially_default_constructible_v<T> is true, then this constructor is a constexpr constructor.
2 Postconditions: in_stream == 0.
3 T* operator*();
Effects: Initializes in_stream with addressof(s). value may be initialized during construction or the first time it is referenced.
4 Postconditions: in_stream == addressof(s).
istream_iterator(const istream_iterator& x) = default;
5 Effects: Constructs a copy of x. If is_trivially_copy_constructible_v<T> is true, then this constructor is a trivial copy constructor.
6 Postconditions: in_stream == x.in_stream.
-istream_iterator() = default;

+   7 Effects: The iterator is destroyed. If is_trivially_destructible_v<T> is true, then this destructor is a trivial destructor.

27.6.1.2 istream_iterator operations [istream.iterator.ops]

+   1 T& operator*() const;
   Returns: value.

ISO/IEC 2017 - All rights reserved 978