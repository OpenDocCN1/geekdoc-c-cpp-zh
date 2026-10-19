
# ISO/IEC 14882:2020(E)

```
};
}
```

1 The class ostrstream supports the writing of objects of class strstreambuf. It supplies a strstreambuf object to control the associated array object. For the sake of exposition, the maintained data is presented here as:

- (1.1) — sb, the strstreambuf object.

## D.13.4.2 ostrstream constructors [depr.ostrstream.cons]

```
ostrstream();
```

1 Effects: Initializes the base class with ostream(&sb) and sb with strstreambuf().

```
ostrstream(char* s, int n, ios_base::openmode mode = ios_base::out);
```

2 Effects: Initializes the base class with ostream(&sb), and sb with one of two constructors:

- (2.1) — If (mode & app) == 0, then s shall designate the first element of an array of n elements. The constructor is strstreambuf(s, n, s).

- (2.2) — If (mode & app) != 0, then s shall designate the first element of an array of n elements that contains an NTBS whose first element is designated by s. The constructor is strstreambuf(s, n, s + std::strlen(s)).331

## D.13.4.3 Member functions [depr.ostrstream.members]

```
strstreambuf* rdbuf() const;
```

1 Returns: (strstreambuf*)&sb.

```
void freeze(bool freezefl = true);
```

2 Effects: Calls rdbuf()->freeze(freezefl).

```
char* str();
```

3 Returns: rdbuf()->str().

```
int pcount() const;
```

4 Returns: rdbuf()->pcount().

# D.13.5 Class strstream [depr.strstream]

## D.13.5.1 General [depr.strstream.general]

```
namespace std {
  class strstream
    : public basic_iostream<char> {
  public:
    // types
    using char_type = char;
    using int_type  = char_traits<char>::int_type;
    using pos_type  = char_traits<char>::pos_type;
    using off_type  = char_traits<char>::off_type;

    // constructors/destructor
    strstream();
    strstream(char* s, int n,
        ios_base::openmode mode = ios_base::in|ios_base::out);
    virtual ~strstream();

    // members
    strstreambuf* rdbuf() const;
    void freeze(bool freezefl = true);
    int pcount() const;
    char* str();
```

> 331) The function signature strlen(const char*) is declared in <cstring> (21.5.3).

```
template<class T>
    bool atomic_compare_exchange_weak(shared_ptr<T>* p, shared_ptr<T>* v, shared_ptr<T> w);
template<class T>
    bool atomic_compare_exchange_strong(shared_ptr<T>* p, shared_ptr<T>* v, shared_ptr<T> w);
template<class T>
    bool atomic_compare_exchange_weak_explicit(
        shared_ptr<T>* p, shared_ptr<T>* v, shared_ptr<T> w,
        memory_order success, memory_order failure);
template<class T>
    bool atomic_compare_exchange_strong_explicit(
        shared_ptr<T>* p, shared_ptr<T>* v, shared_ptr<T> w,
        memory_order success, memory_order failure);
```

Concurrent access to a `shared_ptr` object from multiple threads does not introduce a data race if the access is done exclusively via the functions in this subclause and the instance is passed as their first argument.

