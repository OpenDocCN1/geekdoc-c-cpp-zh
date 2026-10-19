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

+   (1.1) — Elem is the wide-character type, such as wchar_t, char16_t, or char32_t.
+   (1.2) — Maxcode is the largest wide-character code that the facet will read or write without reporting a conversion error.
+   (1.3) — If (Mode & consume_header), the facet shall consume an initial header sequence, if present, when reading a multibyte sequence to determine the endianness of the subsequent multibyte sequence to be read.
+   (1.4) — If (Mode & generate_header), the facet shall generate an initial header sequence when writing a multibyte sequence to advertise the endianness of the subsequent multibyte sequence to be written.
+   (1.5) — If (Mode & little_endian), the facet shall generate a multibyte sequence in little-endian order, as opposed to the default big-endian order.

2 For the facet codecvt_utf8:

+   (2.1) — The facet shall convert between UTF-8 multibyte sequences and UCS-2 or UTF-32 (depending on the size of Elem) within the program.
+   (2.2) — Endianness shall not affect how multibyte sequences are read or written.
+   (2.3) — The multibyte sequences may be written as either a text or a binary file.

3 For the facet codecvt_utf16:

+   (3.1) — The facet shall convert between UTF-16 multibyte sequences and UCS-2 or UTF-32 (depending on the size of Elem) within the program.
+   (3.2) — Multibyte sequences shall be read or written according to the Mode flag, as set out above.
+   (3.3) — The multibyte sequences may be written only as a binary file. Attempting to write to a text file produces undefined behavior.