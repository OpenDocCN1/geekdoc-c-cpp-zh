
# ISO/IEC 14882:2017(E)

```cpp
public:
    explicit codevct_utf8(size_t refs = 0);
    ~codevct_utf8();
```

```cpp
template <class Elm, unsigned long Maxime = 0x0ffff, codevct_mode Mode = (codevct_mode)>
class codevct_utf16 : public codevctElem<Elm, char, mbstate_t> {
public:
    explicit codevct_utf16(size_t refs = 0);
    ~codevct_utf16();
};
```

```cpp
template <class Elm, unsigned long Maxime = 0x0ffff, codevct_mode Mode = (codevct_mode)>
class codevct_utf8_utf16 : public codevctElem<Elm, char, mbstate_t> {
public:
    explicit codevct_utf8_utf16(size_t refs = 0);
    ~codevct_utf8_utf16();
};
```

## D.15.2 Requirements [depr.locale.stdct.req]

- 1 For each of the three conversion faces codevct_utf8, codevct_utf16, and codevct_utf16:
    - (1.1) Elm is the wide-character type, as wchar, char16_t, or char32_t.
    - (1.2) Maxime is the largest wide-character that the facet will read or write without reporting a conversion error.
    - (1.3) If (Mode & consumer_header), the facet shall consume an initial header sequence, if present, when reading a multibyte sequence to determine the endianness of the subsequent multibyte sequence to be read.
    - (1.4) If (Mode & generate_header), the facet shall generate an initial header sequence when writing a multibyte sequence to address the endianness of the subsequent multibyte sequence to be written.
    - (1.5) If (Mode & little_endian), the facet shall generate a multibyte sequence in little-endian order, as opposed to the big-endian order.
- 2 For the facet codevct_utf8:
    - (2.1) The facet shall convert between UTF-8 multibyte sequences and UCS2 or UCS4 (depending on the size of Elm) within the program.
    - (2.2) Endianness shall not affect how multibyte sequences are read or written.
    - (2.3) The multibyte sequences may be written as either a text or a binary file.
- 3 For the facet codevct_utf8_utf16:
    - (3.1) The facet shall convert between UTF-16 multibyte sequences and UCS2 or UCS4 (depending on the size of Elm) within the program.
    - (3.2) Multibyte sequences shall be written or read according to the Mode flag, as set out above.
    - (3.3) The multibyte sequences may be written only as a binary file. Attempting to write to a text file produces undefined behavior.
- 4 For the facet codevct_utf8_utf16:
    - (4.1) The facet shall convert between UTF-8 multibyte sequences and UTF-16 (one or two bit-codes) within the program.
    - (4.2) Endianness shall not affect how multibyte sequences are read or written.
    - (4.3) The multibyte sequences may be written as either a text or a binary file.

SEE ALSO: ISO/IEC 10646-1:1993.

## D.16 Deprecated conversion conversion interfaces

The header `<locale>` has the following additions:

```cpp
namespace std {
    template <Codecvt, class Elem = wchar_t,
        class Wide_alloc = allocator<Elem,
        class Byte_alloc = allocator<char>>
    wstring_convert;

    template <Codecvt, class Elem = wchar_t,
        class Tr = char_traits<Elem>
    class wbuffer_convert;
}
```

## D.16.1 Class template wstring_convert

Class `wstring_convert` performs conversions between a multibyte string and a byte string. It lets you specify a code conversion facet (like template codecvt) to perform the conversions, without affecting any streams or locales. [Example] If you want to use the code conversion facet `codecvt_utf8` to output to a UTF-8 multibyte sequence corresponding to a wide string, but you don't want to alter the locale for, you can write something like:

```cpp
wstring_convert<std::codecvt_utf8<wchar_t>> myconv;
std::wstring nstring(myconv.to_bytes(L"Hello"));
std::cout << nstring;
```

```cpp
namespace std {
    template <Codecvt, class Elem = wchar_t,
        class Wide_alloc = allocator<Elem,
        class Byte_alloc = allocator<char>>
    class wstring_convert {
    public:
        using byte_string = basic_string<char, char_traits<char>, Byte_alloc>;
        using wstring_string = basic_string<Elem, char_traits<Elem>, Wide_alloc>;
        using state_type = typename Codecvt::state_type;
        using int_type = typename Codecvt::traits_type::int_type;

        explicit wstring_convert(Codecvt* pcvt = new Codecvt);
        wstring_convert(Codecvt* pcvt, state_type state);
        explicit wstring_convert(const byte_string& byte_err);
        wstring_convert(const wide_string& wide_err = wide_string());
        ~wstring_convert();

        wstring_convert(const wstring_convert&) = delete;
        wstring_convert& operator=(const wstring_convert&) = delete;

        wide_string from_bytes(char* byte);
        wide_string from_bytes(const char* ptr);
        wide_string from_bytes(const byte_string& str);
        wide_string from_bytes(const char* first, const char* last);

        byte_string to_bytes(Elem wchar)
        byte_string_to_bytes(const Elem* wptr);
        byte_string_to_bytes(const wide_string& wstr);
        byte_string_to_bytes(const Elem* first, const Elem* last);

        size_t converted() const noexcept;
        state_type state() const;

    private:
        byte_string byte_err_string; // exposition only
        wide_string wide_err_string; // exposition only
        Codec cvptr; // exposition only
        state_type cvstate; // exposition only
        size_t cvcount; // exposition only;
};
```

- 2 The class template defines an object that controls conversions between wide string objects of class basic_string<char, char_traits<char>, Wide_alloc> and byte string objects of class basic_string<char, char_traits<char>, Byte_alloc>. The template defines the types wide_string and byte_string as synonyms for these types. The type wide_string and byte_string as a synonym for these types. Conversion between wide_string and byte_string is performed by an object of class Codecvt.

- 3 An object of this class template stores:
    - (3.1) byte_err_string — a conversion error
    - (3.2) wide_err_string — a conversion error
    - (3.3) cvptr — a pointer to the conversion-facet
    - (3.4) cvstate — the initial conversion state
    - (3.5) cvcount — the count

- 4 The type wide_string and byte_string as synonyms for these types. The type wide_string and byte_string as a synonym for these types. Conversion between wide_string and byte_string is performed by an object of class Codecvt.

- 5 The number of elements successfully converted shall be stored in cvcount.

- 6 The state of the conversion is returned.

- 7 In all cases:
    - (7.1) If the object was not constructed with an explicit value, it shall be set to its default value (the initial conversion state) before the conversion begins. Otherwise it shall be unchanged.
    - (7.2) If no error occurs, the member function shall return the converted string. Otherwise, if the object was constructed with a wide-error string, the member function shall throw an object of range_error.