The meaning of the arguments of type `memory_order` is explained in [31.4](#).

```
template<class T> bool atomic_is_lock_free(const shared_ptr<T>* p);
```

*Requires:* p shall not be null.

*Returns:* true if atomic access to *p is lock-free, false otherwise.

*Throws:* Nothing.

```
template<class T> shared_ptr<T> atomic_load(const shared_ptr<T>* p);
```

*Requires:* p shall not be null.

*Returns:* `atomic_load_explicit(p, memory_order::seq_cst)`.

*Throws:* Nothing.

```
template<class T> shared_ptr<T> atomic_load_explicit(const shared_ptr<T>* p, memory_order mo);
```

*Requires:* p shall not be null.

*Requires:* mo shall not be `memory_order::release` or `memory_order::acq_rel`.

*Returns:* `*p`.

*Throws:* Nothing.

```
template<class T> void atomic_store(shared_ptr<T>* p, shared_ptr<T> r);
```

*Requires:* p shall not be null.

*Effects:* As if by `atomic_store_explicit(p, r, memory_order::seq_cst)`.

*Throws:* Nothing.

```
template<class T> void atomic_store_explicit(shared_ptr<T>* p, shared_ptr<T> r, memory_order mo);
```

*Requires:* p shall not be null.

*Requires:* mo shall not be `memory_order::acquire` or `memory_order::acq_rel`.

*Effects:* As if by `p->swap(r)`.

*Throws:* Nothing.

```
template<class T> shared_ptr<T> atomic_exchange(shared_ptr<T>* p, shared_ptr<T> r);
```

*Requires:* p shall not be null.

*Returns:* `atomic_exchange_explicit(p, r, memory_order::seq_cst)`.

*Throws:* Nothing.

```
template<class T>
    shared_ptr<T> atomic_exchange_explicit(shared_ptr<T>* p, shared_ptr<T> r, memory_order mo);
```

*Requires:* p shall not be null.

*Effects:* As if by `p->swap(r)`.

# D.21.2 Header <codecvt> synopsis [depr.codecvt.syn]

```
namespace std {
    enum codecvt_mode {
        consume_header = 4,
        generate_header = 2,
        little_endian = 1
    };

    template<class Elem, unsigned long Maxcode = 0x10ffff, codecvt_mode Mode = (codecvt_mode)0>
    class codecvt_utf8 : public codecvt<Elem, char, mbstate_t> {
    public:
        explicit codecvt_utf8(size_t refs = 0);
        ~codecvt_utf8();
    };

    template<class Elem, unsigned long Maxcode = 0x10ffff, codecvt_mode Mode = (codecvt_mode)0>
    class codecvt_utf16 : public codecvt<Elem, char, mbstate_t> {
    public:
        explicit codecvt_utf16(size_t refs = 0);
        ~codecvt_utf16();
    };

    template<class Elem, unsigned long Maxcode = 0x10ffff, codecvt_mode Mode = (codecvt_mode)0>
    class codecvt_utf8_utf16 : public codecvt<Elem, char, mbstate_t> {
    public:
        explicit codecvt_utf8_utf16(size_t refs = 0);
        ~codecvt_utf8_utf16();
    };
}
```

# D.21.3 Requirements [depr.locale.stdcvt.req]

1 For each of the three code conversion facets codecvt_utf8, codecvt_utf16, and codecvt_utf8_utf16:

- (1.1) — Elem is the wide-character type, such as wchar_t, char16_t, or char32_t.
- (1.2) — Maxcode is the largest wide-character code that the facet will read or write without reporting a conversion error.
- (1.3) — If (Mode & consume_header), the facet shall consume an initial header sequence, if present, when reading a multibyte sequence to determine the endianness of the subsequent multibyte sequence to be read.
- (1.4) — If (Mode & generate_header), the facet shall generate an initial header sequence when writing a multibyte sequence to advertise the endianness of the subsequent multibyte sequence to be written.
- (1.5) — If (Mode & little_endian), the facet shall generate a multibyte sequence in little-endian order, as opposed to the default big-endian order.

2 For the facet codecvt_utf8:

- (2.1) — The facet shall convert between UTF-8 multibyte sequences and UCS-2 or UTF-32 (depending on the size of Elem) within the program.
- (2.2) — Endianness shall not affect how multibyte sequences are read or written.
- (2.3) — The multibyte sequences may be written as either a text or a binary file.

3 For the facet codecvt_utf16:

- (3.1) — The facet shall convert between UTF-16 multibyte sequences and UCS-2 or UTF-32 (depending on the size of Elem) within the program.
- (3.2) — Multibyte sequences shall be read or written according to the Mode flag, as set out above.
- (3.3) — The multibyte sequences may be written only as a binary file. Attempting to write to a text file produces undefined behavior.

# ISO/IEC 14882:2020(E)

4 For the facet codecvt_utf8_utf16:

- (4.1) — The facet shall convert between UTF-8 multibyte sequences and UTF-16 (one or two 16-bit codes) within the program.
- (4.2) — Endianness shall not affect how multibyte sequences are read or written.
- (4.3) — The multibyte sequences may be written as either a text or a binary file.

5 The encoding forms UTF-8, UTF-16, and UTF-32 are specified in ISO/IEC 10646. The encoding form UCS-2 is specified in ISO/IEC 10646:2003.332

# D.22 Deprecated convenience conversion interfaces [depr.conversions]

## D.22.1 General [depr.conversions.general]

1 The header <locale> (28.2) has the following additions:

```
namespace std {
    template<class Codecvt, class Elem = wchar_t,
            class WideAlloc = allocator<Elem>,
            class ByteAlloc = allocator<char>>
    class wstring_convert;

    template<class Codecvt, class Elem = wchar_t,
            class Tr = char_traits<Elem>>
    class wbuffer_convert;
}
```

## D.22.2 Class template wstring_convert [depr.conversions.string]

1 Class template wstring_convert performs conversions between a wide string and a byte string. It lets you specify a code conversion facet (like class template codecvt) to perform the conversions, without affecting any streams or locales.

> [Example 1: If you want to use the code conversion facet codecvt_utf8 to output to cout a UTF-8 multibyte sequence corresponding to a wide string, but you don’t want to alter the locale for cout, you can write something like:
> wstring_convert<std::codecvt_utf8<wchar_t>> myconv;
> std::string mbstring = myconv.to_bytes(L"Hello\n");
> std::cout << mbstring;
> — end example]

```
namespace std {
    template<class Codecvt, class Elem = wchar_t,
            class WideAlloc = allocator<Elem>,
            class ByteAlloc = allocator<char>>
    class wstring_convert {
    public:
        using byte_string = basic_string<char, char_traits<char>, ByteAlloc>;
        using wide_string = basic_string<Elem, char_traits<Elem>, WideAlloc>;
        using state_type = typename Codecvt::state_type;
        using int_type = typename wide_string::traits_type::int_type;

        wstring_convert() : wstring_convert(new Codecvt) {}
        explicit wstring_convert(Codecvt* pcvt);
        wstring_convert(Codecvt* pcvt, state_type state);
        explicit wstring_convert(const byte_string& byte_err,
                                 const wide_string& wide_err = wide_string());

        ~wstring_convert();

        wstring_convert(const wstring_convert&) = delete;
        wstring_convert& operator=(const wstring_convert&) = delete;

        wide_string from_bytes(char byte);
        wide_string from_bytes(const char* ptr);
        wide_string from_bytes(const byte_string& str);
        wide_string from_bytes(const char* first, const char* last);
```

332) Cancelled and replaced by ISO/IEC 10646:2017.
