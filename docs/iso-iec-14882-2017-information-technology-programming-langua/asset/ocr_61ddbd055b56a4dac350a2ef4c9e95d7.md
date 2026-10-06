# ISO/IEC 14882:2017(E)

```
ostream_iterator& operator=(const T& value);

ostream_iterator& operator*();
ostream_iterator& operator++();
ostream_iterator& operator++(int);
```

```
private:
    basic_ostream<charT,traits> out_stream; // exposition only
                                // exposition only
    charT;
```

# 27.6.2.1 ostream_iterator constructors and destructor

> [ostream.iterator.cons]

ostream_iterator(const ostream_type& s);

+   1
2

Effects: Initializes out_stream with addressof(s) and delim null.

ostream_iterator(const ostream_type& s, const charT delimiter);

Effects: Initializes out_stream with addressof(s) and delim delimiter.

ostream_iterator(const ostream_iterator& x);

Effects: Constructs a copy of x.

-ostream_iterator();

Effects: The iterator is destroyed.

# 27.6.2.2 ostream_iterator operator operations

> [ostream.iterator.ops]

ostream_iterator& operator=(const T& value);

As if:

```
*out_stream << value;
if (delim == 0)
    *out_stream << delim;
return *this;
```

ostream_iterator& operator*();

Returns: *this.

```
ostream_iterator& operator++();
ostream_iterator& operator++(int);
```

Returns: *this.

# 27.6.3 Class template istream_bufiter

The class template istream_bufiter defines an input iterator (27.2.3) that reads characters from the streambuf for which access to the current character is provided. When each iterator is evaluated, the iterator advances to the next input. If the end of stream is reached (ambuf_type::getc() traits::eof()), the iterator becomes the end-of-stream iterator value. The default constructor istream_bufiter() and the constructor istream_bufiter(0) construct an end-of-stream iterator suitable for use as an end-of-range. All specializations of istream_bufiter shall have a trivial copy constructor, and a contextexpr default constructor, and a trivial destructor.

+   2. The result of operator*() on an end-of-stream iterator is undefined. For any other iterator value a char_type value is returned. It* is impossible to assign a character via an input iterator.

§ 27.6.3 ©ISO/IEC 2017 - All rights reserved 980