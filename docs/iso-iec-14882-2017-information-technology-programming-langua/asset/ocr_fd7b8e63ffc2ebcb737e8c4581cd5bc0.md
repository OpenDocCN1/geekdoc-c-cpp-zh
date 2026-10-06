# ISO/IEC 14882:2017(E)

14 Returns: sp to indicate success, or pos_type(off_type(-1)) to indicate failure.

```
basic_stringbuf<charT, traits*> setbuf(charT* s, streamsize n);

```

15 Effects: implementation-defined, except that setbuf(0, O) has no effect.

16 Returns: this.

# 30.8.3 Class template basic_istream [ististream]

```
namespace std {
    template <class charT, class traits = traits<charT>>
    class Allocator = allocator<charT>
    class basic_istream : basic_istream<charT, traits> {
    public:
        using char_type = charT;
        using int_type = typename traits::int_type;
        using pos_type = typename traits::pos_type;
        using off_type = typename traits::off_type;
        using traits_type = traits;
        using allocator_type = Allocator;

```

```
// 30.8.3.1, constructors
    explicit basic_istream(
        ios_base::openmode mode = ios_base::in);
    explicit basic_istream(
        const basic_string<charT, traits, Allocator>& str,
        ios_base::openmode mode = ios_base::in);
    basic_istream(const basic_istream& rhs) = delete;
    basic_istream(const basic_istream& rhs);

```

```
// 30.8.3.2, assign and swap
    basic_istream& operator=(const basic_istream& rhs) = delete;
    basic_istream& operator=(basic_istream&& rhs);
    void swap(basic_istream& rhs);

```

```
// 30.8.3.3, members
    basic_stringbuf<charT, traits, Allocator>* rdbuf() const;
    basic_string<charT, traits, Allocator> str() const;
    void str(const basic_string<charT, traits, Allocator>& s) const;

```

```
    private:
        basic_stringbuf<charT, traits, Allocator> sb; // exposition only
    ;
```

```
    template <class charT, class traits, class Allocator>
    void swap(basic_istream<charT, traits, Allocator>& x,
             basic_istream<charT, traits, Allocator>& y);

```

The basic_istream<charT, traits, Allocator> supports reading objects of class basic_string<charT, traits, Allocator>. It uses a basic_stringbuf<charT, traits, Allocator> object to control the associated storage. For the sake of exposition, the maintained data is presented here as:

+   — sb, the stringbuf object.