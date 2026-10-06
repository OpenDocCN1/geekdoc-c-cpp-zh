# ISO/IEC 14882:2017(E)

where om is the open mode to the last call to open(). The operation fails if is_open() returns
false.

If sp is an invalid stream, or if the function neither sequence, the positioning operation
fails if sp has not been obtained by a previous successful call to one of the positioning operations
(seekoff and seekpos) on the same file the effects are undefined.

Returns: sp on success. Otherwise returns pos_type(off_type(-1)).

```
int sync() override;
```

Effects: If a put area exists, class filebuf::overflow write characters to the file, then flushes
the file by calling fflush(file). If a get area exists, the effect is implementation-defined.

```
void imbue(const locale& loc) override;
```

Requires: If the file is not positioned at some index and the encoding of the current locale is
determined by a_codecwt() is state-dependent (25.4.1.4.2) then it is the same as
the corresponding locale of file.

Effects: Characters inserted or extracted from the file can be decoded until one
another call of imbue. This may require reconversion of previously converted characters. In this turn may require
the implementation to reconstruct the original contents of the file.

# 30.9.3 Class template basic_ifream

```
namespace std {
    template <class charT, class charTtraits = char_traits<charT>>
    class basic_ifream : public basic_ifream<charT, charTtraits> {
    public:
        using char_type = charT;
        using int_type = typename traits::int_type;
        using pos_type = typename traits::pos_type;
        using off_type = typename traits::off_type;
        using traits_type = charTtraits;

        // 30.9.3.1, constructors
        basic_ifream();
        explicit basic_ifream(const char* s,
                               ios_base::openmode mode = ios_base::in);
        explicit basic_ifream(const filesystem& path,value_type* s,
                             ios_base::openmode mode = ios_base::in);
        explicit basic_ifream(const string& s,
                              ios_base::openmode mode = ios_base::in);
        explicit basic_ifream(const filesystem& path,
                              ios_base::openmode mode = ios_base::in);
        basic_ifream(const basic_ifream& rhs) = delete;
        basic_ifream(basic_ifream&& rhs) = delete;

        // 30.9.3.2, assign and swap
        basic_ifream& operator=(const basic_ifream& rhs) = delete;
        basic_ifream& operator=(basic_ifream&& rhs) = delete;
        void swap(basic_ifream& rhs);

        // 30.9.3.3, members
        basic_filebuf<charT, traits>* rdbuf() const;
```

30.9.3

©ISO/IEC 2017 - All rights reserved

1228